# is基于地址区分两个变量名是否指向同一个数，而“==”则是根据值来进行判断是否相等</br>
![截屏2021-10-12 22 09 27](https://user-images.githubusercontent.com/74129445/136972786-f53eca0d-ad5e-435d-8fe7-25697950bd18.png)</br>

但是，在做题当中遇到了浮点数与整数值相同的问题，即：</br>
```
x=2;y=2.0   #分号可把两个语句写在一行
if(x is 2):
   print("相等")
else:
   print("不相等")
```
其结果如下：</br>
```
ccf@Macbook Python % python -u "/Users/ccf/Desktop/Python/test.py"
不相等
```
为什么？？？？</br>

为什么计算机能够判断2与2.0的值是相同的呢？我感觉和python的编译器处理机制有关系，故进行查找，发现确实是这样</br>

![截屏2021-10-12 22 10 51](https://user-images.githubusercontent.com/74129445/136973286-ee9a695f-2fa6-4744-8c30-5b246d952e44.png)</br>


