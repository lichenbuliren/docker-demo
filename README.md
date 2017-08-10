# docker php+mysql+nginx+redis 运行环境

## 如何使用

### 安装 `docker-compose`

``` bash
pip install -U docker-compose
```

### 修改映射源码目录 `docker-compose.yml` 文件中的 `volumes` 映射关系

### 配置自定义 `nginx` 配置

在 `nginx/sites-enabled/` 下面新增对应项目的 `nginx` 配置
