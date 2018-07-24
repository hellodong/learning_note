
# 变量自加

* a=1  
* **a=$(($a+1))** （openwrt 支持）  
* a=$[$a+1]  
* a=`expr $a + 1`  
* let a++  
* let a+=1  
* ((a++))  

# while循环

## 数字比较
```shell
while [$count -le 6];do
    count=$(($count+1))
done
```
## 整数表达式
- -eq 数值相等
- -ne 数值不等
- -gt 第一个数>第二个数
- -lt 第一个数<第二个数
- -le 第一个数<=第二个数
- -ge 第一个数>=第二个数
