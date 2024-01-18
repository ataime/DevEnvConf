# 使用Nginx官方镜像作为基础
FROM nginx:alpine

# 删除默认的配置文件
RUN rm /etc/nginx/conf.d/default.conf

# 复制自定义的配置文件到Nginx
COPY default.conf /etc/nginx/conf.d/

# 当容器启动时，Nginx也会随之启动
CMD ["nginx", "-g", "daemon off;"]

