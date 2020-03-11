<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [安装](#%E5%AE%89%E8%A3%85)
- [使用](#%E4%BD%BF%E7%94%A8)

<!-- /MarkdownTOC -->

# `Editor's Choice: Passport`
<a id="%E5%AE%89%E8%A3%85"></a>
## 安装
> {danger.fa-close} 安装过程需严格按照安装流程不可跨越

```bash
https://learnku.com/docs/laravel/5.8/passport/3907
# 安装Oauth2-Passport认证
composer require laravel/passport
# 数据表迁移
php artisan migrate
# 创建生成安全访问令牌时所需的加密密钥(个人访问|密码授权)
php artisan passport:install
# 代码修改
# app/User.php
use Laravel\Passport\HasApiTokens
use HasApiTokens, Notifiable
# app/providers/AuthServiceProvider.php
use Laravel\Passport\Passport
Passport::routes()
# config/auth.php
driver' => 'passport
# 加载vue组件
php artisan vendor:publish --tag=passport-components
# 发布vue组件
# resources/js/app.js
Vue.component(
    'passport-clients',
    require('./components/passport/Clients.vue').default
);
Vue.component(
    'passport-authorized-clients',
    require('./components/passport/AuthorizedClients.vue').default
);
Vue.component(
    'passport-personal-access-tokens',
    require('./components/passport/PersonalAccessTokens.vue').default
);
# 安装nodejs并注意修改环境变量
# 更新npm镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org
# 重新编译资源
npm run dev
## 报错:cross-env 执行npm install更新缺失组件
php artisan passport:keys
```
<a id="%E4%BD%BF%E7%94%A8"></a>
## 使用
```php
# 用户名/邮箱/手机号均可作为登录唯一标志
// 通过config\auth.php找到用户认证的model层、providers
// 然后在app\Models\User中对继承自passport方法进行重新定义
public function findForPassport($username){
    return $user = (new User)->where('email', $username)->orWhere('username', $username)->first();
}
# 密码授权
// 通过数据库获取密码授权的client id secret
$client = \Laravel\Passport\Client::where([
    'password_client' => true,
    'revoked'         => false
])->first();
// make an internal request to the passport server
// 内部接口请求无需通过guzzle curl等方法
$tokenRequest = Request::create('/oauth/token', 'post', [
    'grant_type'    => 'password',
    'client_id'     => $client->id,
    'client_secret' => $client->secret,
    'username'      => $request->input('username'),
    'password'      => EncryptDecrypt::decryptRsa($request->input('password')),
]);
// let the framework handle the request
// 验证用户名密码是否正确 通过密码授权方式返回token
$response = app()->handle($tokenRequest);
$responseBody = json_decode($response->content(),true);
# 通过指定用户认证守护器验证用户是否登录并返回用户信息
// 获取用户全量信息
Auth::guard('api')->authenticate()
// 获取用户个别信息
$uid = Auth::guard('api')->id();
$uname = Auth::user()->find($uid)->name;
auth()->user()->id;
Auth::user()->id;
Auth::id();
```