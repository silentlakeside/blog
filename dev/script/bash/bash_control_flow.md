- if
```bash
if <条件表达式>; then
fi

if <条件表达式>; then
else
fi

if <条件表达式>; then
elif <条件表达式>; then
else
fi 
```
- until
```bash
unitl <条件表达式>; do
done 
```
- while
```bash
while <条件表达式>; do
done
``` 
- case
```bash
case $var in
  value1)
    ;;
  value2)
    ;;
  *)
    ;;
esac 
```
- for
```bash
for file in /tmp*; do
  echo $file
done

for (( i=0; i<5; i++)); do
  echo $i
done
``` 