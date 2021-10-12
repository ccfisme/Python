# 先存右边，然后对变量名从左往右赋值</br>
在python的一个练习题中，发现当并行赋值时，顺序并不像我想的那样由左至右赋值，如图</br>
![截屏2021-10-12 10 56 33](https://user-images.githubusercontent.com/74129445/136883750-497a28d6-06b5-49d9-8635-75573bb7e56b.png)</br>
我以为结果会是[1,3,3,4,5],但是出来的结果让我很疑惑，故我看了汇编</br>
![截屏2021-10-12 10 56 22](https://user-images.githubusercontent.com/74129445/136883717-0dfb1d1b-adae-4012-8358-d996fc6204b8.png)</br>
发现并行赋值时，先将值赋给左边地址，再将值赋给右边地址，我又查了资料</br>
参考：https://darktiantian.github.io/Python-%E5%A4%9A%E4%B8%AA%E5%8F%98%E9%87%8F%E5%90%8C%E6%97%B6%E8%B5%8B%E5%80%BC/</br>
发现确实是把变量先放栈里，然后对变量名从左往右赋值，但实现这种操作的源代码还需查找。</br>

---
---

## 将右侧作为一个元组按索引把地址赋值给左侧的变量

Python中变量保存的都是地址</br>

同时赋值的原理就是，等号右侧是一个元组</br>

而元组定义后都会在内存中创建一个空间，并且保存元组中各个元素的地址，Python中每一个类型数据都是对象，也都是地址。</br>

所以，当定义（a，b）元组后，实际上，内存中元组保存的元素是每个值a和b的地址</br>

而等号左侧之所以多个变量能得到值，是因为Python有一个独特的赋值方式，那就是会把等号右侧元组中值的地址，依次按索引把地址赋值给左侧的变量。</br>

即</br>
```
a, b = 3, 5
```
等价于</br>
```
tup = (3, 5)
a, b = tup
```
