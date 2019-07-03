#### 下载文件

curl <--limit-rate>:限制下载速度, curl --limit-reate 2K   下载速度限制为2K  

curl <-s>:去掉下载显示信息  

curl <-C>: 断点续传, curl -C - -O [url] 

curl <-O>:下载保存文件, curl -O [url]  下载文件名为url 的尾坠

curl <-o>: 下载保存文件另存为, curl -o [file_name] [url]

curl -s --limit-rate 100K -C - -o /tmp/fw.bin http://saascloud.oss-cn-shanghai.aliyuncs.com/fireware/fw-1562035080401-108407.bin