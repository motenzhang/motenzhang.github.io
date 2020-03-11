<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [常用命令](#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
- [find常用命令](#find%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
- [Git SSH连接](#git-ssh%E8%BF%9E%E6%8E%A5)
- [PHP-FPM](#php-fpm)
- [LNMP一键安装](#lnmp%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85)
- [YUM版安装PHP扩展BCMATH](#yum%E7%89%88%E5%AE%89%E8%A3%85php%E6%89%A9%E5%B1%95bcmath)

<!-- /MarkdownTOC -->

<a id="%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
## 常用命令
```bash
# 查看系统下挂载盘大小
df -h
# 查看当前目录下子目录文件大小
ls -lht
# 将du的输出按照目录大小排序并输出
du -sh *
du -s * | sort -k 1 -g | awk '{print $2}' | xargs du -sh {}
# 解压
tar zxvf filename.tar.gz
# 压缩(.tar只是打包文件 并没有被压缩)
tar zcvf filename.tar.gz dirname
# 查看进程是否启动
ps -ef | grep elastic
ps aux | grep elastic
# 添加用户（-d分配用户所属目录 -g分配用户组）
useradd -d /home/code/zhangyang -g root zhangyang
# 设置密码
passwd zhangyang
# 获取系统相关帐号
cat /etc/passwd
# 给服务器增加nginx所用的www账号
# 检查是否有此账号
id www
# 增加www组
groupadd www
# 增加www组并使其不能登录
useradd -g www -s /sbin/nologin www
# 获取服务器版本
cat /etc/issue >> CentOS release 6.4 (Final)
# 查找当前PHP所用配置文件的位置
php -i | grep 'php.ini'
# 卸载源码安装的软件
wget imagemagick.org/download/ImageMagick.tar.gz
tar zxvf ImageMagick.tar.gz
cd ImageMagick-6.8.2-10
./configure
make uninstall
# pscp：linux windows简单文件传输
# 1.从win上传到linux
# 下载putty 找到安装目录内的pscp.exe 添加到环境变量
pscp C:\Users\lenovo\Desktop\xianzhi500.png zhangyang@10.3.38.251:/home/code/zhangyang
# zhangyang@10.3.38.251's password:  WCN*TZivSA#yV&eg
xianzhi500.png            | 6 kB |   6.2 kB/s | ETA: 00:00:00 | 100%
# 2.反之从linux下载到windows
pscp zhangyang@10.3.38.251:/home/code/www/djy/config/database.php  C:\Users\lenovo\Desktop\
```

<a id="find%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
## find常用命令
```bash
# 查找当前目录下.conf结尾的文件是否包含特定字符串
# 列出当前目录及其子目录下所有conf文件
find . -name "*.conf"
# 将目前目录及其子目录下所有最近20天内修改过的文件列出
find . -ctime -20
# 查找/var/log目录中更改时间在7日以前的普通文件，并在删除之前询问它们：
find /var/log -type f -mtime +7 -ok rm {} \;
# 查找前目录中文件属主具有读、写权限，并且文件所属组的用户和其他用户具有读权限的文件：
find . -type f -perm 644 -exec ls -l {} \;
# 查找系统中所有文件长度为0的普通文件，并列出它们的完整路径：
find / -type f -size 0 -exec ls -l {} \;
# 查找xxx目录下最近7天内修改过的php文件
find /var/www/html/zhangyang/ -name '*.php' -mtime +7 -ls
# 在当前目录下查找conf文件内包含特殊字符串(字符串前后不用*通配符)的文件
find . -name "*.conf" -exec grep -l "syswh-error_log" {} \;
# 在指定目录下查找conf文件包含特殊字符串的文件列表
find / -path "/etc/fdfs*" -name "*.conf" -exec grep -l "newsysfile" {} \;
# 查找所有目录下大于1M的文件
find / -type f  -size +1000k
# 查找当前目录下yml文件 并排除xxx目录
find . !  -path "/var/www/newsys_backend/newsys*" -name "*.yml"
# 查找所有目录下yml文件 并排除xxx目录
find / !  -path "/var/www/newsys_backend/newsys*" -name "*.yml"
# 查找比xxx文件较新的文件
find . -newer MsgCode.php
# 时间参数详解
atime >> access time
#访问时间（access time），指的是文件最后被读取的时间，可以使用touch命令更改为当前时间
ctime >> change time
#变更时间（change time），指的是文件本身（权限、所属组、位置......）最后被变更的时间，变更动作可以使chmod、chgrp、mv等等
mtime >> modify time
#修改时间(modify time)指的是文件内容最后被修改的时间，修改动作可以使echo重定向、vi等等
amin cmin mmin
# 以分钟计算
7 : 准确时间，7表示刚好7（天|分钟）起始位置
+7: 7(天|分钟)以前的
-7: 7(天|分钟)以内的
```
<a id="git-ssh%E8%BF%9E%E6%8E%A5"></a>
## Git SSH连接
```bash
# server refused our key 解决方法
nano ~/.ssh/authorized_keys >> ~/.ssh/ 700 >> authorized_keys 600
vim /etc/ssh/sshd_config
找到 #StrictModes yes 改成 StrictModes no （去掉注释后改成 no）
找到 #PubkeyAuthentication yes 改成 PubkeyAuthentication yes （去掉注释）
找到 #AuthorizedKeysFile .ssh/authorized_keys 改成 AuthorizedKeysFile .ssh/authorized_keys （去掉注释）
/etc/rc.d/init.d/sshd reload 重新加载
# putty ssh长连接
# 服务器修改配置
vim /etc/ssh/sshd_config
TCPKeepAlive yes
ClientAliveInterval 60
ClientAliveCountMax 3
service sshd status
# putty在connections里修改seconds between keepalives 到30
# 表示每30秒向服务器发送一次空包
# sqlyog在连接页面设置保持活动间隔为30秒也可
```
```bash
# 查看删除后没有被释放的空间
lsof | grep delete
#查看当前目录下的文件数量（不包含子目录中的文件）
ls -l | grep "^-" | wc -l
# 查看当前目录下的文件数量（包含子目录中的文件） 注意：R，代表子目录
ls -lR |grep "^-" | wc -l
# 查看当前目录下的文件夹目录个数（不包含子目录中的目录），同上述理，如果需要查看子目录的，加上R
ls -l |grep "^d" | wc -l
```
<a id="php-fpm"></a>
## PHP-FPM
```bash
# 查看php fpm进程是否启动
ps aux | grep php-fpm
# 强杀进程
sudo kill -QUIT 2673
# 启动php-fpm
whereis php-fpm
sudo /usr/sbin/php-fpm7.2
# 软链
ln -s /usr/local/php/bin/php /usr/bin/php
```
<a id="lnmp%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85"></a>
## LNMP一键安装
```bash
yum install screen #有screen可跳过
screen -S lnmp
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz -cO lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && ./install.sh lnmp
4: Install MySQL 5.7.22
root password4MySQL
8: Install PHP 7.2.6
3: Install TCMalloc
```

<a id="yum%E7%89%88%E5%AE%89%E8%A3%85php%E6%89%A9%E5%B1%95bcmath"></a>
## YUM版安装PHP扩展BCMATH
```
## BCMATH扩展为处理UUID等大数据所用扩展
# 查找bcmath
yum search bcmath
# 查找对应php版本
yum -y install php72w-bcmath
# 终止php进程
pkill -9 php-fpm
# 启动php
/usr/sbin/php-fpm
# 重启nginx
service nginx restart
```