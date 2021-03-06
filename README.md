# 宝塔Linux面板 Docker 版

`Version：5.6.1 免费版`

本Docker基于[宝塔Linux面板](https://www.bt.cn),集成环境包含 Nginx PHP5.6 PHP7 FTP等基本服务，未包含Mysql，建议用外链服务的方式支持。

## 快速开始
```
docker run \
--name bt \
-p 8888:8888 \
-p 80:80 \
-p 443:443 \
-p 21:21 \
-p 20:20 \
-d ywfwj2008/bt-php-nginx:latest
```
在浏览器中打开：`http://你得ip地址:8888`  
默认用户：admin  
默认密码：123456

## run web server
运行docker时，可以通过 `BT_PASSWORD` 自定义登录密码
```
docker run \
--name bt \
--link mysql:localmysql \
-v /home/backup:/www/backup \
-v /home/wwwlogs:/www/wwwlogs \
-v /home/wwwroot:/www/wwwroot \
-v /home/config/vhost:/www/server/panel/vhost \
-v /home/letsencrypt:/etc/letsencrypt \
-e BT_PASSWORD=my-secret-pw \
-p 8888:8888 \
-p 80:80 \
-p 443:443 \
-p 21:21 \
-p 20:20 \
-d ywfwj2008/bt-php-nginx:latest
```

## run mysql
如果需要外连mysql，先运行mysql镜像。宝塔镜像中使用link参数连接。
```
docker run \
--name mysql \
-v /home/config/mysql:/etc/mysql/conf.d \
-v /home/mysql:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=my-secret-pw \
-d mysql:latest
```
