一直不明白print，感觉最简单的地方反而最麻烦，所以想记录一个详细的关于print函数用法的笔记</br>
首先是print函数的语法</br>
![截屏2021-10-07 17 09 58](https://user-images.githubusercontent.com/74129445/136355228-b4640c89-5cf7-424d-b791-3d306f2dda32.png)</br>
可以看到，当在print写入对象（即指针）时，会有个‘*’ 来指向此地址，所以可以直接访问对象</br>
print里的end = “”干什么用的？可以用来一行输出多组数据,默认是换行，end = “”表示直接衔接</br>
![截屏2021-10-11 22 36 48](https://user-images.githubusercontent.com/74129445/136810076-700e3573-231e-4d18-bcfe-f316070eec6e.png)
实际可以用来打印一些东西，如图形之类的</br>
![截屏2021-10-12 08 18 11](https://user-images.githubusercontent.com/74129445/136870094-e90187bb-ad75-4ac1-9c7f-98803d269fe9.png)
