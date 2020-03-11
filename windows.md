<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [Windows常用命令](#windows%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)

<!-- /MarkdownTOC -->
<a id="windows%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
## Windows常用命令
<kbd>Win</kbd> + <kbd>R</kbd>打开命令行终端
```bash
# 显示DNS缓存内容
ipconfig /displaydns
# 删除DNS缓存内容
ipconfig /flushdns
# windows系统下在dos命令行kill掉被占用的pid
taskkill /F /pid 1288
# win下查找占用端口的任务ID
netstat -ano | findstr 8080
# 根据上一步的ID列出对应进程名称
tasklist | findstr 14180
```