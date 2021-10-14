# for循环可以在列表直接操作

在PTA碰到了一个题</br>
```
你的任务是计算一些整数的和。

输入格式:
输入包含多个测试用例。

每个测试用例包含一个整数N，然后在同一行中跟随N个整数。以0开始的测试用例终止输入，并且这个测试用例不被处理。

输出格式:
对于每一组输入整数，您应该在一行中输出它们的和，输入的每一行都有一行输出。

输入样例:
在这里给出一组输入。例如：

4 1 2 3 4
5 1 2 3 4 5
0
输出样例:
在这里给出相应的输出。例如：

10
15
```
一开始，我想的是先把一组数直接累加，再减个开头就行了，可实现时就犯了难，因为要输入肯定先输入一组数存到map里，可又怎么将它们累加呢？</br>

```
sum的使用语法 sum(iterable[, start]) iterable -- 可迭代对象,如:列表、元组、集合
```
故我想的是把map化成list，然后用个sum函数</br>
```
a = list(map(int, input().split()))
b = sum(a)
print(b - a[0])
```

可我又想实现一下sum函数，故想写个for循环，那么怎么实现map内部数字的累加呢？先求出列表，再找到a[0],知道累加次数，然后累加全部再减a[0]....</br>

太麻烦了，后来经过查找发现原来for可以用in直接遍历列表，于是就写出了实现sum的代码</br>

```
a = list(map(int, input().split()))
b = 0
for i in a:
    b += i
print(b - a[0])
```
