
python中的一切都是对象。Python 将对象存储在堆内存中，并将对象的引用存储在堆栈中。变量、函数存储在堆栈中，对象存储在堆中。</br>

注意，堆中的对象永远存在，直到运行完程序操作系清除，或者做一个垃圾清除机制</br>

详见https://www.zhihu.com/answer/1924671529</br>

一个非常简单的解释是，堆是动态分配的内存所在的内存部分（即通过分配的内存malloc）。从堆分配的内存将保持分配状态，直到发生以下情况之一：</br>

记忆是free'd</br>
程序终止</br>
如果对已分配内存的所有引用都丢失了（例如，不再存储指向它的指针），就会出现所谓的内存泄漏。这是内存仍然被分配的地方，但是你再也没有简单的方法来访问它了。泄漏的内存不能被回收用于未来的内存分配，但是当程序结束时，操作系统会释放内存。</br>

将此与堆栈内存进行对比，堆栈内存是局部变量（在方法中定义的那些）所在的位置。分配在堆栈上的内存通常只在函数返回之前有效（有一些例外，例如静态局部变量）。</br>

所以，</br>

a = 10</br>

我理解为10是创造出的对象，而所有的名称（比如a）类似于C++的函数的引用，存储的是对象的地址，是指针常量，其中引用存储在堆栈中，也就是说，使用时把名称看成一个是指针常量的引用</br>

并且在python中当对变量重新赋值时，即</br>

a = 10</br>

a = 11</br>

这并不是说a存的不是固定的对象10的堆位置，不是指针常量了，而是重新定义了一个指针常量a，这个常量存的地址为对象11的堆位置</br>

即</br>

// 先定义对象10的</br>

int * const a = malloc(sizeof(int));</br>

python代码: a = 10</br>

//再定义对象11的</br>

int * const a = malloc(sizeof(int));</br>

python代码: a = 11</br>

这个例子同样可以解释为什么python变量的id函数总是不一样</br>

因为每次运行，都要重新分配堆内存，运行完后操作系统清空堆内存。</br>

解释python变量为指针常量的最佳例子就是format函数</br>


从这个函数可以看出，site确实是一个指针，访问这个量里的变量的地址需要用‘**’</br>
site = {"name": "ccf", "url": "123"}</br>
print("名字{name}, 地址 {url}".format(**site))</br></br></br>
---
---
#更正
现在发现对之前的对象的理解有误区，即对象代表的不是指针常量，也不是指针</br>

参考：https://yuyang0.github.io/notes/python-source-code.html</br>
下图为a的解释
</br>![截屏2021-09-29 16 24 31](https://user-images.githubusercontent.com/74129445/135231350-13b6ab5f-143e-4ba7-9747-ed0364e2f95b.png)</br>
python的a是个结构体，包含了两部分，一个是对象的引用的计数，一个是对象的类型和地址，也就是</br>
a = 1</br></br>
//对象引用计数</br>
int x = 0;</br>
//定义数据的类型和地址</br>
auto *a = 一个地址</br>
之所以不写malloc来代替“一个地址”的位置，是因为并不一定是malloc分配地址</br>
详见：https://blog.csdn.net/weixin_36019798/article/details/114400801</br>

