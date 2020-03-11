<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Install & Config](#install--config)

<!-- /MarkdownTOC -->
<a id="install--config"></a>
## Install & Config
```bash
curl -L -O https://artifacts.elastic.co/downloads/apm-server/apm-server-6.4.2-x86_64.rpm
sudo rpm -vi apm-server-6.4.2-x86_64.rpm
# 编辑配置文件
vim /etc/apm-server/apm-server.yml
output.elasticsearch
hosts: ["10.38.15.203:9200","10.38.15.214:9200"]
# 先手动启动
/usr/share/apm-server/bin/apm-server -c /etc/apm-server/apm-server.yml -e
# 再加入后台自动启动
sudo chkconfig --add apm-server
systemctl start apm-server
```