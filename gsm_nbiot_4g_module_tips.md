## 移远BG96/BG36
AT <cr> -- 是否连接好  
AT+CPIN?  返回ready -- 已经插入卡  
AT+CGREG? 0,1 -- 已经注册网络  
AT+COPS? -- 当前加入网络  

#### AT+CGDCONT PDP context 移动场景
AT+CGDCONT?  -- 当前PDP内容  
AT+CGDCONT=1,"IP",APN -- 定义PDP context

#### AT+CGACT 附着网络
AT+CGACT=state,cid

## 广合同G510 

POWER_ON:
      电平一直为高，拉底800ms，再拉高   模块上线
RESET:
    一直拉底紧急复位

USART1   ---> 9600 波特率
USART2  --->115200 波特率


AT 指令调试：
    AT --- 功能是否上线
    AT+CSQ -- 网络信号
    AT+CREG -- 网络是否注册成功，<0, 1> 表示成功
    AT+COPS? -- 当前能加入的网络
    AT+CGDCONT=1,"IP","" -- 设置环境，APN
    AT+CGATT？ -- 网络附着，1 -- 附着成功，0 -- 失败
    
    AT+CGACT？ -- PDP 是否激活上线
    AT+CGACT=1 -- 激活PDP<1> 上线