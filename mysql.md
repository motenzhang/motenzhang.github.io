<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [配置释义](#%E9%85%8D%E7%BD%AE%E9%87%8A%E4%B9%89)
- [授权](#%E6%8E%88%E6%9D%83)
- [备份与恢复](#%E5%A4%87%E4%BB%BD%E4%B8%8E%E6%81%A2%E5%A4%8D)
- [MySQL CLI](#mysql-cli)

<!-- /MarkdownTOC -->

<a id="%E9%85%8D%E7%BD%AE%E9%87%8A%E4%B9%89"></a>
## 配置释义
```bash
# case insensitive 不区分大小写 (utf8_general_cs 区分大小写)
utf8_general_ci 
# 判断/开启慢查询
SHOW VARIABLES LIKE '%slow%'
# 开启慢查询记录
SET GLOBAL log_slow_queries=ON
# 设置慢查询记录文件
SET GLOBAL slow_query_log_file='/var/log/mysql.slow.log'
# 设置大于1秒的数据库查询进入日志
SET GLOBAL long_query_time=1
#cnf
slow_query_log = true
log-slow-queries = /tmp/mysql-slow.log
long_query_time = 1
```

<a id="%E6%8E%88%E6%9D%83"></a>
## 授权
```bash
grant all privileges  on *.* to root@'%' identified by "password";
flush privileges;
```
<a id="%E5%A4%87%E4%BB%BD%E4%B8%8E%E6%81%A2%E5%A4%8D"></a>
## 备份与恢复
```bash
# 数据库连接
mysql -hlocalhost -uroot -p123456
# 命令行导入导出数据库命令
mysqldump -h192.168.1.169 -uroot -p'vtestdbpw' cnt_cms | gzip > /home/cnt_cms.sql.gz
mysql -h192.168.1.169 -uroot -p'vtestdbpw' cntcms_test < /home/cnt_cms.sql
# 导出所有数据库
mysqldump -u root -p --all-databases --skip-lock-tables > alldb.sql
# 导入
mysql -u root -p < alldb.sql
```
<a id="mysql-cli"></a>
## MySQL CLI

```sql
-- (模糊)查询当前连接(非仅当前数据库)所有包含xxx的字段名
SELECT * FROM information_schema.`COLUMNS` WHERE COLUMN_NAME LIKE '%siteName%';
-- 时间戳与可读时间互转
SELECT FROM_UNIXTIME('1527207174');
SELECT UNIX_TIMESTAMP('2017-05-26 21:57:33');
SELECT UNIX_TIMESTAMP('2018-03-01');
-- 查询当前数据库所设置时间区域
SHOW VARIABLES LIKE "%time_zone%";
-- 给出当前数据库最适合的字段(5.7下适用，8已废弃)
SELECT * FROM users PROCEDURE ANALYSE(100,25);
-- 重置数据表自增ID为1
ALTER TABLE TABLE_NAME AUTO_INCREMENT = 1
-- 按天计算文章转发量
SELECT DATE_FORMAT(FROM_UNIXTIME(pubtime),'%Y-%m-%d') AS perday,SUM(zz_num) AS amount FROM paper_daily_article GROUP BY perday
# perday     amount
# 2018-12-20 100
# 2018-12-21 200
# 2018-12-22 300
-- 按天增量计算文章转发量
SET @orisum := 0;
SELECT a.perday, a.amount, (@orisum := @orisum + a.amount) AS sumamount
FROM (SELECT DATE_FORMAT(FROM_UNIXTIME(pubtime),'%Y-%m-%d') AS perday,SUM(zz_num) AS amount FROM paper_daily_article GROUP BY perday ) AS a
# perday     amount sumamount
# 2018-12-20 100    100
# 2018-12-21 200    300
# 2018-12-22 300    600
# 数据库中 = 表示等于 >> 类似php中 ==
# 数据库中 := 表示赋值 >> 类似php中 =
-- 计算表中某字段(例 分数分布|地域分布|性别(适用男中女，男女就不用这么麻烦了))的百分比
SELECT
  sta_toa.status_total AS 'total',
  sta_0.status_total AS '-1',
  CONCAT((sta_1.status_total/sta_toa.status_total)*100,'%') AS '1',
  sta_1.status_total AS '0',
  CONCAT((sta_0.status_total/sta_toa.status_total)*100,'%') AS '1',
  sta_2.status_total AS '1',
  CONCAT((sta_2.status_total/sta_toa.status_total)*100,'%') AS '1'
FROM
  (SELECT COUNT(*) AS status_total,credit_score FROM user_info_bak WHERE credit_score = '2' GROUP BY sexual) AS sta_0,
  (SELECT COUNT(*) AS status_total,credit_score FROM user_info_bak WHERE credit_score = '0' GROUP BY sexual) AS sta_1,
  (SELECT COUNT(*) AS status_total,credit_score FROM user_info_bak WHERE credit_score = '1' GROUP BY sexual) AS sta_2,
  (SELECT COUNT(*) AS status_total FROM user_info_bak) AS sta_toa
-- 查询表中是否有重复的值
SELECT uid,COUNT(*) AS COUNT FROM `user_info` GROUP BY uid HAVING COUNT > 1;
-- 删除表中重复的值 且保留较大的值(根据主键ID|时间|其他字段)
DELETE n1 FROM user_info n1, user_info n2 WHERE n1.id < n2.id AND n1.user_id = n2.user_id;
DELETE FROM user_info
 WHERE id NOT IN (
    SELECT * FROM (SELECT MAX(n.id) FROM user_info AS n GROUP BY n.user_id) X
 )；
-- 增加字段
ALTER TABLE test.test4 ADD COLUMN test VARCHAR(255) NULL AFTER user_id;
-- 插入随机数
INSERT INTO test4(user_id) VALUES(CAST(RAND()*10 AS SIGNED));
# rand函数返回(0,1]的随机数
# round(1.234,2)返回带有2位小数位的数据
SELECT ROUND(1.234,2)
# 随机顺序对结果进行排序(效率不好 慎用)
SELECT * FROM users ORDER BY RAND();
# cast函数转换第一个参数为指定类型(整数|时间格式等)
# 获取当前时间戳的整形格式
SELECT CAST(NOW() AS SIGNED);
-- case when用法进行统计计算
# count()函数内代表计算的基数值 1代指第一个字段(一般默认为表主键ID)
SELECT
  COUNT(1) AS '计数',
  CASE TYPE
    WHEN '1' THEN '互动'
    WHEN '2' THEN '新增'
    ELSE 'ERROR'
  END '用户类型',
  CASE header_type
    WHEN '1' THEN '人民日报'
    WHEN '2' THEN '央视新闻'
    WHEN '3' THEN '新华视点'
    ELSE 'ERROR'
  END '用户来源'
FROM
  weibo_user_type
GROUP BY TYPE, header_type ;
-- 计算通过率
SELECT
  a.urank,
  SUM(IF(a.is_gte = 1, a.num, 0)) / SUM(a.num) * 100 AS pass_rate
  (SELECT urank,INTERVAL(credit_score, 60) AS is_gte,COUNT(1) AS num
FROM
    weibo_user_type GROUP BY urank,is_gte) a
GROUP BY a.class
# if 判断语句 类似三元运算
# INTERVAL()函数进行比较列表(N，N1，N2，N3等等)中的N值。该函数如果N<N1返回0，如果N<N2返回1，如果N<N3返回2等等
# 如果N为NULL，它将返回-1,列表值必须是N1<N2<N3的形式才能正常工作
SELECT INTERVAL(6,1,2,3,4,5,6,7,8,9,1);-- 返回比N大的位置6(索引起始位为0)
# 比较值的大小
SET @score := 50;
SELECT INTERVAL(@score, 60);
-- 按照IN里面的值进行排序，同样适用于中文
SELECT * FROM TABLE WHERE id IN (3,2,1) ORDER BY FIELD(id,3,2,1);
SELECT * FROM TABLE WHERE name IN ('北京日报','千龙网','BTV') ORDER BY FIELD (siteName,'北京日报','千龙网','BTV');
```

```sql
-- 优化 —— Optimization
# 根据某字段值所占总数百分比计算是否需要添加索引
SELECT
  COUNT(DISTINCT(field_a)) / COUNT(*) AS field_a_cardinality,
  COUNT(DISTINCT(field_b)) / COUNT(*) AS field_b_cardinality,
  COUNT(*) AS total_num
FROM
  table_name
# cardinality
# 上述查询计算字段a和字段b的值分别占总数的百分比
# 以男女性别为例，如总数据为100W，男女各占50%，则需要建立索引
# 以男女性别为例，如总数据为100W，男占80%，女占20%(阈值)，则 不 需要建立索引
# 一般设定阈值为20%～30%
-- SQL_NO_CACHE 不使用缓存
EXPLAIN SELECT SQL_NO_CACHE * FROM users;
-- 列出数据库服务器当前进程
SHOW PROCESSLIST;
-- 延迟关联索引优化limit查询/分页
# id自增主键的100W行数据表
# 每页10条数据 求取第90W页
-- 优化前语句
EXPLAIN SELECT SQL_NO_CACHE * FROM js_news LIMIT 900000,10;
-- 优化后语句
EXPLAIN SELECT SQL_NO_CACHE * FROM js_news WHERE id > (900000 - 10) LIMIT 10;
```

- [x] 推荐使用

```sql
-- 常用函数
# length(返回字符串所占字节——byte数，1汉字=3字节)
# char_length(返回字符串所占字符——character数)
SELECT LENGTH('数据库'), CHAR_LENGTH('数据库'); >> 9,3
SELECT LENGTH('mysql'), CHAR_LENGTH('mysql');  >> 5,5
# concat 字段合并
SELECT CONCAT(lastname,firstname) FROM users;
-- left right 函数
SELECT LEFT(FROM_UNIXTIME('1516585127'),10); >> 2018-01-22
-- 函数堆叠使用
SELECT ID,siteName,areaIds,LENGTH(areaIds) AS len, areaNames FROM website WHERE INSTR(TRIM(areaIds), ' ') > 0 ORDER BY len DESC
-- 带中文的年月日转换
SELECT STR_TO_DATE('2016年1月10日','%Y年%m月%d日'); -- 2016-01-10
SELECT UNIX_TIMESTAMP(STR_TO_DATE('2016年1月10日','%Y年%m月%d日')); -- 1452355200
```

- [ ] 不推荐程序中使用,但在确认问题时可用

```sql
-- 不常用函数
# 根据正则查询判断
SELECT *, REPLACE(`body`, "1", "<em>""1""</em>") AS `s_body` FROM `purify_ugc_info` WHERE  INSTR(`body`, "1") > 0  ORDER BY `id` ASC;
# replace('str','from_str','to_str')
# instr和locate都可以定位字符出现在字符串的位置
SELECT INSTR("Alibaba", "ba")-- returns 4
SELECT LOCATE("ba", "Alibaba")-- returns 4 because the third parameter was not specified
SELECT LOCATE("ba", "Alibaba", 5)-- returns 6
# 函数instr locate position find_in_set均为类似功能 如用到mysql查询 则会拖累数据库
# 功能与like查询相像 但返回值不同
```

```sql
-- C平台获取平台栏目规则
SELECT
  a.productId,a.productName,a.channelName,a.channelNewName,a.channelId,b.conditionId,d.artType,c.columnName,d.conditionName,d.xml,c.platformColumnId
FROM
  `channel_info` AS a,
  `column_condition_relate` AS b,
  `column_info` AS c,
  `condition_info` AS d
WHERE a.productId = b.productId
  AND a.productId IN(2,3,7,11,13,26,33,36,48,58,59,61,63,64,88,113,120,123,124,126,127,130,132,135,145,147,150,154,155,157,158,163,165,167,170,171,172,173,174,182,192,194,197,198,200,201,203,205,206,207,208,213,214,216,219,220,221,222,225,230,233,234,236,238,240,241,243,245,249,257,258,262,265,271,273,282,285,288,290,292,295,296,301,303,305,307,309,310,312,313,318,319,322,323,330,336,338,341,342,345,347,351,353,357,358,360,362,363,364,369,372,378,379,380,388,397,398,399,400,401,406,409,416,422,425,430,441,448)
  AND b.columnId = c.id -- 栏目/菜单ID对应关系
  AND (
      (c.unionColId = '30' AND a.channelId = 184)-- 舆情预警
   OR (c.unionColId = '20' AND a.channelId = 185)-- 实时监测
   OR (c.unionColId = '40' AND a.channelId = 186)-- 微博监测
   -- OR (c.unionColId = '0' AND a.channelId = 187)-- 热点事件-不在此配置，后台文章管理-热点事件
   -- OR (c.unionColId = '50' AND a.channelId = )-- 仅5个平台用此通用平台ID
   OR (c.unionColId = '60' AND a.channelId = 188)-- 人物监测 领导舆情
   OR (c.unionColId = '70' AND a.channelId = 189)-- 外媒监测
   OR (c.unionColId = '82' AND a.channelId = 190)-- 行业监测-行业文章
   OR (c.unionColId = '80' AND a.channelId = 246)-- 行业监测-竞争对手
   OR (c.unionColId = '99' AND a.channelId = 191)-- 统计分析 文章
   OR (c.unionColId = '90' AND a.channelId = 191)-- 统计分析 微博
   -- OR (c.unionColId = '90' AND a.channelId = 192)-- 舆情报告-不在此配置
   OR (c.unionColId = '140' AND a.channelId = 253)-- 职能监测 中央巡视 巡视组
   OR (c.unionColId = '90' AND a.channelId = 291)-- 移动微博-意见领袖
   -- OR (c.unionColId = '0' AND a.channelId = 292)-- 视频监测-暂不列出
   OR (c.unionColId = '952' AND a.channelId = 445)-- 微信监测
   OR (c.unionColId = '310' AND a.channelId = 587)-- 区域监测
   -- OR (c.unionColId = '0' AND a.channelId = 618)-- 意见领袖-微博领袖-不在此配置后台微博意见领袖管理处获取数据
  )
  AND b.conditionId = d.id
  -- and d.artType = 1 -- 1文章 2微博
  AND d.termType = 1 -- 1列表 2统计
  -- and c.platformColumnId = 3
  GROUP BY a.productId,c.unionColId 
  ORDER BY a.productId,a.channelId,d.artType ASC
```
