在python里面input函数用于输入，但它接受一个输入数据，返回为 string 类型，所以一般需要强转来实现输入数据，如</br>
a = int(input())</br>
当然也会有一些错误，如</br>
![截屏2021-09-30 00 47 00](https://user-images.githubusercontent.com/74129445/135313220-1d8e7d8d-11ee-40d6-832c-f325528f00a6.png)
类型错误：int（）参数必须是字符串、对象或数字之类的字节，而不是“list”</br>
这也就限定了强转的类型，但为什么x, y = input().split()会是list，以及如何对列表的数据类型进行改动我就不懂了，于是就进行查找，找到了第一个问题的答案：split()函数运用指定的分隔符对字符串进行分割，返回一个列表，列表里面是分割好的子字符串。</br>
参考：https://blog.csdn.net/sinat_28576553/article/details/81150853</br>
那么，怎么对列表的字符串转型呢？这就用到了map函数，如map(int, input().split())就可以成功对一个列表强制性转换
