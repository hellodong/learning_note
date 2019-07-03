## #交叉编译gdb调试
目标机 gdbserver host_ip:port program arg1 arg2 ...
主机 交叉编译工具链-gdb target_ip:port program

##### 设置程序输入参数
1) (gdb) run arg1 arg2
2) (gdb) set args arg1 arg2
3) 显示输入参数: (gdb) show args


