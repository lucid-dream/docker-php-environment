##### DNMP（Docker + Nginx + Mongo + PHP7.1）

###### 目录结构
```
.
└── docker-php-environment
    ├── build                           镜像构建目录
    │   ├── mongo
    │   │   └── Dockerfile
    │   ├── nginx
    │   │   └── Dockerfile
    │   └── php71
    │       ├── Dockerfile
    │       ├── GeoLiteCity.dat
    │       ├── cphalcon.tgz
    │       ├── geoip-1.1.1.tgz
    │       ├── memcached-3.0.4.tgz
    │       ├── mongodb-1.4.2.tgz
    │       ├── redis-4.0.0.tgz
    │       ├── sources.list
    │       ├── swoole-2.2.0.tgz
    │       └── xdebug-2.6.0.tgz
    ├── components                     组件库
    │   ├── nginx
    │   │   └── conf.d                 nginx项目配置文件目录
    │   │       └── localhost.conf
    │   └── php71                       
    │       └── conf.d
    │           ├── fpm
    │           │   └── www.conf
    │           └── php.ini
    ├── docker-compose.yml             docker compose 配置文件
    ├── .env                           环境配置文件
    ├── xdebug_alias_ip.sh             mac设置ip别名
    └── www                            项目目录
        └── html
            └── index.php
```

###### 开始安装

```
git clone https://github.com/lucid-dream/docker-php-environment.git
cd docker-php-environment
# 配置项目目录、端口
vim .env
# 构建镜像并启动容器
sudo docker-compose up --build -d
```

###### 启动成功访问 http://localhost 

###### 参考资料
```
https://github.com/yeszao/dnmp
https://github.com/exc-soft/docker-lnmp
```
