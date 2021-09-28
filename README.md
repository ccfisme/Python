在学习python的过程中遇到与python列表的存储方式有关的问题，先上代码</br>
代码：</br>
![截屏2021-09-28 08 41 56](https://user-images.githubusercontent.com/74129445/135003996-49df9de8-d5e3-4ca7-a378-124dc8d8de46.png)</br>

运行后：</br>
![截屏2021-09-28 08 42 06](https://user-images.githubusercontent.com/74129445/135004003-00510d63-4040-446b-acd0-a8b6bcae7782.png)</br>
正如问题所描述的，为什么列表不会区分两个数组中含有的两个地址是相同的，其实这个问题很沙雕，就如同c++中问为什么两个数组合并会有相同的数一样，即

![截屏2021-09-28 08 50 33](https://user-images.githubusercontent.com/74129445/135004515-65eeef35-bd8c-432a-9ac5-05041d55754e.png)</br>
![截屏2021-09-28 08 50 39](https://user-images.githubusercontent.com/74129445/135004520-ca1d1e8b-c5e4-4e93-ab99-2858144efd8c.png)</br>

其实c++的数组存数的机制也是这样，存每个数的地址，且每个数组单元之间并无关系，虽然c++相同数的地址肯定不一样，和python不同，但是在这里只是为了说明两两数据单元之间并无关系，为什么说这个呢，因为这与python的存储机制有关系。</br>

参考：https://blog.csdn.net/u014029783/article/details/107992840</br>
可以从此文发现，python的存储机制就是把python数的指针存到一个数组里，类似于c++数组的合并，其数组元素都是指针。
