
在写python的多组输入时，发现用while TRUE虽然能够实现，但会出现runtime error，原因是没有终止代码，但问题是python不能像c语言那样while(scanf()!=EOF),所以我就通过查找看到了用try...catch这个方法来终止代码，不过try究竟能捕获什么异常呢，其原理又是什么，如何打印出异常类型，这些是本文要了解的内容</br>
## try的所有异常
首先我找到了try能捕获的所有异常</br>

![FireShot Capture 031 - 在线翻译_有道 - fanyi youdao com](https://user-images.githubusercontent.com/74129445/136764389-02c379ed-83ce-4bab-9efa-db1d7e920041.png)</br>

不过说实话，由于没遇见过所有，因此这一步只能说是了解，那么try是如何捕获的异常呢？</br>
见：https://www.cnblogs.com/traditional/p/11869246.html 的11.4.2节</br>
发现其实是对每种类似返回值为NULL这种问题的函数设置了一个指针，然后作为异常返回，用if...else语句判断</br>
那么怎样发现异常呢？一般是要等PTA平台报错才知道，或者平时遇到一些可以记下来</br>

## 捕获异常
怎么知道是哪种异常呢？</br>
想要捕获所有的异常，可以直接捕获 Exception 即可：</br>
![截屏2021-10-11 18 48 39](https://user-images.githubusercontent.com/74129445/136778145-19ac017e-976f-4cd6-a61b-0c05ca07e55b.png)</br>
这个将会捕获除了 SystemExit 、 KeyboardInterrupt 和 GeneratorExit 之外的所有异常。 如果还想捕获这三个异常，将 Exception 改成 BaseException 即可。</br>

## break什么时候用

一开始以为所有都可以用，类似于多组输入这种：</br>
```
PI = 3.1415926
while True:
    try:
        a = float(input())
        b = (4 / 3) * a * a * a * PI
        print('{:.3f}'.format(b))
    except:
        break
```
后来发现只有在循环时才能够使用break，不然会报错</br>
![截屏2021-10-14 08 22 43](https://user-images.githubusercontent.com/74129445/137230294-b9db5a1e-eba6-4618-8213-cd5b86d2c06e.png)</br>
此译为非循环不可使用break

---

## 注意！！！一定注意，写except：break时，一定注意，try语句一定要在while语句之内写

‘’‘
while True:
    try:
        print("{}".format(sum(map(int, input().split()))))
    except:
        break
’‘’
