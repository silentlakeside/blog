- BASH脚本第一行，#!用来指定脚本解释器
```bash
#! /bin/bash
``` 
- 检查参数个数（$#是参数个数，$0是命令自身，if语句注意方括号和条件表达式之间有空格）
```bash
if [ $# -lt 2 ]; then
  echo "Usage: $0 <arg1> <arg2> " >&2
  exit 1
fi
```
- 获取命令路径
```bash
SCRIPT_PATH=`dirname $0`
```
- 获取参数（$1是第一个参数，$n是第n个参数），函数里获取参数也是这样
```bash
arg1=$1
arg2=$2
```
- 获取命令输出
```bash
var=`date`
```