<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [指定安装目录](#%E6%8C%87%E5%AE%9A%E5%AE%89%E8%A3%85%E7%9B%AE%E5%BD%95)
- [JDK Upgrade](#jdk-upgrade)
- [配置](#%E9%85%8D%E7%BD%AE)
- [备份与恢复](#%E5%A4%87%E4%BB%BD%E4%B8%8E%E6%81%A2%E5%A4%8D)

<!-- /MarkdownTOC -->
<a id="%E6%8C%87%E5%AE%9A%E5%AE%89%E8%A3%85%E7%9B%AE%E5%BD%95"></a>
## 指定安装目录
```bash
cd /usr/local/
```
<a id="jdk-upgrade"></a>
## JDK Upgrade
```bash
yum makecache fast
yum search java | grep jdk
yum install java-1.8.0-openjdk.x86_64
java -version
```
<a id="%E9%85%8D%E7%BD%AE"></a>
## 配置
```bash
# 确定安装版本
vim /etc/yum.repos.d/elasticsearch.repo
[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
# 安装
sudo yum install elasticsearch
# 默认安装目录
cd /usr/share/elasticsearch/
# 配置文件
vim /etc/elasticsearch/elasticsearch.yml
# 系统自启动
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
# 启动服务
sudo systemctl start elasticsearch.service
sudo service elasticsearch restart
# 打开远程连接
vim /etc/elasticsearch/elasticsearch.yml
open server.port
update server.host: "0.0.0.0"(all ips)
# 搭建ES Cluster
vim /etc/elasticsearch/elasticsearch.yml
# 打开tcp传输端口
transport.tcp.port: 9300
# 设置集群IP数组
discovery.zen.ping.unicast.hosts: ["10.38.15.203:9300","10.38.15.214:9300"]
# 测试连接
curl -XGET 'localhost:9200/?pretty'
# 其他
es rmzx1234
sudo chown -R es:es elasticsearch
# 卸载
rpm -e elasticsearch-6.1.2-1.noarch
vim /etc/security/limits.d/90-nproc.conf
# 开启匿名登录
xpack.security.enabled: false
# 查看当前节点的所有Index
curl -X GET 'http://localhost:9200/_cat/indices?v'
```
<a id="%E5%A4%87%E4%BB%BD%E4%B8%8E%E6%81%A2%E5%A4%8D"></a>
## 备份与恢复
```bash
# 安装elasticdump
# 安装epel软件包(Extra Packages for Enterprise Linux)
yum install -y epel-release
yum install -y npm
# 设置npm 安装以http连接 (如果是https则不需要)
npm config set strict-ssl false
# 全局安装备份工具 不全局则不需要带-g
npm install elasticdump -g
# 查看帮助手册
elasticdump --help
# 开始导出
# 备份某个索引(sys-es-log)的mapping映射到指定目录|目标地址
elasticdump \
    --input=http://localhost:9200/sys-es-log \
    --output=/usr/share/sys-es-log_mapping.json \
    --type=mapping
elasticdump \
    --input=http://localhost:9200/sys-es-log \
    --output=http://backup:9200/sys-es-log \
    --type=mapping
# 备份某个索引(sys-es-log)的data数据到指定目录
elasticdump \
    --input=http://localhost:9200/sys-es-log \
    --output=/usr/share/sys-es-log.json \
    --type=data
# 备份所有索引(my_index)并压缩data数据到指定目录
elasticdump \
    --input=http://localhost:9200/my_index \
    --output=$ \
    | gzip > /usr/share/my_index.json.gz
# 准备导入
elasticdump \
    --output=http://localhost:9200 \
    --input=/usr/share/my_index.json \
    --type=data
```