一直不懂format是什么原理来输出浮点型数据，以及相对比与‘ % ’的优势，所以研究研究</br>
首先先搞懂‘ % ’的含义，才明白，这是占位符的意思，即预定饭店，然后后面预定饭店的人到了，就自动去那个地方，要做什么样式的菜，必须在预定的时候说清楚，即%.1f这样类似的控制语句</br>
参考：https://www.jb51.net/article/216508.html</br>
那么，format函数也就是来实现这个占位问题的了，如何实现的呢？以及为什么会比‘%’有优势呢？</br>
本来想总结一下，但是有篇文章总结的实在太好，所以我就简单说一下用法，就是可以用多种方式（如键值、字典等）进行传值。不多说了，以后我不会了就看这篇文章就行了</br>
参考：https://blog.csdn.net/lincoco49/article/details/89554005</br>
注意几个点，不知道原因就看上面文章：</br>
1.{}一定要用‘’引起来</br>
2.整数就不用在{}写变量了</br>
3.数与数之间用空格或者符号隔开</br>
![截屏2021-10-11 19 32 43](https://user-images.githubusercontent.com/74129445/136783652-698c9b79-c181-41cc-97a3-0797b57f5003.png)</br>
4.一定要在{}的:.后面写明数据类型，不写就按有效数字个数来输出</br>
![截屏2021-10-11 20 20 09](https://user-images.githubusercontent.com/74129445/136789116-45f664ba-8199-4ab7-8311-4c63a3dae456.png)
