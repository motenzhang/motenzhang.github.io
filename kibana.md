<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Install & Config](#install--config)

<!-- /MarkdownTOC -->
<a id="install--config"></a>
## Install & Config
```bash
vim /etc/yum.repos.d/kibana.repo
[kibana-6.x]
name=Kibana repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
# 安装kibana
sudo yum install kibana
# 系统自启
sudo chkconfig --add kibana
sudo systemctl start kibana.service
# 配置文件
vim /etc/kibana/kibana.yml
# 打开远程连接
vim /etc/kibana/kibana.yml
open server.port
# 配置本机IP
server.host: "10.38.15.214"
```