# docker php+mysql+nginx+redis 运行环境

## 如何使用

### 安装 `docker-compose`

``` bash
pip install -U docker-compose
```

### 修改映射源码目录 `docker-compose.yml` 文件中的 `volumes` 映射关系

这里我们案例写的是 `./code/:/opt/htdocs/code/`,其中 ./code/ 可以替换成本地项目路径

### 配置自定义 `nginx` 配置

在 `nginx/sites-enabled/` 下面新增对应项目的 `nginx` 配置

例如新增一个 `web.conf` ：

``` conf
server {
  listen   80;
  server_name  local.evaengine.com;
  root  /opt/htdocs/web/public;
  index index.php;
  try_files $uri $uri/ @rewrite;
  location @rewrite {
      rewrite ^/(.*)$ /index.php?_url=/$1;
  }

  location ~ \.php {
      include fastcgi_params;
      fastcgi_pass   php:9000;
      fastcgi_index  index.php;
      fastcgi_param  SCRIPT_FILENAME  /opt/htdocs/web/public/$fastcgi_script_name;
      fastcgi_param  APPLICATION_NAME evaengine;
  }
}


server {
  listen   80;
  server_name  static.evaengine.com;
  root  /opt/htdocs/web/public/static/;
  add_header Access-Control-Allow-Origin *;
  index index.html index.htm;
  access_log off;
}
```

### 编译运行容器

``` bash
docker-compose up --build
```

具体其它用法，请查看对应的 API

``` bash
docker-compose -h
```
