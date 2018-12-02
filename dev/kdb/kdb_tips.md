KDB tips

1. 将float转换成symbol： `$string <float_data>

1. 将symbol转换成float： "F"$string <symbol data>

1. 更新指定列，如果该列的值的第5个字符是0或者.则截取前4个字符，否则截取前5个字符： 
```kdb
update <column name>:`${(5 4 (any "0." in a 4))#a:string x} each <column name> from `<table name>
```

1. KDB可以通过update语句将指定列的类型也同时变更，但是要注意，如果包含了where子句，那么就不能变更，因为部分值仍然是原来的类型。我的做法是先用不带where子句的update语句变更类型，再使用where子句变更值，例如：
```kdb
update <column name>:`$string <column name> from `<table name>;
update <column name>:`<symbol data> from `<table name> where <...>;
```
 不知道有没更好的方法

1. 处理Symbol中的空格等特殊字符

```kdb
正确： dict:`a`b`c!(`a1`a2`a3)
错误： dict:`a`b`c!(`a1`a2`a3 a4)
错误： dict:`a`b`c!(`a1`a2`$"a3 a4")
正确： dict:`a`b`c!`$("a1";"a2";"a3 a4")

q) dict
(Roundtrip: 031ms)
(`a`b`c)!`a1`a2`a3 a4
```

1. 用分隔符连接两个字段并赋值给另一个字段
```kdb
update NEW_COL:"-"sv/: flip (string COL1;string COL2) from `tbl;
```

1. 日期转换时区
```kdb
d1:2013.06.05T00:00:00.000
d2:08:00:00.000
d3:d1+d2

q) d1
(Roundtrip: 016ms)
2013.06.05T00:00:00.000

q) d2
(Roundtrip: 015ms)
08:00:00.000

q) d3
(Roundtrip: 015ms)
2013.06.05T08:00:00.000 
```

1. left join (t1需要包含有key1列，1b用于区分是否在t2有对应的数据)
```kdb
t1 lj `key1 xkey select key1,1b from t2
```

1. 将不补0的时间（时：分：秒）字符串（KDB不能直接将该字符串转换成时间）转换成KDB时间类型

```kdb
append0ToTime:{[timeStr]
    sections:":" vs timeStr;
    sectionCount:count sections;
    index:0;
    do [sectionCount;
        sections[index]:"" sv ("00";sections[index]);
        sections[index]:-2#sections[index];
        index:index+1];
    "V"$":" sv sections
};

result:append0ToTime["9:21:3"];

q) result
(Roundtrip: 156ms)
09:21:03
```

1. 判断文件是否存在（Key是关键字，()代表一个空的list，~是匹配）

```kdb
() ~ key `:c:/q/sp.q 
```

1. 给一个字段赋值（字符）

```kdb
update col:count[i]#enlist "abc" from `table 
```

1. 读取csv文件

```kdb
// load csv with header line
data:("ISS";enlist ",") 0: `:/tmp/data.csv;

// ignore the header line
data:1_filp `ID`Name`Description!("ISS";",") 0: `:/tmp/data.csv; 
```

1. 获取字符型字段、值为空的行

```kdb
select from table where 0=type each column
``` 