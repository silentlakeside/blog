有时候需要执行组装的命令或者外部（例如文件）定义的命令，需将这些命令定义为一个变量，然后执行。

## 直接执行

```bash
cmd="ls -l"
$cmd
```
但这种方式不适用于多个命令或者一些复杂的命令，例如
```
cmd="ls -l > a.log 2>&1"
$cmd

cmd="cd; ls -l"
$cmd
```
会报如下错误（a.log存在）
```bash
ls: >: No such file or directory
ls: 2>&1: No such file or directory
-rw-r--r-- 1 v504613 acsot 641 Feb  6 16:36 a.log
./a.sh: line 10: cd;: command not found
```

## 使用eval

```bash
cmd="ls -l"
eval $cmd

cmd="ls -l > a.log 2>&1"
eval $cmd

cmd="cd; ls -l"
eval $cmd
```