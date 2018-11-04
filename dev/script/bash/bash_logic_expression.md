以下均用if语句用作逻辑表达式的例子。注意左右两方括号和条件表达式之间都必须有空格。
 
- 字符串判断
```bash
# 空和非空可以用于判断变量是否已经定义
if [ -z "$var" ]; then
    # 空
fi
if [ -n "$var" ]; then
    # 非空
fi
if [ "$var" == "Y" ]; then
    # 相等
fi
if [ "$var" != "Y" ]; then
    # 不等
fi
```

- 判断文件状态
```bash
if [ -e $var ]; then
    # 文件或者目录存在
fi
if [ -f $var ]; then
    # 一般文件存在
fi
if [ -d $var ]; then
    # 目录存在
fi
```

- 数字比较
```bash
if [ $var -eq 1 ]; then
    # 等于
fi
if [ $var -ne 1 ]; then
    # 不等于
fi
if [ $var -gt 6 ]; then
    # 大于
fi
if [ $var -lt 5 ]; then
    # 小于
fi
```

- 逻辑或、逻辑与
```bash
if [ $var -lt 5 -o $var -gt 6 ]; then
    # 小于5或者大于6
fi
if [ $var -gt 2 -a $var -lt 6 ]; then
    # 大于2而且小于6
fi
```