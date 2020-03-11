<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Laravel版本差异](#laravel%E7%89%88%E6%9C%AC%E5%B7%AE%E5%BC%82)
- [Laravel扩展版本差异](#laravel%E6%89%A9%E5%B1%95%E7%89%88%E6%9C%AC%E5%B7%AE%E5%BC%82)
- [已知安全漏洞](#%E5%B7%B2%E7%9F%A5%E5%AE%89%E5%85%A8%E6%BC%8F%E6%B4%9E)
- [安全防御预案](#%E5%AE%89%E5%85%A8%E9%98%B2%E5%BE%A1%E9%A2%84%E6%A1%88)

<!-- /MarkdownTOC -->

<a id="laravel%E7%89%88%E6%9C%AC%E5%B7%AE%E5%BC%82"></a>
## Laravel版本差异

>> `v5.8.14 VS v5.7.*`
- `标红的为已用功能(不限于当前党建云项目)`
- `引入新的 Eloquent 关联关系（has-one-through）`
- 优化邮箱验证
- 基于约定的授权策略类自动注册
- DynamoDB 缓存及 Session 驱动
- 优化任务调度器的时区配置
- `支持分配多个认证 guard 到广播频道(['guards' => ['web', 'admin']])`
- `Token Guard 令牌哈希算法(支持SHA-256)`
- `PSR-16 缓存驱动规范(缓存时间精确到秒)`
- 优化 artisan serve 命令
- 支持 PHPUnit 8.0
- `支持 Carbon 2.0`
- 支持 Pheanstalk 4.0（队列库） 
- 以及多个 bug 修复和可用性的提升

>> `v5.7.* VS v5.6.*`
- *官方后台RBAC管理控制台(Laravel Nova)（收费）*
- 可选的邮件认证到认证脚手架
- `在授权和策略中对未登录用户的支持`
- 控制台测试的改进
- Symfony dump-server 的集成
- 可定位的通知
- 还有各类其他 bug 修复和可用性改进

>> `v5.6.* VS v5.5.*`
- `添加了一个改良的日志系统(根据日志级别进行分级写入/推送)`
- `单机任务调度系统(分布式服务器时可指定某台服务器执行任务)`
- 对模型序列化进行改进
- `动态的速率限制(最大频率可以作为参数传递到路由)`
- `广播频道类添加`
- `可生成 API 资源控制器`
- `Eloquent 日期格式改进`
- Blade 组件别名
- `Argon2 密码哈希支持(需要php7.2+ 服务器7.2.6)`
- 加入 Collision 包
- 前端脚手架已经升级为 Bootstrap 4
- `所有Laravel使用的Symfony组件已经升级到Symfony~4.0系列`
- *此次发布Laravel5.6的同时也发布了Spark6.0（收费）*

>> `v5.5.* VS v5.4.*`
- `vendor组件包自动发现/注册(5.5重要功能 减少安装组件流程)`
- API 资源／转换
- `控制台命令自动注册(需要用但没有用到)`
   - `Kernel >> $this->load(__DIR__.'/Commands');`
- `队列任务链`
- `队列任务速率限制`
- 基于时间任务的尝试
- 可渲染的邮件
- `自定义异常报告(优化返回值 相对繁琐)`
- `异常处理规范化`
- 数据库测试改进
- 更简单自定义验证规则
- 前端预配置
- `Route::view 和 Route::redirect 方法`
- Memcached 和 Redis 缓存驱动程序的「锁定」
- `按需通知功能`
- Dusk 支持 Chrome 的 headless 模式 
- 方便的 Blade 快捷键
- 改进可信代理支持等。
- `Laravel Horizon(管理你的 Redis 队列的后台)`


<a id="laravel%E6%89%A9%E5%B1%95%E7%89%88%E6%9C%AC%E5%B7%AE%E5%BC%82"></a>
## Laravel扩展版本差异

|vendor package  | 5.5.* (更新时间)  | 当前版本(更新时间)|最新稳定5.8.* (更新时间)  |
| :------------- | :--------------- | :--------------- | :--------------------- |
|laravel/laravel | 5.5(2019-04-23)  | 5.8.14(2019-05-07) | 5.8.21(2019-06-04)   |
|laravel/passport| 4.0(2018-08-11)  | 7.2(2019-03-13)   | 7.3(2019-05-29)       |
|tymon/jwt-auth  | 0.5(2017-06-07)  | 1.0(2019-03-14)   | 1.0(2019-03-14)       |
|caouecs/laravel-lang| 3.0(2019-03-17)  | 4.0(2019-06-05)   | 4.0(2019-06-05)   |
|propaganistas/laravel-phone| 4.2(2019-06-05)| 4.2(2019-06-05) | 4.2(2019-06-05) |
|elasticsearch/elasticsearch| 6.5(2019-04-29)| 6.7(2019-05-20)  | 6.7(2019-05-20)  |


<a id="%E5%B7%B2%E7%9F%A5%E5%AE%89%E5%85%A8%E6%BC%8F%E6%B4%9E"></a>
## 已知安全漏洞

| 版本  |  CVE ID                                |   发布日期  | 更新日期   |
| :---- | :--------------------------------------------------------------- | :----------| :----------|
| 5.8.3  |[Unique SQL注入](https://github.com/laravel/framework/pull/27940)|  2019-03-20 | `2019-03-24` |
| 5.5.40 |[CVE-2018-15133](https://www.cvedetails.com/cve/CVE-2018-15133/) |2018-08-09 | 2018-10-11 |
| 5.5.21 |[CVE-2017-16894](https://www.cvedetails.com/cve/CVE-2017-16894/) |2017-11-19 | 2018-03-08 |
| 5.5.9  |[CVE-2017-14775](https://www.cvedetails.com/cve/CVE-2017-14775/) |2017-09-27 | 2017-10-10 |
| 5.4.0  |[CVE-2017-9303](https://www.cvedetails.com/cve/CVE-2017-9303/)   |2017-05-29 | 2017-06-08 |

<a id="%E5%AE%89%E5%85%A8%E9%98%B2%E5%BE%A1%E9%A2%84%E6%A1%88"></a>
## 安全防御预案
1. 过滤 & 验证所有用户的输入
   - 过滤：[mews/purifier](https://packagist.org/packages/mews/purifier)
   - 验证：[validation](https://learnku.com/docs/laravel/5.8/validation/3899)
2. 避免使用原生数据库查询，使用[参数绑定](https://learnku.com/docs/laravel/5.8/queries/3926)
3. 确保服务器代码[目录权限](https://stackoverflow.com/questions/30639174/how-to-set-up-file-permissions-for-laravel-5-and-others)够用即可，尤其是对于.env文件的防护
4. 使用内置加密算法，5.8中已升级到BCRYT SHA-256，不要使用自己的加密算法
5. 定期对已安装组件进行漏洞检查，[security-checker检查composer.lock](https://github.com/sensiolabs/security-checker)
6. session里不存储敏感数据，尽量[即用即消](https://github.com/sobstel/sesshin/wiki/PHP-Session-Security---Best-Practices)
7. 日志记录尽量详尽，生产环境错误/异常提示记录到日志，且关闭web[错误提示/异常记录](https://learnku.com/docs/laravel/5.8/errors/3900)
8. 使用https服务器，通过[tls/密钥对](https://www.digitalocean.com/community/tutorials/7-security-measures-to-protect-your-servers#public-key-infrastructure-and-ssltls-encryption)连接生产服务器
9. 付费商用安全厂商[sqreen安全策略](https://assets.sqreen.com/whitepapers/laravel-security-checklist.pdf?__s=nnazsvsq4tnqxwnbwwce)
10. LTS版本仅为[长期支持](https://github.com/laravel/ideas/issues/983#issuecomment-367204770)版本，并非最安全版本
11. 生产服务器使用[密钥对登录](https://learnku.com/articles/25924),[避免使用根用户](https://learnku.com/articles/25753)进行线上操作
12. Nginx配置添加图片防盗链,对请求图片URL的referer进行主站域名过滤筛选
   - location ~*\.(gif|jpg|jpeg|png|bmp|swf)$ {  valid_referers none blocked *.yourname.com;  if ($invalid_referer) {  rewrite ^/ http://youname.com/error.html;  #return 403; } }
