# <center>Linux学习笔记</center>
### <font color='#22ffdd'>常用命令</font>
* 解压tar.gz文件
```
tar -zxvf filename.tar.gz
```
* 安装软件
```
sudo apt-get install -i appname
```
* 创建目录
```
mkdir Directory
```
* 删除指定目录
```
rmdir Directory
```
* 关机、重启
```
shutdown && shutdown -r
```
* 安装软件
```
sudo apt-get install -i appname
```
### <font color='#22ffdd'>双系统时间</font>
```
sudo apt-get update
sudo apt-get install ntpdate
sudo ntpdate time.windows.com

sudo hwclock --localtime --systohc
```