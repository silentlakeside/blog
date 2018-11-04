```bash
# 显式定义数组
declare -a arr

# 赋值（下标从0开始）
arr[0]="element0"
arr[1]="element1"

# 取值
ele0=${arr[0]}
ele1=${arr[1]}

# 遍历
for ele in ${arr[@]}; do
    echo $ele
done
```