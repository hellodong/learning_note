
##开源包打补丁
1) quilt new 001-xxxx.patch
2) quilt add xx/old.xx
3) cp new.xx xx/old.xx (将老文件覆盖)
4) quilt diff
5) quilt refresh
6) cp patches/001-xxx.patch xxxxx/patches/
