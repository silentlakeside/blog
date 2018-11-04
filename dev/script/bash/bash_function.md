## 定义函数

括号里不需要定义输入参数。
$1是第一个参数，$n是第n个参数，$#是参数个数
```bash
function func() {
    arg1=$1
    arg2=$2

    return 0
}
```

## 调用函数

不需要在参数两边加括号
```bash
func $var1 $var2
```