FROM nginx

ADD nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled/* /etc/nginx/conf.d/

RUN mkdir /opt/htdocs && mkdir /opt/log && mkdir /opt/log/nginx
# 设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
RUN chown -R www-data.www-data /opt/htdocs /opt/log

EXPOSE 80
VOLUME ["/opt"]

