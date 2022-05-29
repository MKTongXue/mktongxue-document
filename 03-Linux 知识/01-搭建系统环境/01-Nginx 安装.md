# 1 Linux 系统安装 Nginx

## 1.1 安装Nginx

```text
# 新建 mktongxue 文件夹
cd /usr
mkdir mktongxue
cd mktongxue

# 安装前置环境，避免出错
yum -y install pcre-devel openssl openssl-devel

# 下载安装包
wget http://nginx.org/download/nginx-1.18.0.tar.gz

# 解压
tar -zxvf nginx-1.18.0.tar.gz
cd nginx-1.18.0

# /usr/local/nginx 配置时更换为实际希望安装路径即可
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
make && make install

# 安装完后验证是否安装成功
cd /usr/local/nginx/sbin
./nginx -t 

# 出现如下内容为安装成功
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

# 启动 Nginx
./nginx

# 浏览器访问服务器 IP 地址，出现 Nginx 欢迎页面
```

![安装 Nginx 成功](http://image.mktongxue.com/202205/011.png)

![启动 Nginx 成功](http://image.mktongxue.com/202205/012.png)


## 1.2 安装 SSL 证书

（1）
```text
# 进入 Nginx 默认安装目录，如果您修改过默认安装目录，请根据实际配置进行调整。
cd /usr/local/nginx/conf

# 创建证书目录，命名为 cert
mkdir cert
cd cert

# 上传证书
```
![上传 SSL 证书](http://image.mktongxue.com/202205/013.png)


（2）
```text
# 编辑配置文件
vim /usr/local/nginx/conf/nginx.conf

# 进入编辑模式
i

# 保存并退出
Esc 键
:wq
```


（3）配置文件 nginx.conf 内容
```text
server {
    listen       80;
    server_name  mktongxue.com;
    rewrite ^(.*)$ https://$host$1;

    location / {
        # Web 网站程序存放目录
        # root  /usr/local/webapp;
        index   index.html index.htm;
    }

    # 默认的，未修改
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root   html;
    }
}

server {
    listen       443 ssl;
    server_name  mktongxue.com;

    ssl_certificate      cert/mktongxue.com.pem;
    ssl_certificate_key  cert/mktongxue.com.key;

    # ssl_session_cache  shared:SSL:1m;
    ssl_session_timeout  5m;

    # 表示使用的加密套件的类型
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    # 表示使用的 TLS 协议的类型
    ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;

    location / {
        # Web 网站程序存放目录
        root   /usr/local/webapp;
        index  index.html index.htm;
    }

    # /prod-api/ 是我前端项目 API 路径
    # http://127.0.0.1:8003/ 后端 gateway 微服务
	location /prod-api/ {
        proxy_pass http://127.0.0.1:8003/;
    }
}

```


（4）启动
```text
# 进入 Nginx 服务的可执行目录
cd /usr/local/nginx/sbin

# 重新载入配置文件
./nginx -s reload  
```


## 1.3 参考文档

（1）[通过 Nginx 搭建自建 Url 转发](https://help.aliyun.com/document_detail/206119.html)

（2）[在 Nginx（或 Tengine）服务器上安装证书](https://help.aliyun.com/document_detail/98728.html)


# 2 结束
