<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Nginx](#nginx)

<!-- /MarkdownTOC -->
<a id="nginx"></a>
## Nginx
```bash
# 默认配置文件目录
vim /usr/local/nginx/conf/nginx.conf
# 重启nginx
/usr/local/nginx/sbin/nginx -s reload
service nginx restart
# 其他配置
/usr/local/nginx/sbin/nginx 
  -c(指定配置文件(configuration)目录 不指定默认/conf/nginx.conf)
  -t(测试配置文件是否正常)
  -s(signal >> stop, quit, reopen, reload)
# 获取nginx系统用户/组
# 默认在nginx.conf的第一行
user www www
```
```bash
# 查找有没有www用户
id www
# id: www: no such user
# 添加www用户组
groupadd www
# 添加www用户
useradd -g www -s /sbin/nologin www

```