<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [REQUEST请求 & RESPONSE响应](#request%E8%AF%B7%E6%B1%82--response%E5%93%8D%E5%BA%94)
- [Laravel MySQL](#laravel-mysql)
    - [判断是否存在某条记录](#%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%E5%AD%98%E5%9C%A8%E6%9F%90%E6%9D%A1%E8%AE%B0%E5%BD%95)
    - [Eloquent ORM用法备忘](#eloquent-orm%E7%94%A8%E6%B3%95%E5%A4%87%E5%BF%98)
- [phpunit单元测试](#phpunit%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)
- [artisan使用](#artisan%E4%BD%BF%E7%94%A8)
- [Laravel事件监听系统\(未完成\)](#laravel%E4%BA%8B%E4%BB%B6%E7%9B%91%E5%90%AC%E7%B3%BB%E7%BB%9F%E6%9C%AA%E5%AE%8C%E6%88%90)
- [表单校验Validator\(未完成\)](#%E8%A1%A8%E5%8D%95%E6%A0%A1%E9%AA%8Cvalidator%E6%9C%AA%E5%AE%8C%E6%88%90)
- [Throttle接口请求频率限制\(未完成\)](#throttle%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E9%A2%91%E7%8E%87%E9%99%90%E5%88%B6%E6%9C%AA%E5%AE%8C%E6%88%90)

<!-- /MarkdownTOC -->
<a id="request%E8%AF%B7%E6%B1%82--response%E5%93%8D%E5%BA%94"></a>
## REQUEST请求 & RESPONSE响应
```php
'https://learnku.com/docs/laravel/5.8/requests/3894'
// 获取请求头信息
Request::server('HTTP_REFERER')
$request()->headers->get('referer')
$request->header('Authorization')
// 中间件向下传参
$request->merge($userInfo);
// 获取中间件传来的参数
$data['userInfo'] = $request->input();
$requestUrl = "http://www.example.com/one/two?key=value";
Request::getPathInfo();return /one/two;
Request::url(); return "http://www.example.com/one/two";
// 跳转到外部域名
return redirect()->away('https://www.google.com');
// 获取路由参数
$request->route('id');
// 返回当前用户请求的中间件
auth()->getDefaultDriver() >>> api api_abchina
// 下载源文件
return Redirect::to('http://img.people.cn/group1/M00/00/00/wKgL11zmP1qAEDmRAAHOjAB5EzI446.jpg');
return response()->streamDownload(function () {
  echo file_get_contents('http://img.people.cn/group1/M00/00/00/wKgL11zmP1qAEDmRAAHOjAB5EzI446.jpg');
}, 'newName.jpg');
```
<a id="laravel-mysql"></a>
## Laravel MySQL
<a id="%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%E5%AD%98%E5%9C%A8%E6%9F%90%E6%9D%A1%E8%AE%B0%E5%BD%95"></a>
### 判断是否存在某条记录
```php
// 判断用户名(手机号)是否存在用户表中
// 第一种方法，主动截取异常信息后返回
try {
    $user = (new User)->where('email', $request['username'])->orWhere('phone', $request['username'])->firstOrFail();
} catch (\Illuminate\Database\Eloquent\ModelNotFoundException $e) {
    return $this::repsErrJson('手机号不存在', [], 1000);
}
// 第二种方法，自定义异常处理器，截取相应异常信息后返回
$user = (new User)->where('email', $request['username'])->orWhere('phone', $request['username'])->firstOrFail();
// 然后在app/Exceptions/Handler.php中render截获特定异常到返回信息中
if ($exception instanceof ModelNotFoundException ) {
    return response()->json([
        'code' => 1000,
        'msg' => '查询不到此条记录',
        'data' => '',
    ], 404);
}
// 第三种方法，通过validator校验器进行异常信息返回
'phone'     =>'required|phone:CN,mobile|exists:users',
// 判断字段‘phone’是否存在于‘exists’表‘users’中
// 其中'exists' => ':attribute不存在',（文件在resources\lang\zh-CN\validation.php）
```
<a id="eloquent-orm%E7%94%A8%E6%B3%95%E5%A4%87%E5%BF%98"></a>
### Eloquent ORM用法备忘
[updateOrInsert OR updateOrCreate](https://blog.csdn.net/u010324331/article/details/82698211)
```php
// 如有更新记录
// 若无插入记录
updateOrInsert()
```
<a id="phpunit%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95"></a>
## phpunit单元测试
```bash
# win上安装
# 为 PHP 的二进制可执行文件建立一个目录，例如 D:\laragon\bin
# 将 ;D:\laragon\bin 附加到 PATH 环境变量中
# 下载 http://phar.phpunit.cn/phpunit-x.x.phar
# 并将文件另存为到 D:\laragon\bin\phpunit.phar(去掉版本号)
# 打开命令行（例如，按 Windows+R » 输入 cmd » ENTER)
# 建立外包覆批处理脚本（最后得到 D:\laragon\bin\phpunit.cmd）：
C:\Users\username> cd D:\laragon\bin
D:\laragon\bin> echo @php "%~dp0phpunit.phar" %* > phpunit.cmd
D:\laragon\bin> exit
# 新开一个命令行窗口，确认一下可以在任意路径下执行 PHPUnit：
C:\Users\username> phpunit --version
    PHPUnit x.y.z by Sebastian Bergmann and contributors.
```
<a id="artisan%E4%BD%BF%E7%94%A8"></a>
## artisan使用
```bash
# 文件目录
# Models
php artisan make:model App\Models\Test
```

<a id="laravel%E4%BA%8B%E4%BB%B6%E7%9B%91%E5%90%AC%E7%B3%BB%E7%BB%9F%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## Laravel事件监听系统(未完成)

<a id="%E8%A1%A8%E5%8D%95%E6%A0%A1%E9%AA%8Cvalidator%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 表单校验Validator(未完成)

<a id="throttle%E6%8E%A5%E5%8F%A3%E8%AF%B7%E6%B1%82%E9%A2%91%E7%8E%87%E9%99%90%E5%88%B6%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## Throttle接口请求频率限制(未完成)
429 Too many requests
https://github.com/laravel/framework/issues/13623