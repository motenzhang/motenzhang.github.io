<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Apache](#apache)

<!-- /MarkdownTOC -->
<a id="apache"></a>
## Apache
```bash
# 启动/停止/查看apache
systemctl status httpd.service
# 启动/停止/查看apache 方法2
/usr/local/apache/bin/apachectl restart
/etc/init.d/httpd start
service httpd start
# apache启动不了,优先查看错误日志
# 查找apache安装路径
systemctl status httpd.service
apachectl -v
rpm -q  httpd
# 查看端口号占用情况
netstat -anp | grep 80
netstat -tulnp | grep ':80'
# 查看防火墙是否开启xxx端口
# 先win上检查端口是否开放(需要在设置里启用telnet客户端功能)
telenet 10.3.38.251 6379
vim /etc/sysconfig/iptables
-A INPUT -p tcp -m tcp --dport 8080 -j ACCEPT
service iptables restart
# 查看日志文件
tail -f /usr/local/apache2.4.12/logs/error_log
# 203
ServerRoot "/etc/httpd"
vim /etc/httpd/conf/httpd.conf
tail -f /etc/httpd/logs/error_log
# 代码初次上传时需更改代码文件所在文件的所属用户、组为apache
# apache默认守护进程用户、组为deamon
# 如需确认守护进程用户 需查看httpd.conf文件中User\Group
chown -R daemon:daemon /var/www/newsys_backend/newsys/
```
