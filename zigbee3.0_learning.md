## JN-UG-3101-PRO Stack

##### Descriptors
There are three mandatory descriptors and two optional descriptors stored in a node. The mandatory descriptors are the Node, Node Power and Simple descriptors, while 
the optional descriptors are called the Complex and User descriptors
For each node, there is only one Node and Node Power descriptor, but there is a 
Simple descriptor for each endpoint. There may also be Complex and User 
descriptors in the device.

##### Starting Routers and End Devices
process to join a network:
1) **Searches for a network to join**,ZPS_eAplZdoStartStack(),the device searches for 
networks by listening for beacons from Routers and Co-ordinators of ZigBee 
PRO networks in the neighbourhood; pre-set EPID value is zero, ZPS_EVENT_NWK_DISCOVERY_COMPLETE stack event
2) **Selects a network to join**, On the basis of the results in ZPS_EVENT_NWK_DISCOVERY_COMPLETE  
3) **Submits a join request to network**, the function 
ZPS_eAplZdoJoinNetwork() must be called to submit the request.The 
outcome of this request is reported in one of the following stack events on the 
requesting device:  
ZPS_EVENT_NWK_JOINED_AS_ROUTER (if joined as Router)  
ZPS_EVENT_NWK_JOINED_AS_ENDDEVICE (if joined as End Device)  
ZPS_EVENT_NWK_FAILED_TO_J OIN (if failed to join)  
In the case of success, the above stack event contains the 16-bit network 
address that the network has allocated to the local device. In addition, the event 
ZPS_EVENT_NWK_NEW_NODE_HAS_JOINED is generated on the parent.
If the case of failure, the device can attempt another join by calling 
ZPS_eAplZdoJoinNetwork() with a different result reported in the 
ZPS_EVENT_NWK_DISCOVERY_COMPLETE event.

#### Discovering the Network
##### Obtaining Network Properties
ZPS_eAplZdoStartStack()--> ZPS_eAplZdoDiscoverNetworks(), Both of these function calls eventually result in the stack event 
ZPS_EVENT_NWK_DISCOVERY_COMPLETE on the End Device or Router, where 
this event reports the following properties of the discovered networks:  
Extended PAN ID  
ZigBee version  
ZigBee stack profile  

#### Binding
##### Binding Endpoints
ZPS_eAplZdoBind() creates a one-to-one binding to a single remote endpoint.  
ZPS_eAplZdoBindGroup() creates a one-to-many binding for which the 
destination endpoints are specified via a group address  


#### Transferring Data
##### Sending Data
There are five ways to send data to one or more remote nodes:  
**Unicast**:  Sending data to a single destination endpoint  
**Broadcast**: Sending data to (potentially) all endpoints
**Group Multicast**:  Sending data to a group of endpoints  
**Bound Transfer**:  Sending data to bound endpoints  
**Inter-PAN Transfer**: Sending data to another ZigBee PRO network  
ZPS_eAplAfApsdeDataReq() can be used 
which imposes no restrictions on the destination address, destination application 
profile, destination cluster and destination endpoint number.

##### Unicast

ZPS_eAplAfUnicastDataReq() is used to send a data packet to an endpoint 
on a node with a given network address.  
These functions  request end-to-end acknowledgements 
which, when received, generate ZPS_EVENT_APS_DATA_ACK events (note that the 
‘next hop’ ZPS_EVENT_APS_DATA_CONFIRM  events will also be generated).  
A timeout of approximately 1600 ms is applied to the acknowledgements. If an 
acknowledgement has not been received within the timeout period, the data is re-sent, and up to 3 more re-tries can subsequently be performed before the data transfer is abandoned completely.

##### Receiving Data
When a data packet  is received by the destination node, it is put into a message queue. A ZPS_EVENT_AF_DATA_INDICATION stack event is generated on the destination node to indicate that a data packet has arrived (the destination endpoint is indicated in this event). The packet must then be collected from the message queue using the RTOS function  OS_eCollectMessage().  
An End Device which is asleep will be unable to receive a data packet directly, so the data is buffered by its parent for collection later. The End Device must explicitly request this data, once awake.  
##### Polling for Data
In the case of an End Device which is capable of sleeping, messages are not delivered directly to the device, since it may be  asleep when the messages arrive. Instead, the messages are temporarily buffered by the End Device’s parent. Once awake, the End Device can then ask or ‘poll’ its parent for data.  
Data polling is performed using the function ZPS_eAplZdoPoll() in the End Device application. This function requests the buffered data and should normally be called immediately after waking from sleep. If the poll request is successfully sent to the parent, a ZPS_EVENT_NWK_POLL_CONFIRM  stack event will occur on the End Device. The subsequent arrival of data from the parent is indicated by the stack event ZPS_EVENT_AF_DATA_INDICATION. Any messages forwarded from the parent should then be collected from the relevant message queue using the RTOS function OS_eCollectMessage().

#### Leaving and Rejoining the Network
A node can be intentionally removed from the network using the function 
ZPS_eAplZdoLeaveNetwork() , which issues a leave request.

If the node successfully rejoins the network, the stack event 
ZPS_EVENT_NWK_NEW_NODE_HAS_JOINED is generated on the parent node 
and one of the following stack events is generated on the joined node:  
ZPS_EVENT_NWK_JOINED_AS_ROUTER (if joined as a Router)  
ZPS_EVENT_NWK_JOINED_AS_ENDDEVICE (if joined as an End Device)  
If the join request is unsuccessful, the ZPS_EVENT_NWK_FAILED_TO_JOIN event 
is generated on the requesting node.


## JN-UG-3076 ZigBee Home Automation User Guide

## JN-UG-3103 ZigBee Cluster Library

#### Power Configuration Cluster(0x0001)
Four attribute sets:Mains Information, Mains Settings, Battery Information and Battery Settings
##### Mains Information Attribute Set
1) u16MainsVoltage,measured AC (RMS) mains voltage or DC voltage 
currently applied to the device, in units of 100 mV.  
2) u8MainsFrequency, 0x00 indicates a DC supply or that AC frequency is too low to be measured.  
3) u8MainsAlarmMask, is a bitmap indicating which mains voltage alarms can be 
generated (a bit is set to ‘1’ if the alarm is enabled):
<table>
    <tr>
        <td>**Bit**</td>
        <td>**Description**</td>
    </tr>
    <tr>
        <td>0</td>
        <td>Under-voltage alarm (triggered when measured RMS mains 
voltage falls below a pre-defined threshold)</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Over-voltage alarm (triggered when measured RMS mains 
voltage rises above a pre-defined threshold )</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Mains power supply has been lost or is unavailable - that is, 
the device is now running on battery power.  This value is 
part of the HA extension to the cluster</td>
    </tr>
    <tr>
        <td>3~7</td>
        <td>reserverd</td>
    </tr>
</table>
4) u16MainsVoltageMinThreshold is the threshold for the under-voltage 
alarm, in units of 100 mV.  
5) u16MainsVoltageMaxThreshold is the threshold for the over-voltage 
alarm, in units of 100 mV.  
6) u16MainsVoltageDwellTripPoint, defines the time-delay.  

##### Battery Information Attribute Set(Battery 1)
1) u8BatteryVoltage,  is the measured battery voltage currently applied to the 
device, in units of 100 mV.  
2) u8BatteryPercentageRemaining  indicates the remaining battery life as a  
percentage of the complete battery lifespan, expressed to the nearest half-percent  in the range 0 to 100 - for example, 0xAF represents 87.5%.  
##### Battery Settings Attribute Set(Battery 1)
1) u8BatterySize,  is an enumeration indicating the type of battery in the device, listed:
``` c
typedef enum 
{
    E_CLD_PWRCFG_BATTERY_SIZE_NO_BATTERY    = 0x00,
    E_CLD_PWRCFG_BATTERY_SIZE_BUILT_IN,
    E_CLD_PWRCFG_BATTERY_SIZE_OTHER,
    E_CLD_PWRCFG_BATTERY_SIZE_AA,
    E_CLD_PWRCFG_BATTERY_SIZE_AAA,
    E_CLD_PWRCFG_BATTERY_SIZE_C,
    E_CLD_PWRCFG_BATTERY_SIZE_D,
    E_CLD_PWRCFG_BATTERY_SIZE_UNKNOWN       = 0xff,
} teCLD_PWRCFG_BatterySize;
```
2) u8BatteryQuantity, is the number of batteries used to power the device.
3) u8BatteryPercentageMinThreshold,  is the minimum alarm threshold for 
percentage battery-life, expressed in half-percent steps in the range 0 to 100 - if the remaining percentage battery-life ( u8BatteryPercentageRemaining ) 
falls below this threshold, an alarm can be triggered.  
4) u32BatteryAlarmState, is a bitmap repesenting the current state of the 
alarms for the battery or batteries (the  bitmap includes status bits for optional additional batteries 2 and 3). It indicates the state of the battery in relation to the voltage and percentage-life thresholds  defined by the attributes above (a bit is set to ‘1’ when the corresponding threshold has been reached).  listed:
<table>
    <tr>
        <td>Bit</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>0</td>
        <td>Bit is set if one of the following thresholds has been reached:<br>
1)u8BatteryVoltageThreshold1 <br>   
2)u8BatteryPercentageThreshold1</td>
    </tr>
</table>





