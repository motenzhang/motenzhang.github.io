<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Laravel常见问题](#laravel%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)
	- [Class config does not exist](#class-config-does-not-exist)
	- [页面显示白板无任何错误信息](#%E9%A1%B5%E9%9D%A2%E6%98%BE%E7%A4%BA%E7%99%BD%E6%9D%BF%E6%97%A0%E4%BB%BB%E4%BD%95%E9%94%99%E8%AF%AF%E4%BF%A1%E6%81%AF)
	- [数据库连接异常](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E5%BC%82%E5%B8%B8)
	- [数据库连接格式](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%A0%BC%E5%BC%8F)
- [Nginx常见问题](#nginx%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)
	- [超出上传文件限制](#%E8%B6%85%E5%87%BA%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E9%99%90%E5%88%B6)
	- [重启NGINX报错](#%E9%87%8D%E5%90%AFnginx%E6%8A%A5%E9%94%99)
- [Git常见问题](#git%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)
	- [重新忽略GIT文件](#%E9%87%8D%E6%96%B0%E5%BF%BD%E7%95%A5git%E6%96%87%E4%BB%B6)
	- [git diff提示filemode发生改变](#git-diff%E6%8F%90%E7%A4%BAfilemode%E5%8F%91%E7%94%9F%E6%94%B9%E5%8F%98)
	- [更新远程仓库地址](#%E6%9B%B4%E6%96%B0%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E5%9C%B0%E5%9D%80)
	- [代码推送失败](#%E4%BB%A3%E7%A0%81%E6%8E%A8%E9%80%81%E5%A4%B1%E8%B4%A5)
	- [提交代码时出现换行符问题](#%E6%8F%90%E4%BA%A4%E4%BB%A3%E7%A0%81%E6%97%B6%E5%87%BA%E7%8E%B0%E6%8D%A2%E8%A1%8C%E7%AC%A6%E9%97%AE%E9%A2%98)
- [Win下CMDER软件使用](#win%E4%B8%8Bcmder%E8%BD%AF%E4%BB%B6%E4%BD%BF%E7%94%A8)
	- [cmder添加常用命令别名](#cmder%E6%B7%BB%E5%8A%A0%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E5%88%AB%E5%90%8D)
- [收藏夹](#%E6%94%B6%E8%97%8F%E5%A4%B9)
	- [Laravel DOC](#laravel-doc)

<!-- /MarkdownTOC -->
> {info} 所有错误优先查看日志信息 配合ELK食用更佳

<a id="laravel%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98"></a>
## Laravel常见问题
<a id="class-config-does-not-exist"></a>
### Class config does not exist
Q:`Uncaught exception 'ReflectionException' with message 'Class config does not exist'`  
A:`删除 bootstrap/cache/\*.php` `确认config目录下不缺少如app.php等配置文件`
<a id="%E9%A1%B5%E9%9D%A2%E6%98%BE%E7%A4%BA%E7%99%BD%E6%9D%BF%E6%97%A0%E4%BB%BB%E4%BD%95%E9%94%99%E8%AF%AF%E4%BF%A1%E6%81%AF"></a>
### 页面显示白板无任何错误信息
Q:`白板显示可能会有多种原因 待追加`  
A:`.env文件里类如APP_NAME="lara vel"中间如若有空格需加引号`
<a id="%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E5%BC%82%E5%B8%B8"></a>
### 数据库连接异常
Q:`Malformed UTF-8 characters, possibly incorrectly encoded`  
A:`mysql或redis没有连接成功(一般情况)`

<a id="%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%A0%BC%E5%BC%8F"></a>
### 数据库连接格式
Q:`SQLSTATE[42000]: Syntax error or access violation: 1055 Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'uam.roles.id' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by`
A:`config/database.php`中所用到的数据库连接验证格式改为`'strict' => false,`

<a id="nginx%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98"></a>
## Nginx常见问题
<a id="%E8%B6%85%E5%87%BA%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E9%99%90%E5%88%B6"></a>
### 超出上传文件限制
Q:`413 Request Entity Too Large`  
A:`nginx默认上传文件为1m`  
`vim /usr/local/nginx/conf/nginx.conf`  
在http中添加`client_max_body_size 10m;`  
<a id="%E9%87%8D%E5%90%AFnginx%E6%8A%A5%E9%94%99"></a>
### 重启NGINX报错
Q:`NGINX [error] open() /usr/local/Nginx/logs/nginx.pid`  
A:`指定配置文件重新加载`  
`/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf`  
<a id="git%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98"></a>
## Git常见问题
<a id="%E9%87%8D%E6%96%B0%E5%BF%BD%E7%95%A5git%E6%96%87%E4%BB%B6"></a>
### 重新忽略GIT文件
Q:`ignore已被提交到git库的文件`  
A:`原因：git ignore只会对不在git仓库中的文件进行忽略`  
`解决：先删除文件 >> push(同步) >> 新建文件 >> ignore新文件 >> push`  
<a id="git-diff%E6%8F%90%E7%A4%BAfilemode%E5%8F%91%E7%94%9F%E6%94%B9%E5%8F%98"></a>
### git diff提示filemode发生改变
Q:`old mode 100644、new mode 10075`  
A:`git config --add core.filemode false`  
<a id="%E6%9B%B4%E6%96%B0%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E5%9C%B0%E5%9D%80"></a>
### 更新远程仓库地址
Q:`git 修改远程仓库地址`  
A1:`直接修改覆盖原地址git remote set-url origin [url]`  
A2:先删后加`git remote rm origin git remote add origin [url]`  
<a id="%E4%BB%A3%E7%A0%81%E6%8E%A8%E9%80%81%E5%A4%B1%E8%B4%A5"></a>
### 代码推送失败
Q：`! [rejected]        master -> master (non-fast-forward)`  
A:`git config --global push.default current`    
`git branch --set-upstream-to=origin/dev`  
<a id="%E6%8F%90%E4%BA%A4%E4%BB%A3%E7%A0%81%E6%97%B6%E5%87%BA%E7%8E%B0%E6%8D%A2%E8%A1%8C%E7%AC%A6%E9%97%AE%E9%A2%98"></a>
### 提交代码时出现换行符问题
Q:`warning: LF will be replaced by CRLF` 
A:`git config --global core.autocrlf false` 
<a id="win%E4%B8%8Bcmder%E8%BD%AF%E4%BB%B6%E4%BD%BF%E7%94%A8"></a>
## Win下CMDER软件使用
<a id="cmder%E6%B7%BB%E5%8A%A0%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E5%88%AB%E5%90%8D"></a>
### cmder添加常用命令别名
Q:cmder本为win下软件 不支持ll等Linux缩写  
A：`vim c:\cmder\config\user_aliases.cmd`    
`gs=git status`   
`ll=ls -gohlat --show-control-chars -F --color $*`  

<a id="%E6%94%B6%E8%97%8F%E5%A4%B9"></a>
## 收藏夹
<a id="laravel-doc"></a>
### Laravel DOC
> * [官方文档(英文)](https://laravel.com/docs/5.8)
> * [机翻文档(中文)](https://learnku.com/docs/laravel/5.8)
> * [开发规范](https://learnku.com/docs/laravel-specification/5.5)
> * [命令速查表(中文旧版)](https://cs.laravel-china.org/)
> * [命令速查表(英文)](https://cheats.jesse-obrien.ca/)
> * [API速查表(英文)](https://laravel.com/api/5.8)
> * [生命周期](https://www.jianshu.com/p/08b810b720d9)
> * [Socket.IO聊天系统](https://github.com/tlaverdure/laravel-echo-server)
> * [Swoole WebSocket聊天系统](https://www.jianshu.com/p/65ed802ab393)
> * 国外较好论坛
>> * [StackOverFlow](http://stackoverflow.com/)
>> * [Laracasts](https://laracasts.com/discuss)
>> * [Reddit](https://www.reddit.com/r/laravel/)


![end logo](http://newsysfile.peopleyuqing.com/group1/M00/00/01/CiYL2FwnF3KATxlEAAKkLos2QDA992.bmp)