# 安装Nginx
```
https://www.cnblogs.com/architectforest/p/12755195.html
https://nginx.org/en/linux_packages.html#RHEL-CentOS
```

### 设置www目录所属  防止502
``` cmd
chown -R nginx:nginx /var/www
```


## 参考配置
### ./nginx.conf文件
```
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```

### ./conf.d/配置文件目

#### www.plots.cn.conf
``` conf
server {
    listen 80;
    #SSL 访问端口号为 443
    listen 443 ssl;
    #填写绑定证书的域名
    server_name www.plots.cn;
    #证书文件名称
    ssl_certificate ssl/www.plots.cn/1_www.plots.cn_bundle.crt;
    #私钥文件名称
    ssl_certificate_key ssl/www.plots.cn/2_www.plots.cn.key;
    ssl_session_timeout 5m;
    #请按照以下协议配置
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
    ssl_prefer_server_ciphers on;

    root /var/www/plots.cn;
}
```

#### api.plots.cn.conf
``` conf
# api.plots.cn.conf 配置  代理api域名
server {
  listen 80;
  server_name api.plots.cn;

      location / {
        proxy_redirect off;
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```
