<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Centos安装ImageMagick](#centos%E5%AE%89%E8%A3%85imagemagick)
	- [1.yum安装](#1yum%E5%AE%89%E8%A3%85)
	- [2.源码安装](#2%E6%BA%90%E7%A0%81%E5%AE%89%E8%A3%85)
- [Centos安装php扩展imagick.so](#centos%E5%AE%89%E8%A3%85php%E6%89%A9%E5%B1%95imagickso)
	- [1.pecl安装](#1pecl%E5%AE%89%E8%A3%85)
	- [2. 源码安装](#2-%E6%BA%90%E7%A0%81%E5%AE%89%E8%A3%85)
- [Windows安装ImageMagick及其PHP扩展](#windows%E5%AE%89%E8%A3%85imagemagick%E5%8F%8A%E5%85%B6php%E6%89%A9%E5%B1%95)

<!-- /MarkdownTOC -->
<a id="centos%E5%AE%89%E8%A3%85imagemagick"></a>
## Centos安装ImageMagick
及其PHP扩展imagick.so
<a id="1yum%E5%AE%89%E8%A3%85"></a>
### 1.yum安装
```bash
# 第一种是通过yum库内的集成软件包
# 第二种是通过源码包
# 1.yum安装ImageMagick软件包
yum install php-pear php-devel gcc 
yum install ImageMagick ImageMagick-devel ImageMagick-perl
convert --version
# 输出Version: ImageMagick 6.7.8-9 ...
# 2.源码安装
# 安装工具
yum groupinstall 'Development Tools'
yum -y install bzip2-devel freetype-devel libjpeg-devel libpng-devel libtiff-devel giflib-devel zlib-devel ghostscript-devel djvulibre-devel libwmf-devel jasper-devel libtool-ltdl-devel libX11-devel libXext-devel libXt-devel lcms-devel libxml2-devel librsvg2-devel OpenEXR-devel php-devel
```
<a id="2%E6%BA%90%E7%A0%81%E5%AE%89%E8%A3%85"></a>
### 2.源码安装
```bash
# 下载源码包（官方地址被墙了 需要到gihub上下载）
# 不指定版本下载的为当前最新的7+版本 但是现在的php-imagick扩展安装到php7以上时会报warning
# 推荐使用Yum安装6+版本
wget https://www.imagemagick.org/download/ImageMagick.tar.gz
tar xvzf ImageMagick.tar.gz
cd ImageMagick
./configure
make && make install
magick -version
# 输出Version: ImageMagick 7.0.8-28 Q16 x86_64
##### 错误处理
# error while loading shared libraries: libMagickCore-7.Q16HDRI.so.6
ldconfig /usr/local/lib
# ldconfig命令的用途主要是在默认搜寻目录/lib和/usr/lib以及动态库配置文件/etc/ld.so.conf内所列的目录下
# 搜索出可共享的动态链接库（格式如lib*.so*）,进而创建出动态装入程序(ld.so)所需的连接和缓存文件
# 服务器启动后 库文件（so > shared object）会自动加载到/lib或/usr/lib下
# 而新装软件则不会自动加载库文件 需要手动加载（ld > LoaD 或 Load eDitor）配置文件
```

<a id="centos%E5%AE%89%E8%A3%85php%E6%89%A9%E5%B1%95imagickso"></a>
## Centos安装php扩展imagick.so
<a id="1pecl%E5%AE%89%E8%A3%85"></a>
### 1.pecl安装
```bash
pecl install imagick
```
<a id="2-%E6%BA%90%E7%A0%81%E5%AE%89%E8%A3%85"></a>
### 2. 源码安装
```bash
wget https://pecl.php.net/get/imagick-3.4.4.tgz
tar -xzvf imagick-3.4.4.tgz
cd imagick-3.4.4
./configure --with-php-config=/usr/local/php7.2.19/bin/php-config --with-imagick=/usr/local/imagemagick
make && make install
echo extension=imagick.so >> /etc/php.ini
service httpd restart
php -m | grep imagick
```
<a id="windows%E5%AE%89%E8%A3%85imagemagick%E5%8F%8A%E5%85%B6php%E6%89%A9%E5%B1%95"></a>
## Windows安装ImageMagick及其PHP扩展
[原文链接](https://mlocati.github.io/articles/php-windows-imagick.html)
```bash
# 根据php版本 架构等确认需要安装软件包版本及其对应的扩展
# 如版本不对应可能报错 或有warning
# 和Linux版本不同的是 win下可正常使用7+版本 且不会出现需要更改convert.exe的问题
php -i | find "PHP Version"
php -i | find "Thread Safety"
php -i | find "Architecture"
# 软件包下载解压后点击安装到没有中文的目录下
# 通过magick --version进行验证是否安装成功
# 扩展包解压后先将其压缩包内`php_imagick.dll`文件放置于php/ext目录下(laragon\bin\php\php-7.2.11-Win32-VC15-x64\ext)
# 然后将压缩包内所有IM_*.dll及CORE_RL*.DLL放到php的根目录下(亦即php.exe同目录)
# 编辑php.ini文件 添加`extension=php_imagick.dll`
# 重启apache/nginx
```