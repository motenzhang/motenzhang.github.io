<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [安装](#%E5%AE%89%E8%A3%85)
- [使用](#%E4%BD%BF%E7%94%A8)

<!-- /MarkdownTOC -->
<a id="%E5%AE%89%E8%A3%85"></a>
## 安装
```bash
# 安装(自定义版本)
wget http://download.redis.io/releases/redis-5.0.4.tar.gz
tar xzf redis-5.0.4.tar.gz
cd redis-5.0.4
make
# vim redis.conf
# 绑定连接redis的地址为所有 + 关闭proteced-mode代表均可访问
bind 127.0.0.1 >> bind 0.0.0.0 
protected-mode yes >> protected-mode no
# 设为后台守护进程启动
daemonize no >> daemonize yes
# 加载配置文件
./src/redis-server redis.conf
# 远程访问6379不行的话
进[媒体云后台](https://www.peopledailycloud.com)修改安全组规则 添加6379端口可见
```
<a id="%E4%BD%BF%E7%94%A8"></a>
## 使用
```bash
redis-cli -h host -p port -a password
# 切换数据库
select 1
# 显示原生key值
redis-cli --raw
# 正则删除数据
redis-cli keys "guangdong__base*" | xargs redis-cli del
# bitmap
SETBIT key offset value
setbit test 132 1
getbit test 132
bitcount test
# redis-cli: command not found
cp /usr/local/redis-5.0.4/src/redis-cli /usr/local/bin/
```
