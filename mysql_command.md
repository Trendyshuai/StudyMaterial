## 启动MySQL服务
``` shell
[root@69~ #]> systemctl start mysqld.service
```

## 查看初始密码
``` shell
[root@69~ #]> grep "temporary password" /var/log/mysqld.log
```

## 修改默认密码
``` sql
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';
```

## 退出MySQL
``` sql
mysql> QUIT
```

