### HQL_Note

#### 1 hive splict, explode, lateral view, concat_ws, collect_set

```sql
create table arrays (x array<string>)
row format delimited fields terminated by '\001'
collection items terminated by '\002';

load data local inpath '/home/zhangchao/arrays.text' into table arrays;
["a","b"]
["c","d","e"]

select explode(x) as xx from arrays; 
select concat_ws(',', '1','2','3','4') from arrays;
select split(concat_ws(',', '1','2','3','4'),',')[3] from arrays;
select explode(split(concat_ws(',', '1','2','3','4'),',')) from arrays;
select *, sp from arrays lateral view explode(split(concat_ws(',','1','2','3','4'),',')) a as sp;
select 'xx' ,sp from arrays lateral view explode(split(concat_ws(',','1','2','3','4'),',')) a as sp;

select * from lateral_test; --999
select * , sp  from lateral_test lateral view explode(split(concat_ws(',','1','2','3','4','5'),',')) as sp;
select lateral_test.* , sp  from lateral_test lateral view explode(split(concat_ws(',','1','2','3','4','5'),',')) a as sp;
select lateral_test.* , sp  from lateral_test lateral view explode(split(concat_ws(',','1','2','3','4','5'),',')) a as sp;

--collect_set a string, b string, c int
c d 1
c d 2
c d 3
e f 4
e f 5
e f 6
select a, b, concat_ws(',' , collect_set(cast(c as string)))
from table group by a,b;
c d 1,2,3
e f 4,5,6
```



