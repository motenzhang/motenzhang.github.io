<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Windows安装](#windows%E5%AE%89%E8%A3%85)
- [代码提交到git](#%E4%BB%A3%E7%A0%81%E6%8F%90%E4%BA%A4%E5%88%B0git)
- [安装指定版本](#%E5%AE%89%E8%A3%85%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC)

<!-- /MarkdownTOC -->
<a id="windows%E5%AE%89%E8%A3%85"></a>
## Windows安装
```bash
# 需要电脑上配置composer环境变量等
composer global require laravel/installer
# 确认代码目录
laravel new blog
# 生成.env中加密key值
php artisan key:generate
# 配置config/app.php
'timezone' => 'PRC',
'locale' => 'zh-CN',
'faker_locale' => 'zh_CN',
# 配置config/database.php 更改数据库连接
# 配置.env文件 更改程序名称、数据库连接等
# 配置.gitignore文件 加入.env config/database.php public/.htaccess 取消/vendor
# 配置vhosts
...\conf\extra\httpd-vhosts.conf # 报403forbidden >> 重启apache
# 配置host
C:\Windows\System32\drivers\etc\hosts
127.0.0.1      blog.local
# 刷新本地dns
ipconfig /displaydns
ipconfig /flushdns
# 按需更改配置文件中db + app_url参数
# 按需新建数据库
config/app.php
.env
```
<a id="%E4%BB%A3%E7%A0%81%E6%8F%90%E4%BA%A4%E5%88%B0git"></a>
## 代码提交到git
```bash
cd ..\blog\
# 避免出现换行符的warning提示
git config --global core.autocrlf false
# 避免出现文件格式的提示
git config --add core.filemode false
git init
git remote add origin git@10.3.38.251:8080:php_server/blog.git
git add .
git commit -m "Initial commit"
git push -u origin master
```
<a id="%E5%AE%89%E8%A3%85%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC"></a>
## 安装指定版本
```bash
# z-song/laravel-admin目前官方支持laravel5.5
composer create-project --prefer-dist laravel/laravel laradmin "5.5.*"
composer require encore/laravel-admin
php artisan vendor:publish --provider="Encore\Admin\AdminServiceProvider"
php artisan admin:install
# 同上配置vhosts host db appurl后启动
```