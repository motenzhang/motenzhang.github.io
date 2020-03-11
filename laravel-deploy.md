<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [部署Deploy](#%E9%83%A8%E7%BD%B2deploy)
- [环境更新Environment](#%E7%8E%AF%E5%A2%83%E6%9B%B4%E6%96%B0environment)
- [Web页面Jenkins部署上线](#web%E9%A1%B5%E9%9D%A2jenkins%E9%83%A8%E7%BD%B2%E4%B8%8A%E7%BA%BF)

<!-- /MarkdownTOC -->
<a id="%E9%83%A8%E7%BD%B2deploy"></a>
## 部署Deploy
```bash
cd /var/www/laravel
git pull
# 此下文件必须手动上传 暂不存放在git库
# 更改全局配置文件(db app_url etc)
vim .env
vim config/database.php
vim config/elastic-apm.php(此为es-apm相关 非必需)
# 赋予代码目录权限（nginx默认用户|组为www，apache默认用户为deamon）
chown -R www:www /var/www/laravel
chown -R deamon:deamon /var/www/laravel
# 更改目录权限(需确认上一级目录也要有读的权限)
chmod -R 755 /var/www/laravel
# 存储软链 使storage目录可被访问
php artisan storage:link
chmod -R 777 storage/
# cache目录需要写入缓存文件
chmod -R 777 bootstrap/cache/
# Nginx作为web服务器的配置方式
# 修改nginx配置文件
vim /usr/local/nginx/conf/vhost/laravel.conf
# vue反向代理（前端配置文件中作转发）
location /api/ {
    proxy_pass   http://api.people.cn;
}
# Apache作为web服务器的配置方式
# 修改apache配置文件
vim /etc/httpd/conf.d/laravel.conf
# 转发代理（前端配置文件中作转发）
ProxyRequests Off
ProxyPass /interface http://djy.local
```
<a id="%E7%8E%AF%E5%A2%83%E6%9B%B4%E6%96%B0environment"></a>
## 环境更新Environment
```bash
# 清空缓存
php artisan view:cache && php artisan cache:clear && php artisan route:cache && php artisan clear-compiled && php artisan clockwork:clean && php artisan config:cache
# 安装一个包后 就会缓存该包到本地 再次下载会优先从本地获取 如果不需要可以清掉这些本地缓存
composer clearcache
# 重新加载最新的函数、服务、别名等对应关系到vendor/composer/autoload_*文件下
# 多人协同作业时易发生冲突 提交代码前尽量更新环境
composer dumpautoload
php artisan config:cache
# 生成配置文件、路由文件缓存
php artisan optimize 
# 上线 初次上线用
php artisan up
#####命令释义#######
php artisan view:clear 
# 删除storage/framework/views下缓存文件
php artisan view:cache
# 生成系统内所有视图层缓存文件到storage/framework/views目录
php artisan cache:clear
# 删除storage/framework/cache/data下缓存文件
php artisan config:clear
# 删除bootstrap/cache/config.php文件
php artisan config:cache
# 先执行config:clear命令删除bootstrap/cache/config.php文件
# 然后重新生成config目录下所有配置文件到bootstrap/cache/config.php文件
# 此项可以极大提高程序运行效率
php artisan route:clear
# 删除bootstrap/cache/routes.php文件
php artisan route:cache
# 生成routes目录下路由缓存文件到bootstrap/cache/routes.php
# 目前routes/api.php含有闭包函数，待去掉后方可正常使用
php artisan clear-compiled
# 删除bootstrap/cache/packages.php bootstrap/cache/services.php
php artisan clockwork:clean
# 删除storage/clockwork内debug文件
# 目前通过config/clockwork.php中参数storage_expiration设置10分钟有效期
```
<a id="web%E9%A1%B5%E9%9D%A2jenkins%E9%83%A8%E7%BD%B2%E4%B8%8A%E7%BA%BF"></a>
## Web页面Jenkins部署上线

[jenkins](jenkins)


