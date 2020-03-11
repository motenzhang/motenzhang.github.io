<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [常用正则](#%E5%B8%B8%E7%94%A8%E6%AD%A3%E5%88%99)

<!-- /MarkdownTOC -->
<a id="%E5%B8%B8%E7%94%A8%E6%AD%A3%E5%88%99"></a>
### 常用正则

```regex
# 匹配正整数
[^1-9]\d*$
/u 
# 表示按unicode(utf-8)匹配（主要针对多字节比如汉字）
/i 
# 表示不区分大小写（如果表达式里面有 a， 那么 A 也是匹配对象）
/s 
# 表示将字符串视为单行来匹配
```