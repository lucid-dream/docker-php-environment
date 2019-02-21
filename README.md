##### DNMP（Docker + Nginx + Mongo + PHP7.1）

###### 目录结构

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
