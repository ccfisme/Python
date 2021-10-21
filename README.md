## 列表实现二维数组

今天做题碰到了一个让我为之称赞的存数方式，它来源于一个题，从此题中我不仅学到了python的二维数组的表示方法，还学会了一种新的有序存数方式  

```
编写程序，将输入字符串中的大写英文字母按以下对应规则替换，其他字符不变。

(Python实现提示：转换表用元组实现）

原字母   对应字母
    A        Z
    B        Y
    C        X
    D        W
   ...       ...
    X        C
    Y        B
    Z        A
输入格式:
在一行中输入字符串。

输出格式:
在一行中给出替换完成后的字符串。

输入样例:
This is a pen.
结尾无空行
输出样例:
在这里给出相应的输出。例如：

Ghis is a pen.
结尾无空行



trans=[(chr(65+i),chr(65+25-i)) for i in range(26) ]        # 表示存了26组[a，b]类型的列表
s=input()
lst1=[trans[ord(c)-65][1] if "A"<=c<="Z" else c for c in s ]
print("".join(lst1))

```

说实话，一开始很懵逼，因为看不懂`(chr(65+i),chr(65+25-i))`的含义，后来我抽丝剥茧，把这行代码简化成一次循环  

```
a = [[1,23,4,56,], [1,2,4,56,6]]
print(a[1][2])

# 运行结果为4
```

果然，真的是python中二维数组的表示方法，表中表，而答案给的（）是把列表中的[]换掉了，主要是想体现表中的组内容不可变，其实（）换成[]也是可以的  

然后就是独特的存数方式了，我头次知道在列表中还能加for循环和if语句来直接存结果，真的是让我大开眼界 



[那么，在列表中插入语句的顺序是什么呢?](https://github.com/ccfisme/Python/blob/%E5%88%97%E8%A1%A8%E5%86%85%E5%B5%8C%E8%AF%AD%E5%8F%A5/README.md)










