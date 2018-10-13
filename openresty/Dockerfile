############################################
# version : 10.0.0.149:5000/ubuntu:dev-openresty1.11
# 设置继承自我们创建的 tools 镜像
############################################
FROM 10.0.0.149:5000/ubuntu:dev-tools

# 下面是一些创建者的基本信息
MAINTAINER LIUJQ


# 设置环境变量，所有操作都是非交互式的
ENV DEBIAN_FRONTEND noninteractive

# 添加 supervisord 的配置文件，并复制配置文件到对应目录下面。
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
#COPY luajit /usr/local/luajit
ADD  /usr/local/luajit /usr/local/luajit
ADD  /soft/local/opensoft /software/openresty
RUN  ln -sf luajit-2.1.0-beta2 /usr/local/luajit/bin/luajit
RUN  ln -s /usr/local/luajit/lib/libluajit-5.1.so.2 /lib64/libluajit-5.1.so.2

# 执行supervisord来同时执行多个命令，
#使用 supervisord 的可执行路径启动服务。
# 设置nginx是非daemon启动
RUN echo 'daemon off;' >> /software/openresty/nginx/nginx.conf
RUN echo 'master_process off;' >> /software/openresty/nginx/nginx.conf
RUN echo 'error_log  logs/error.log;' >> /software/openresty/nginx/nginx.conf

# 设置 NGINX 的环境变量
ENV NGINX_HOME /software/openresty/nginx
#ENV LUAJIT_LIB=/usr/local/luajit/lib
#ENV LUAJIT_INC=/usr/local/luajit/include/luajit-2.1

# 容器需要开放Nginx 8088端口
EXPOSE 8088
#使用 supervisord 的可执行路径启动服务。
CMD ["/usr/bin/supervisord"]
