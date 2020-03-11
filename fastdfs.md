<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [`简述版`](#%E7%AE%80%E8%BF%B0%E7%89%88)
- [安装依赖包](#%E5%AE%89%E8%A3%85%E4%BE%9D%E8%B5%96%E5%8C%85)
- [安装libfastcommon函数库](#%E5%AE%89%E8%A3%85libfastcommon%E5%87%BD%E6%95%B0%E5%BA%93)
- [安装fastdfs源文件](#%E5%AE%89%E8%A3%85fastdfs%E6%BA%90%E6%96%87%E4%BB%B6)
- [修改配置文件](#%E4%BF%AE%E6%94%B9%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
- [打开端口](#%E6%89%93%E5%BC%80%E7%AB%AF%E5%8F%A3)
- [命令行启动tracker+storage测试](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%90%AF%E5%8A%A8trackerstorage%E6%B5%8B%E8%AF%95)
- [追加nginx模块](#%E8%BF%BD%E5%8A%A0nginx%E6%A8%A1%E5%9D%97)
- [安装php-fastdfs扩展](#%E5%AE%89%E8%A3%85php-fastdfs%E6%89%A9%E5%B1%95)

<!-- /MarkdownTOC -->

<a id="%E7%AE%80%E8%BF%B0%E7%89%88"></a>
### `简述版`
> * 安装libfastcommon函数库
> * 安装fastdfs源文件(打开端口22122 23000)
>> * 如果只是linux命令行操作，则可到此为止
>> * 如果需要fdfs作为php内置函数，则需要安装php扩展
> * 安装php_client，复制php.ini
> * php -m查看是否安装成功
> * 框架无需引入fastdfs公共函数库(已作为PHP扩展-类内置函数)
<a id="%E5%AE%89%E8%A3%85%E4%BE%9D%E8%B5%96%E5%8C%85"></a>
### 安装依赖包
```bash
# 确认是否安装C C++编译包，无则需要安装
rpm -qa | grep gcc*
yum install -y gcc gcc-c++
# 确认安装libevent
yum -y install libevent
# 进入安装目录
cd /usr/local
```
<a id="%E5%AE%89%E8%A3%85libfastcommon%E5%87%BD%E6%95%B0%E5%BA%93"></a>
### 安装libfastcommon函数库
```bash
git clone https://github.com/happyfish100/libfastcommon.git
cd libfastcommon
./make.sh && ./make.sh install
# 从64位库拷贝编译文件到32位
ll /usr/lib | grep libfast*
cp /usr/lib64/libfastcommon.so /usr/lib
```
<a id="%E5%AE%89%E8%A3%85fastdfs%E6%BA%90%E6%96%87%E4%BB%B6"></a>
### 安装fastdfs源文件
```bash
cd /usr/local
git clone https://github.com/happyfish100/fastdfs.git
```
<a id="%E4%BF%AE%E6%94%B9%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6"></a>
### 修改配置文件
```bash
cd fastdfs
./make.sh && ./make.sh install
# 复制配置文件到etc/fdfs/目录下
cp /usr/local/fastdfs/conf/* /etc/fdfs/
# 修改以下配置
vim /etc/fdfs/client.conf
# base_path=/home/code/fastdfs
# tracker_server=10.3.38.251:22122
# http.tracker_server_port=80
vim /etc/fdfs/http.conf
# 无修改配置
# 如需添加防盗链 需要设置
# http.anti_steal.check_token=true
# http.anti_steal.secret_key=FastDFS1234567890
# 且需要设置php.ini中同样的key
vim /usr/local/php7.2.19/etc/php.ini
# fastdfs_client.http.anti_steal_secret_key = FastDFS1234567890
vim /etc/fdfs/storage.conf
# base_path=/home/code/fastdfs
# store_path0=/home/code/fastdfs
# tracker_server=10.3.38.251:22122
# http.domain_name=http://img.people.cn
# http.server_port=80
vim /etc/fdfs/storage_ids.conf
# 无修改配置
vim /etc/fdfs/tracker.conf
# base_path=/home/code/fastdfs
## 使用apache的服务器到此结束配置可以进行启动fdfs
# 安装fastdfs-nginx-module后追加此配置
cp /usr/local/src/fastdfs-nginx-module/src/mod_fastdfs.conf /etc/fdfs/
vim /etc/fdfs/mod_fastdfs.conf
# base_path=/home/code/fastdfs
# store_path0=/home/code/fastdfs
# tracker_server=10.3.38.251:22122
# the format of filename is invalid
# url_have_group_name=true
```
<a id="%E6%89%93%E5%BC%80%E7%AB%AF%E5%8F%A3"></a>
### 打开端口
```bash
# 追加 >>> 如果仅限于单机配置 则不需要配置端口
# 仅需将tracker ip设定为单机地址(非127.0.0.1 需192.168.11.125)
# 第一种：
# 通过云主机的安全组添加22122和23000两个端口
# 添加连接源地址到安全组的入口白名单
# 第二种：
# 通过设置服务器防火墙添加
vim /etc/sysconfig/iptables
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22122 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 23000 -j ACCEPT
service iptables restart
```
<a id="%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%90%AF%E5%8A%A8trackerstorage%E6%B5%8B%E8%AF%95"></a>
### 命令行启动tracker+storage测试
```bash
/sbin/service fdfs_trackerd start
/sbin/service fdfs_storaged start
# 测试fdfs本尊(非php客户端)是否安装成功
/usr/bin/fdfs_test /etc/fdfs/client.conf upload /etc/fdfs/anti-steal.jpg
# 输出
group_name=group1, ip_addr=10.38.11.216, port=23000
storage_upload_by_filename
group_name=group1, remote_filename=M00/00/01/CiYL2FwtqsyABb2PAABdrZgsqUU418.jpg
source ip address: 10.38.11.216
file timestamp=2019-01-03 14:25:16
file size=23981
file crc32=2553063749
example file url: http://10.38.11.216/group1/M00/00/01/CiYL2FwtqsyABb2PAABdrZgsqUU418.jpg
```
<a id="%E8%BF%BD%E5%8A%A0nginx%E6%A8%A1%E5%9D%97"></a>
### 追加nginx模块
```bash
# FastDFS通过Tracker服务器,将文件放在Storage服务器,但是同组存储服务器之间需要进入文件复制,有同步延迟的问题；
# 假设Tracker服务器将文件上传到了ip01,上传成功后文件ID已经返回给客户端；
# 此时FastDFS存储集群机制会将这个文件同步到同组存储ip02,
# 在文件还没有复制完成的情况下,客户端如果用这个文件ID在ip02上取文件,就会出现文件无法访问的错误；
# 而fastdfs-nginx-module可以重定向文件连接到源服务器取文件,避免客户端由于复制延迟导致的文件无法访问错误；
# 需要先下载nginx源码然后追加fastdfs-nginx模块到nginx安装目录
wget http://nginx.org/download/nginx-1.16.0.tar.gz
# 按需安装nginx依赖
yum install gcc gcc-c++ make automake autoconf libtool pcre* zlib openssl openssl-devel
tar -xzvf nginx-1.16.0.tar.gz
cd nginx-1.16.0
./configure --prefix=/usr/local/nginx --add-module=/usr/local/fastdfs-nginx-module/src
make && make install
# 编辑nginx.conf文件 后reload nginx
server {
  listen       80;
  server_name img.people.cn;
  location ~/group[0-9]/M00 {
      root /home/code/fastdfs/data;
      ngx_fastdfs_module;
  }
  error_page   500 502 503 504  /50x.html;
  location = /50x.html {
       root   html;
  }
}
```
<a id="%E5%AE%89%E8%A3%85php-fastdfs%E6%89%A9%E5%B1%95"></a>
### 安装php-fastdfs扩展
```bash
cd /usr/local/fastdfs/php_client
/usr/local/php7/bin/phpize
./configure --with-php-config=/usr/local/php7/bin/php-config
make && make install
cat fastdfs_client.ini >> /usr/local/php7/etc/php.ini
# 查看是否安装成功
php -m | grep fastdfs_client
# 测试
php /usr/local/fastdfs/php_client/fastdfs_test1.php
```