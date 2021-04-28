# linux安装jenkins

## 安装Java
``` cmd
yum install -y java
```

## 安装Jenkins

### 添加yum仓库
yum的repo中默认没有jenkins，需要先将jenkins的存储库添加到yum repos
``` cmd
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
### 安装
``` cmd
通过yum，下载jenkins
```
### 启动
``` cmd
service jenkins start
```