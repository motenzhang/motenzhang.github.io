<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [手机号验证](#%E6%89%8B%E6%9C%BA%E5%8F%B7%E9%AA%8C%E8%AF%81)
- [图片验证码\(未完成\)](#%E5%9B%BE%E7%89%87%E9%AA%8C%E8%AF%81%E7%A0%81%E6%9C%AA%E5%AE%8C%E6%88%90)
- [身份证号验证\(未完成\)](#%E8%BA%AB%E4%BB%BD%E8%AF%81%E5%8F%B7%E9%AA%8C%E8%AF%81%E6%9C%AA%E5%AE%8C%E6%88%90)
- [debug web工具clockwork\(未完成\)](#debug-web%E5%B7%A5%E5%85%B7clockwork%E6%9C%AA%E5%AE%8C%E6%88%90)
- [跨域访问设置\(未完成\)](#%E8%B7%A8%E5%9F%9F%E8%AE%BF%E9%97%AE%E8%AE%BE%E7%BD%AE%E6%9C%AA%E5%AE%8C%E6%88%90)
- [rbac角色权限entrust\(未完成\)](#rbac%E8%A7%92%E8%89%B2%E6%9D%83%E9%99%90entrust%E6%9C%AA%E5%AE%8C%E6%88%90)
- [ip限制访问-黑白名单\(未完成\)](#ip%E9%99%90%E5%88%B6%E8%AE%BF%E9%97%AE-%E9%BB%91%E7%99%BD%E5%90%8D%E5%8D%95%E6%9C%AA%E5%AE%8C%E6%88%90)
- [用户输入过滤-防xss攻击\(未完成\)](#%E7%94%A8%E6%88%B7%E8%BE%93%E5%85%A5%E8%BF%87%E6%BB%A4-%E9%98%B2xss%E6%94%BB%E5%87%BB%E6%9C%AA%E5%AE%8C%E6%88%90)
- [后台管理组件-voyager\(未完成\)](#%E5%90%8E%E5%8F%B0%E7%AE%A1%E7%90%86%E7%BB%84%E4%BB%B6-voyager%E6%9C%AA%E5%AE%8C%E6%88%90)

<!-- /MarkdownTOC -->
<a id="%E6%89%8B%E6%9C%BA%E5%8F%B7%E9%AA%8C%E8%AF%81"></a>
## 手机号验证
```php
// 刷新数据库结构并执行数据填充
php artisan migrate:refresh --seed
# 验证手机号符合中国(自定义)的规则
# 且不与表users中phone字段重复
# 且此扩展(propaganistas/laravel-phone)不允许左侧key值为mobile
'phone'     => 'required|phone:CN,mobile|unique:users,phone',
# 设置数据库中某个字段自增/自减 +-N
# 需要设置article_count为数字类型 非null
# SELECT NULL+1 >> NULL
increment('article_count',1);
```
<a id="%E5%9B%BE%E7%89%87%E9%AA%8C%E8%AF%81%E7%A0%81%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 图片验证码(未完成)

[api验证](https://github.com/mewebstudio/captcha/issues/115#issuecomment-405964829)

<a id="%E8%BA%AB%E4%BB%BD%E8%AF%81%E5%8F%B7%E9%AA%8C%E8%AF%81%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 身份证号验证(未完成)

<a id="debug-web%E5%B7%A5%E5%85%B7clockwork%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## debug web工具clockwork(未完成)

<a id="%E8%B7%A8%E5%9F%9F%E8%AE%BF%E9%97%AE%E8%AE%BE%E7%BD%AE%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 跨域访问设置(未完成)

<a id="rbac%E8%A7%92%E8%89%B2%E6%9D%83%E9%99%90entrust%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## rbac角色权限entrust(未完成)

<a id="ip%E9%99%90%E5%88%B6%E8%AE%BF%E9%97%AE-%E9%BB%91%E7%99%BD%E5%90%8D%E5%8D%95%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## ip限制访问-黑白名单(未完成)

<a id="%E7%94%A8%E6%88%B7%E8%BE%93%E5%85%A5%E8%BF%87%E6%BB%A4-%E9%98%B2xss%E6%94%BB%E5%87%BB%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 用户输入过滤-防xss攻击(未完成)

<a id="%E5%90%8E%E5%8F%B0%E7%AE%A1%E7%90%86%E7%BB%84%E4%BB%B6-voyager%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 后台管理组件-voyager(未完成)


