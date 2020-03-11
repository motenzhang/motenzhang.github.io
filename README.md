<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [备忘代码段](#%E5%A4%87%E5%BF%98%E4%BB%A3%E7%A0%81%E6%AE%B5)
- [安装extensions扩展](#%E5%AE%89%E8%A3%85extensions%E6%89%A9%E5%B1%95)
- [常用命令](#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)

<!-- /MarkdownTOC -->
<a id="%E5%A4%87%E5%BF%98%E4%BB%A3%E7%A0%81%E6%AE%B5"></a>
## 备忘代码段

```php
// Creating default object from empty value
$res = new \stdClass();
// array_search返回键名，key为0时返回false 不会是预期结果 用in_array返回true/false
array_search('1', [0=>1,1=>2]);return false;
in_array('1', [0=>1,1=>2]); return true;
// 对象转数组
$data = array_map(function($item){
    return (array) $item;
},DB::table('table_name')->select(*));
// 通过键值互换较array_unique更快速地去重数组
array_flip($array);
// 删除数组中的某值(非key)(https://stackoverflow.com/questions/7225070/php-array-delete-by-value-not-key)
if ( ($key = array_search($del_val, $messages)) !== false ) {
    unset($messages[$key]);
}
// 解析url参数
$url = "http://xxx/?uid=123&code=456";
$refer_parse = parse_url($url);
// 解析参数为数组
parse_str($refer_parse['query'],$queryArr);
$code = $queryArr['code'];
return $code = '456';
```
<a id="%E5%AE%89%E8%A3%85extensions%E6%89%A9%E5%B1%95"></a>
## 安装extensions扩展
```bash
# 查找有没有安装此扩展
php -i | grep fileinfo 
# 查看扩展的版本
php --ri fileinfo
# 下载扩展包
wget -O php-7.2.6.tar.gz http://cn2.php.net/get/php-7.2.6.tar.gz/from/this/mirror
tar -zxvf php-7.2.6.tar.gz
cd php-7.2.6/ext/fileinfo
# phpize执行
/usr/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
# 更改php.ini 打开fileinfo扩展
# 重啟php
# 重启nginx(reload不行)/apache
```
<a id="%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
## 常用命令
```bash
# php.ini修改生效
vim /usr/local/php/etc/php.ini
# 强杀php进程
pkill -9 php-fpm
# 启动
/usr/bin/php-fpm
service php-fpm restart
```
