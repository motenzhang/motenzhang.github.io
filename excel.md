<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [比较两列数据差异](#%E6%AF%94%E8%BE%83%E4%B8%A4%E5%88%97%E6%95%B0%E6%8D%AE%E5%B7%AE%E5%BC%82)
- [计算百分比](#%E8%AE%A1%E7%AE%97%E7%99%BE%E5%88%86%E6%AF%94)
- [填充空白区域数据](#%E5%A1%AB%E5%85%85%E7%A9%BA%E7%99%BD%E5%8C%BA%E5%9F%9F%E6%95%B0%E6%8D%AE)
- [插入特殊符号](#%E6%8F%92%E5%85%A5%E7%89%B9%E6%AE%8A%E7%AC%A6%E5%8F%B7)

<!-- /MarkdownTOC -->


<a id="%E6%AF%94%E8%BE%83%E4%B8%A4%E5%88%97%E6%95%B0%E6%8D%AE%E5%B7%AE%E5%BC%82"></a>
## 比较两列数据差异
```bash
COUNTIF(B:B,A1)
```
<a id="%E8%AE%A1%E7%AE%97%E7%99%BE%E5%88%86%E6%AF%94"></a>
## 计算百分比
```bash
# B100为和值
$B1/$B$100
```
<a id="%E5%A1%AB%E5%85%85%E7%A9%BA%E7%99%BD%E5%8C%BA%E5%9F%9F%E6%95%B0%E6%8D%AE"></a>
## 填充空白区域数据

- 选中处理的区域 
- F5 
- 定位条件 
- 空值填充 
- 填充第一个空值后 
- CRTL+ENTER 
- 其他值同时会被填充

<a id="%E6%8F%92%E5%85%A5%E7%89%B9%E6%AE%8A%E7%AC%A6%E5%8F%B7"></a>
## 插入特殊符号
```bash
# 插入对号
按住Alt，输入41420，松开Alt，得到对号
# 插入错号
同理，输入41409，得到错号
```