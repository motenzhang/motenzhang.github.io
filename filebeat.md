<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Install & Config](#install--config)

<!-- /MarkdownTOC -->
<a id="install--config"></a>
## Install & Config
```bash
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.4.2-x86_64.rpm
sudo rpm -vi filebeat-6.4.2-x86_64.rpm
start automatically during boot
sudo chkconfig --add filebeat
sudo service filebeat start
sudo filebeat modules enable apache2
filebeat -configtest -c /etc/filebeat/modules.d/apache2.yml
```
