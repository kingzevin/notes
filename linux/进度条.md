
*摘自http://yangtze736.github.io/%E6%8A%80%E6%9C%AF/2018/05/02/shell-tips/*
# 转圈效果
```
function waiting()
{
    i=0
    while [ $i -le 100 ]
    do
        for j in '\\' '|' '/' '-'
        do
            printf "\t\t\t\t%c%c%c%c%c test waiting %c%c%c%c%c\r" \
            "$j" "$j" "$j" "$j" "$j" "$j" "$j" "$j" "$j" "$j"
            sleep 0.1
        done
        let i=i+4
    done
}
```
# 进度条效果

## 通过符号#填充[ ]完成进度

```
#!/bin/bash
i=0
str=""
arry=("\\" "|" "/" "-")
while [ $i -le 100 ]
do
    let index=i%4
    printf "[%-100s] %d %c\r" "$str" "$i" "${arry[$index]}"
    sleep 0.1
    let i=i+1
    str+="#"
done
echo ""
```
## 每个阶段有不同颜色区分进度

```
i=0
str=""
arry=("\\" "|" "/" "-")
while [ $i -le 100 ]
do
    let index=i%4
    if [ $i -le 20 ]; then
        let color=44
        let bg=34
    elif [ $i -le 45 ]; then
        let color=43
        let bg=33
    elif [ $i -le 75 ]; then
        let color=41
        let bg=31
    else
        let color=42
        let bg=32
    fi
    printf "\033[${color};${bg}m%-s\033[0m %d %c\r" "$str" "$i" "${arry[$index]}"
    sleep 1
    let i=i+1
    str+="#"
done
echo ""
```

# 进度条递进填充

```

total_stdy="$(($(stty size|cut -d' ' -f1)))"
total_stdx="$(($(stty size|cut -d' ' -f2)))"

head="Progress bar: "
total=$[${total_stdx} - ${#head}*2]

i=0
loop=100
while [ $i -lt $loop ]
do
    let i=i+1
    
    per=$[${i}*${total}/${loop}]
    remain=$[${total} - ${per}]
    printf "\r\e[${total_stdy};0H${head}\e[42m%${per}s\e[47m%${remain}s\e[00m" "" ""
    sleep 0.1
done

echo ""
```
