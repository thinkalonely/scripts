# 一个快速获取/更新 Let's encrypt 证书的 shell script
## 配置文件
只需要修改 DOMAIN_KEY DOMAIN_DIR DOMAINS 为你自己的信息
```
ACCOUNT_KEY="letsencrypt-account.key"
DOMAIN_KEY="example.com.key"
DOMAIN_DIR="/var/www/example.com"
DOMAINS="DNS:example.com,DNS:whatever.example.com"
#ECC=TRUE
#LIGHTTPD=TRUE
```
## 运行
```./letsencrypt.sh letsencrypt.conf```
## 注意

需要已经绑定域名到 /var/www/example.com 目录，即通过 http://example.com http://whatever.example.com 可以访问到 /var/www/example.com 目录，用于域名的验证
## 在 nginx 里添加 ssl 相关的配置
```
ssl_certificate     /path/to/cert/example.chained.crt;
ssl_certificate_key /path/to/cert/example.com.key;
```
## cron 定时任务

``` 0 0 1 * * /etc/nginx/certs/letsencrypt.sh /etc/nginx/certs/letsencrypt.conf && nginx -s reload >> /var/log/lets-encrypt.log 2>&1```