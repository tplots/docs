# systemctl

#### 说明
```
System V init 命令
systemctl命令
```


#### 启动服务
```
service foo start
systemctl start foo.service
```
#### 重启服务
```
service foo restart
systemctl restart foo.service
```

#### 停止服务
```
service foo stop
systemctl stop foo.service
```

#### 重加载配置文件(不终止服务)
```service foo reload
systemctl reload foo.service
```

#### 查看服务状态
```
service foo status
systemctl status foo.service
```

#### 开机自动启动
```
chkconfig foo on
systemctl enable foo.service
```

#### 开机不自动启动
```
chkconfig foo off
systemctl disable foo.servie
```


#### 查看特定服务是否为开机自动启动
```
chkconfig foo
systemctl is-enable foo.service
```


#### 查看各个级别下服务的启动与禁用情况
```
chkconfig --list
systemctl list-unit-files --type=service
```