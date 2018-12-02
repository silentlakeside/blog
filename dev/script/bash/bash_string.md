使用正则表达式拆分字符串（BASH 3.0以上支持=~正则表达式）
```bash
# 格式：name="value1","value2"
# name、value1和value2是我们需要的字符串
# 在分隔符前后可以有空格（tab等无显示字符不允许）
# 用~=做正则表达式匹配
# [ ]*表示可以有任意空格，()表示里面是要提取的部分，.*表示任意数目的任意字符串，=、，、“都没有定义数目，因此只能有一个
# 匹配表达式右边最好是一个变量，因为在Bash 4.1，右边如果是字符串的话会强制使用字符串匹配而不是把它当作正则表达式
# 请参考http://blog.csdn.net/vimostan/article/details/8213784
# 和http://wiki.bash-hackers.org/syntax/ccmd/conditional_expression
REG='[ ]*(.*)[ ]*=[ ]*"(.*)"[ ]*,[ ]*"(.*)"[ ]*'
if [[ $var =~ $REG ]]; then
    # 用${BASH_REMATCH[n]}获取第n部分，n从1开始
    name=${BASH_REMATCH[1]}
    value1=${BASH_REMATCH[2]}
    value2=${BASH_REMATCH[3]}
fi
```