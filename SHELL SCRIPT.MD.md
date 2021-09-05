## <center>Linx脚本运行</center>

文件目录./root
* NginxStatus.sh
* RunSendEmail.sh
* <font color='red'>sendEmail-v1.56</font>

Shell脚本文件
* NginxStatus.sh
* RunSendEmail.sh

执行命令
1. 查看Nginx状态
`# bash NginxStatus.sh`
2. 发送电子邮件
`# bash RunSendEmai.sh`

修改邮件发送配置
1. 进入<font color='red'>sendEmail-v1.56</font>文件夹
`# cd sendEmail-v1.56`
2. 编辑sendemail.sh文件
`# vim sendemail.sh`
3. 修改配置
```shell
#!/bin/bash

#接收者邮箱 可以写多个 用空格隔开
email_reciver="trendyshuai@sohu.com"

#发送者邮箱
email_sender=18340815237@163.com

#发送者用户名
email_username=18340815237@163.com

#发送者密码
email_password=ly666666

#附件路径
#file1_path="path1"
#file2_path="path2"

#服务器
email_smtphost=smtp.163.com

#邮件标题
email_title="Linux Shell Script Test"

#邮件内容
email_content="This is test content!"

#发送邮件
./sendEmail -f ${email_sender} -t ${email_reciver} -s ${email_smtphost} -u ${email_title} -xu ${email_username} -xp ${email_password} -m ${email_content} -a ${file1_path} ${file2_path} -o message-charset=utf-8

```




<hr>
#### 常见问题

运行发送邮件脚本时报如下错误：
```
*******************************************************************
 Using the default of SSL_verify_mode of SSL_VERIFY_NONE for client
 is deprecated! Please set SSL_verify_mode to SSL_VERIFY_PEER
 possibly with SSL_ca_file|SSL_ca_path for verification.
 If you really don't want to verify the certificate and keep the
 connection open to Man-In-The-Middle attacks please set
 SSL_verify_mode explicitly to SSL_VERIFY_NONE in your application.
*******************************************************************
  at /usr/local/bin/sendEmail line 1906.
invalid SSL_version specified at /usr/share/perl5/vendor_perl/IO/Socket/SSL.pm line 444.
```
* 解决方案
CentOS 7.3上Perl版本为5.16，使用sendEmail-v1.56似乎要使用5.10版本的Perl才能够成功发送邮件。

<b>下载并安装Perl-5.10</b>
```
# wget http://www.cpan.org/src/5.0/perl-5.10.0.tar.gz
# tar zxf perl-5.10.0.tar.gz
# cd perl-5.10.0
# ./configure.gnu -des -Dprefix=/usr/local/perl
# echo $?  (返回0，编译没问题)
# make
# make test
# make install
# mv /usr/bin/perl /usr/bin/perl.bak  (备份原来的Perl)
# ln -s /usr/local/perl/bin/perl /usr/bin/perl
# perl -v  (查看Perl版本，显示5.10表示已经成功)
```
