<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [请求REQUEST\(未完成\)](#%E8%AF%B7%E6%B1%82request%E6%9C%AA%E5%AE%8C%E6%88%90)
- [返回RESPONSE\(未完成\)](#%E8%BF%94%E5%9B%9Eresponse%E6%9C%AA%E5%AE%8C%E6%88%90)
- [异常EXCEPTION\(未完成\)](#%E5%BC%82%E5%B8%B8exception%E6%9C%AA%E5%AE%8C%E6%88%90)

<!-- /MarkdownTOC -->

<a id="%E8%AF%B7%E6%B1%82request%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 请求REQUEST(未完成)
1. 请求方式约定
   - `GET POST PUT DELETE PATCH`
   - [RESTful API请求规范](front-back-restful)
2. 请求参数约定
   - ID是请求参数中用到最多、最为频繁的字段，书写方式不一而足
      - 用户ID常见写法：id uid userid ID UID USERID userID等等
      - 文章ID常见写法：articleId articleid article_id articleID artid artID等等
   - 分页：page limit ~~`page不要用pg简写`~~
3. 请求地址约定
4. [常用命名方法](https://www.cnblogs.com/hamburgerBear/p/7529255.html)
   - 骆驼式（Camel）`articleId`
   - 帕斯卡（Pascal）`ArticleId`
   - 匈牙利（Hungarian）`g_i10ArticleId`
   - 下划线（UnderScore）`article_id`


<a id="%E8%BF%94%E5%9B%9Eresponse%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 返回RESPONSE(未完成)
1. 正确架构
```php
{
    "code": "0000",
    "msg": "success",
    "data": {
        "token": "eyJ0e......",
        "expires_in": 86400
    }
}
```
2. 错误架构
```php
{
    "code": "2000",
    "msg": "Token已经过期，请重新登录",
    "data": "Token has expired"
}
```
3. code约定
```php
    // 用户管理文案
    public static $user_code = [
        1001 => '账号或密码错误',
        1002 => '非法邮箱格式',
        1003 => '非法手机格式',
        1004 => '当前密码错误',
        1005 => '用户不存在',
        1006 => '两次密码不一致',
        1007 => '该用户已存在此角色',
        1008 => '分配角色错误',
        1009 => '用户名输入有误',
        1010 => '退出成功',
        1011 => '非法座机格式',
        1012 => '部分用户已存在此角色',
        1013 => '分配角色成功',
        1014 => '用户已存在',
        1015 => '新密码不能与旧密码相同',
        1016 => '短信验证码错误',
        1017 => '短信验证码已过期',
        1018 => '图片验证码错误',
    ];
```
4. msg约定
   - msg? OR message?
   - 消息难以约定的主要原因是在
      - 前端倾向于给用户展现产品文档中规定好的词语
      - 后端倾向于展现给开发实际的错误信息，但又不能暴露错误的本质
5. data约定

<a id="%E5%BC%82%E5%B8%B8exception%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 异常EXCEPTION(未完成)
1. 捕获异常
```php
try {
} catch (Exception $e) {
}
```
2. 记录异常
3. 异常种类


