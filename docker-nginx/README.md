# docker 部署 ngixn 做转发
#### default.conf
```
http {
    # ...

    # 配置对 vuean.com 的转发
    server {
        listen 80;
        server_name vuean.com;

        location / {
            proxy_pass http://host.docker.internal:8080;
            # 其他可能的Nginx配置...
        }
    }

    # 配置对 zan.cool 的转发
    server {
        listen 80;
        server_name zan.cool;

        location / {
            proxy_pass http://host.docker.internal:8081;
            # 其他可能的Nginx配置...
        }
    }

    # 配置对 gaozo.com 的转发
    server {
        listen 80;
        server_name gaozo.com;

        location / {
            proxy_pass http://host.docker.internal:8083;
            # 其他可能的Nginx配置...
        }
    }

    # ...
}

```

在这里，proxy_pass 指令将请求转发到您的应用程序。host.docker.internal 是Docker提供的特殊DNS名称，它指向您的宿主机。8080, 8081, 8082, 8083 是您的服务实际运行的端口。

#### Dockerfile
```
# 使用Nginx官方镜像作为基础
FROM nginx:alpine

# 删除默认的配置文件
RUN rm /etc/nginx/conf.d/default.conf

# 复制自定义的配置文件到Nginx
COPY default.conf /etc/nginx/conf.d/

# 当容器启动时，Nginx也会随之启动
CMD ["nginx", "-g", "daemon off;"]
```

#### 运行
```
docker build -t my-nginx-image .
docker run -d -p 80:80 my-nginx-image
```
