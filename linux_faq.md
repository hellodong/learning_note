主要有3种方法：

1. 用ln将需要的so文件链接到/usr/lib或者/lib这两个默认的目录下边

ln -s /where/you/install/lib/*.so /usr/lib

sudo ldconfig -v

2.修改LD_LIBRARY_PATH

export LD_LIBRARY_PATH=/where/you/install/lib:$LD_LIBRARY_PATH

sudo ldconfig -v

 

3.修改/etc/ld.so.conf，然后刷新

vim /etc/ld.so.conf

add /where/you/install/lib

sudo ldconfig -v
