<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Install & Config](#install--config)

<!-- /MarkdownTOC -->
<a id="install--config"></a>
## Install & Config
```bash
vim /etc/yum.repos.d/logstash.repo
[logstash-6.x]
name=Elastic repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
# 安装logstash
sudo yum install logstash
# 系统自启
sudo initctl start logstash
# 启动服务
sudo systemctl start logstash.service
# 加载配置文件[配置文件格式必须为"UTF-8 Without BOM"(推荐用notepad查看格式并转换)]
./scripts/import_dashboards /usr/share/logstash/bin/logstash -f gstash-mysqltest.conf --path.data=/usr/local/mysqltest/
```