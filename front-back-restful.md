<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [~~`伪`~~RESTful API](#%7E%7E%E4%BC%AA%7E%7Erestful-api)

<!-- /MarkdownTOC -->
<a id="%7E%7E%E4%BC%AA%7E%7Erestful-api"></a>
## <a href="https://zh.wikipedia.org/wiki/REST" target="_blank">~~`伪`~~RESTful API</a>
```bash
目前所用RESTful为其行，内在逻辑并非完全遵循设计者的规范，亟需商议确定下来
```
```bash
自从Roy·Fielding博士在2000年他的博士论文中提出REST风格的软件架构模式后，REST就基本上迅速取代了复杂而笨重的SOAP，
成为WebAPI的标准了，RESTful（遵循REST原则的web服务）目的是便于不同软件、程序在网络中互相传递信息。  
```
```bash
REST不是“rest”这个单词，而是 REpresentation State Transfer的缩写，直译：表现层状态转换，
通俗的说法是：URL定位资源，通过HTTP动词（GET，POST，DELETE，PUSH等）来描述操作。
```
1. 动词 + 宾语
   - RESTful 的核心思想就是，客户端发出的数据操作指令都是`"动词 + 宾语"`的结构
   - 比如，GET `/articles`这个命令，GET是动词，`/articles`是宾语。
   - 动词通常就是五种 HTTP 方法，对应 CRUD 操作，根据 HTTP 规范，动词一律大写
      - `GET`：读取（Read）
      - `POST`：新建（Create）
      - `PUT`：更新（Update）
      - `PATCH`：更新（Update），通常是部分更新
      - `DELETE`：删除（Delete）
2. ~~`动词的覆盖`~~
   - 有些客户端只能使用GET和POST这两种方法，服务器必须接受POST模拟其他三个方法（PUT、PATCH、DELETE）
   - 这时，客户端发出的 HTTP 请求，要加上`X-HTTP-Method-Override`属性，告诉服务器应该使用哪一个动词，覆盖POST方法
```bash
    POST /api/Person/4 HTTP/1.1  
    X-HTTP-Method-Override: PUT
```
   - 上面代码中，X-HTTP-Method-Override指定本次请求的方法是PUT，而不是POST
   - `由于现在主要用GET POST两种请求方法，是否使用这种方式视以后情况而定`
3. 宾语必须是名词
   - 宾语就是API的URL，是HTTP动词作用的对象，它应该是名词，不能是动词，比如，`/articles`这个 URL 就是正确的，而下面的 URL 不是名词，所以都是错误的
```bash
    /getAllCars
    /createNewCar
    /deleteAllRedCars
```
4. 复数 URL
   - 既然 URL 是名词，那么应该使用复数，还是单数？
   - 这没有统一的规定，但是常见的操作是读取一个集合，比如GET `/articles`（读取所有文章），这里明显应该是复数
   - 为了统一起见，建议都使用复数 URL，比如GET `/articles/2`要好于GET `/article/2`
5. 避免多级 URL
   - 常见的情况是，资源需要多级分类，因此很容易写出多级的 URL，比如获取某个作者的某一类文章
```bash
    GET /authors/12/categories/2
```
   - 这种 URL 不利于扩展，语义也不明确，往往要想一会，才能明白含义
   - 更好的做法是，除了第一级，其他级别都用查询字符串表达
```bash
    GET /authors/12?categories=2
```
   - 下面是另一个例子，查询已发布的文章，你可能会设计成下面的 URL：
```bash
    GET /articles/published
```
   - 查询字符串的写法明显更好：
```bash
    GET /articles?published=true
```