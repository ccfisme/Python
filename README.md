## 这是一种独特的存数方式，我头次知道在列表中还能加for循环和if语句来直接存结果，真的是让我大开眼界  

那么，在列表中插入语句的顺序是什么呢?  

根据实战经验，我将其分为两类：  

* 第一类，for循环为第二句


`列表名 = [表达式 for 变量a in 列表/字符串 if 语句 else 变量b for 变量b in 列表/字符串]  `  

左边第二句为最外层，然后往右第二层，以此类推，最后是左边第一条语句

即  

```

第一层：for 变量a in 列表/字符串
第二层：if 表达式 else 变量b
第三层：for 变量b in 列表/字符串
第四层：左边第一条语句->表达式
```
例：  

```
[(x, y) for x in range(5) if x % 2 == 0 for y in range(5) if y % 2 == 1]

等价于下面的一般 for 循环：

L = []
for x in range(5):
    if x % 2 == 0:
for y in range(5):
    if y % 2 == 1:
    L.append((x, y))
```

* 第二类，if语句为第二句

`列表名 = [表达式 if 语句 else 变量 for 变量 in 列表/字符串] `

这种和for语句为第二句的不同，这是一种倒装，要先将for循环提前，然后if语句接表达式，再接else  

即：  

```
第一层：for 变量a in 列表/字符串
第二层：if 语句 表达式 else 变量b
```

例：  

```
[a[ord(c)-65][1] if "A"<=c<="Z" else c for c in s ]

等价于 
for c in s 
    if "A"<=c<="Z"：
        [a[ord(c)-65][1]
    else：
        c
    
```






















