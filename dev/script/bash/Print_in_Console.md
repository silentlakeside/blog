echo命令用于打印字符串到控制台
 
命令用法： echo [选项]... [打印内容]
 
选项：

- -n，不打印最后的换行，不加该选项的话会自动附加上一个换行
```
-bash-3.2$ echo aa
aa
-bash-3.2$ echo -n aa
aa-bash-3.2$
```
- -e，支持解析转义字符，如\t，\n等，注意要加上双引号，即便里面是一个变量（echo -e "$var"），否则不能正确解析转义字符
```
-bash-3.2$ echo -e "aa\tbb\ncc"
aa      bb
cc
-bash-3.2$ echo -e aa\tbb\ncc
aatbbncc
```
- -E，不支持解析转义字符，直接把它们当作普通字符串处理，这个是默认选项
```
-bash-3.2$ echo "aa\tbb\ncc"
aa\tbb\ncc
```
