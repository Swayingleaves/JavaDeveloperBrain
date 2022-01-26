## 联合索引
对列col1、列col2和列col3建一个联合索引

联合索引 test_col1_col2_col3 实际建立了(col1)、(col1,col2)、(col,col2,col3)三个索引。
```sql
SELECT * FROM test WHERE col1=“1” AND clo2=“2” AND clo4=“4”
```
上面这个查询语句执行时会依照最左前缀匹配原则，检索时会使用索引(col1,col2)进行数据匹配。 

对于联合索引(col1,col2,col3)，查询语句SELECT * FROM test WHERE col2=2;是否能够触发索引？
```sql
EXPLAIN SELECT col2 FROM test WHERE col2=2;
EXPLAIN SELECT * FROM test WHERE col2=2;
EXPLAIN SELECT col1 FROM test WHERE col1=1;
EXPLAIN SELECT * FROM test WHERE col1=1;

```
观察上述两个explain结果中的type字段。查询中分别是：
- type: index
- type: ALL
- type: ref
- type: ref

## 建表有什么优化的地方
- 表需要主键
- 不使用外键
- 字段设置尽量不设为null
- 尽量建联合索引
- 查询频繁使用的字段记得加索引
- 数据值区分不大，数据量小情况不建索引
- 尽量满足三范式，但也是根据业务需求可以添加冗余字段
- 尽量选择小的数据类型，数据类型选择上尽量tinyint(1字节)>smallint(2字节)>int(4字节)>bigint(8字节)，比如逻辑删除yn字段上（1代表可用，0代表）就可以选择tinyint（1字节）类型
- 避免宽表，能拆分就拆分，一个表往往跟一个实体域对应，就像设计对象的时候一样，保持单一原则
- 尽量避免使用text和blob，如果非使用不可，将类型为text和blob的字段在独立成一张新表，然后使用主键对应原表
- 金额 decimal
- 如果表的数量可以预测到非常大，最好在建表的时候，就进行分表，不至于一时间数据量非常大导致效率问题

## 写SQL的时候要注意什么
- 尽量不要使用select * 使用 select col 
- 使用count(*)或count(1)来统计行数来查询，使用count(列)的时候，需要在查看列中这个是否为null,不会统计此列为null的情况，而且mysql已经对count(*)做了优化
- 联合索引要注意where条件满足最左匹配
- 不要使用 where 函数(列名)= ss  这样,会使索引失效

## char和varchar区别
1、最大长度： char最大长度是255字符，varchar最大长度是65535个字节。

2、定长： char是定长的，不足的部分用隐藏空格填充，varchar是不定长的。

3、空间使用： char会浪费空间，varchar会更加节省空间。

4、查找效率： char查找效率会很高，varchar查找效率会更低。

5、尾部空格： char插入时可省略，vaechar插入时不会省略，查找时省略。