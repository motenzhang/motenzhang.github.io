<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [常用扩展](#%E5%B8%B8%E7%94%A8%E6%89%A9%E5%B1%95)

<!-- /MarkdownTOC -->

> {danger} 线上环境禁用  

此操作会将所有扩展包（包含laravel库本身）升级到最新版本  
`composer install`
`composer update`  
虽仅升级单个扩展，但容易造成与git上冲突  
`composer update vendor/package`  
安装扩展并显示详细信息  
`composer -vvv require vendor/package`   
在线上安装新扩展也容易与git冲突   
`composer require vendor/newpackage`   
<a id="%E5%B8%B8%E7%94%A8%E6%89%A9%E5%B1%95"></a>
## 常用扩展
```bash
# 全局安装composer
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
# 全局加速composer
composer config -g repo.packagist composer https://packagist.phpcomposer.com
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
# 显示所有扩展的详细信息，并列出扩展之间的依赖关联关系
composer show -t
# 常用composer扩展
# 压缩
composer require chumper/zipper
# ES搜索(官方版需要拼接原始json串发请求)
composer require elasticsearch/elasticsearch
# ES搜索格式伪造成数据库查询模式(没用过 待验证)
composer require elasticquent/elasticquent
# JWT用户验证
composer require tymon/jwt-auth
# rbac用户角色权限系统
composer require zizaco/entrust
# passport用户验证(逻辑较jwt复杂 但可以做第三方客户端授权)
composer require laravel/passport
# redis
composer require predis/predis
# excel
composer require maatwebsite/excel
# pdf
composer require barryvdh/laravel-dompdf
# 微信sdk
composer require "overtrue/wechat:~4.1" -vvv
# 模拟http请求(curl)
composer require guzzlehttp/guzzle
# 验证码
composer require mews/captcha
# 手机号验证扩展包
composer require propaganistas/laravel-phone
# 调试扩展(代码注入性较debugbar少)|依据chrome/ff扩展|依据env.debug是否开启
composer require itsgoingd/clockwork
# 语言包
composer require caouecs/laravel-lang
# 生成所有vendor内扩展包的license证书
composer global require comcast/php-legal-licenses
which php-legal-licenses
php-legal-licenses generate
# 过滤用户输入，防止xss攻击
composer require mews/purifier
# 更新单个扩展包
composer update vendor/package
# 卸载composer扩展
composer remove "vendor/packagename"
# 扩展包推荐
https://learnku.com/laravel/t/2530/the-highest-amount-of-downloads-of-the-100-laravel-extensions-recommended
```