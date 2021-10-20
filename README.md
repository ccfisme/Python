# `*`+列表和`**`+字典操作的原理是不是指针？

今天做题时看答案，发现对于列表而言除了用join创建一个新的字符串的方式来去掉列表框，还有一种方式竟然是用是用`*`+列表直接输出  

不是听说python没有指针么？？？！！我又被骗了？？  

我翻了翻网上的回答，虽然令我欣慰的是大家都不认为这是指针，但我总感觉不妥，因为我并没有从python官网里找到对于`*`的解释，但这么多人都说不是指针，应该没错吧？  

后来又做到一个字典的题，是用`**`访问value  

？？？怎么越看越像指针  

于是，我准备从列表和字典的源码来探究其中的真相  

首先，我找了几个源代码网址，并最终锁定了[这里] https://flaggo.github.io/python3-source-code-analysis/objects/list-object/  

我看明白了，列表是类似于
