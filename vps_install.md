## <center>`trojan一键脚本，开启TLS1.3，系统支持centos7+/debian9+/ubuntu16+`</center>
#
### 1、执行以下脚本，然后选择1，安装trojan，然后输入解析到VPS的域名，回车安装即可。注意：安装时不要开启CDN，否则会提示IP地址不匹配。
```
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```
### 2、BBR加速
```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

<br><br>

## <center>`最稳定的翻墙方式：v2ray tls1.3 | v2ray一键脚本 | v2ray ws tls1.3教程`</center>
#
### 1、使用SSH工具连接VPS，执行下列命令，选择安装v2ray+ws+tls
```
curl -O https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls1.3.sh && chmod +x v2ray_ws_tls1.3.sh && ./v2ray_ws_tls1.3.sh
```
### 2、BBR加速
```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

<br><br>

## <center>`最稳的上网方式：v2ray+ws+tls一键脚本（CentOS7版）`</center>
#
### 1、使用SSH工具连接VPS，执行下列命令，选择安装v2ray+ws+tls
```
curl -O https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls.sh && chmod +x v2ray_ws_tls.sh && ./v2ray_ws_tls.sh
```
### 2、安装BBR加速（可不安装，或自行开启bbr），下面命令，分享自网络
```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
### 3、重启后键入
```
cd /usr/src && ./tcp.sh
```