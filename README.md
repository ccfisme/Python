# join函数基本用法 
* 什么时候用？  

用一个字符将一个序列的元素连接为一个字符串

例：

![截屏2021-10-26 09 27 40](https://user-images.githubusercontent.com/74129445/138793109-bc991aee-ca3a-4a2c-9b78-74e92326a036.png)


* 语法：  

`str.join(iterable)`  
  
  
iterable -- 要连接的元素序列

* 返回值  

返回生成的新字符串

---

## 扩展  

### 去框  

今天遇到一个题，用列表做的，最后输出不知道怎么输出不含框的列表，即</br>
```
7-23 sdut-单链表数据的拆分 (10 分)
输入N个整数顺序建立一个单链表，将该单链表拆分成两个子链表：

第一个子链表存放了所有的偶数，第二个子链表存放了所有的奇数。

两个子链表中数据的相对次序与原链表一致。

输入格式:
第一行输入整数N;

第二行依次输入N个整数，中间用空格隔开。

输出格式:
第1行分别输出偶数链表与奇数链表的元素个数； 

第2行依次输出偶数子链表的所有数据；

第3行依次输出奇数子链表的所有数据。

输入样例:
10
1 3 22 8 15 999 9 44 6 1001
结尾无空行
输出样例:
4 6
22 8 44 6 
1 3 15 999 9 1001
```
经查找后发现都在用join函数，那么究竟怎么用呢？</br>
首先我把复制的代码写出来</br>
```
n = int(input())
a = list(map(int, input().split()))
x = y = 0
b = []
c = []
for i in a:
    if i % 2 == 1:
        x += 1
        b.append(i)
    elif i % 2 == 0:
        y += 1
        c.append(i)
print(y, x)
print(' '.join(str(i) for i in c))
print(' '.join(str(i) for i in b))
```
可以看到，在最后两行实现的，我先看了看vs code的官方解释</br>
![截屏2021-10-15 02 23 37](https://user-images.githubusercontent.com/74129445/137374379-60fb345d-5e28-4d9b-a8a5-d2bc0cb4e349.png)</br>
翻译为：</br>
连接任意数量的字符串，

调用其方法的字符串插入到每个给定元素之间，结果将作为新字符串返回。</br>


这也就是说，join的括号内的迭代对象只能是字符，如果是直接迭代列表里的数，则会报错  

```
a  = [1, 2, 3, 4]
print(''.join(i for i in a))

# File "/Users/ccf/Desktop/Python/test.py", line 2, in <module>
#     print(''.join(i for i in a))
# TypeError: sequence item 0: expected str instance, int found
```
其操作原理是join只能把迭代出的所有字符合成一个新字符，即在加入join之前，就应该把参数变为str类型

```
join 是首先遍历 list 中的每一个字符串确定 maxchar 通过 maxchar 和所有字符串的长度和 sz 通过 PyUnicode(sz,maxchar) 创建新的字符串对象 然后通过每一个字符串的长度和偏移将 list 字符串快速拷贝到新串中
```

参考：https://blog.csdn.net/weixin_42716570/article/details/113571129
