# `*`+列表和`**`+字典操作的原理是不是指针？

今天做题时看答案，发现对于列表而言除了用join创建一个新的字符串的方式来去掉列表框，还有一种方式竟然是用是用`*`+列表直接输出  

不是听说python没有指针么？？？！！我又被骗了？？  

我翻了翻网上的回答，虽然令我欣慰的是大家都不认为这是指针，但我总感觉不妥，因为我并没有从python官网里找到对于`*`的解释，但这么多人都说不是指针，应该没错吧？  

后来又做到一个字典的题，是用`**`访问value  

？？？怎么越看越像指针  

于是，我准备从列表和字典的源码来探究其中的真相  

## `*`+列表

首先，我找了几个源代码网址，并最终锁定了[这里]https://flaggo.github.io/python3-source-code-analysis/objects/list-object/  

我看明白了，列表是类似于寄存器寻址的一个结构，即列表结构体中用于找元素的指针是双重指针，要先找到用来存下标的数组，然后再找到数组中存的地址所指向的元素，看图更清晰  

![20200311174712810](https://user-images.githubusercontent.com/74129445/138089731-ae7e6ecb-4420-4835-987f-a3ceae1cf8d0.png)  

而列表实际是指针指向的结构体，即列表自带一个指针  

![截屏2021-10-20 20 09 57](https://user-images.githubusercontent.com/74129445/138090151-29856ddd-05b3-4923-8b53-992f650ab4a6.png)  

故使用列表时，可以用`*`+列表的形式来访问列表内部的值

## `**`+字典

同样，我也从上面网址看了字典，玛德字典竟然用到了哈希表，我都忘完了，于是又现学的哈希表，然后发现我依然看不懂python字典用的什么哈希函数（其实是不想看，因为已经预测到指针原理了，懒得学一遍哈希函数）  
但是大致原理我搞清楚了，先找key，找到key再通过key找value，这样也用到两个指针，并且我进行了实践  

```
实践1（证明* + 字典是访问的key）

dic1={"ONE" : 15264771766,"Kate" : 13063767486,"Rose" : 15146046882,"Chise" : 13606379542,"Jason" : 13611987725}
dic2={"ONE" : 15619397270,"TWO" : 15929494512,"THREE" : 13794876998,"FOUR" : 18890393268,"FIVE" : 13292597821}
dic3={**dic1}

print(dic3)

# 结果为{'ONE': 15264771766, 'Kate': 13063767486, 'Rose': 15146046882, 'Chise': 13606379542, 'Jason': 13611987725}



实践2（证明** + 字典访问value）

dic1={"ONE" : 15264771766,"Kate" : 13063767486,"Rose" : 15146046882,"Chise" : 13606379542,"Jason" : 13611987725}
dic2={"ONE" : 15619397270,"TWO" : 15929494512,"THREE" : 13794876998,"FOUR" : 18890393268,"FIVE" : 13292597821}
dic3={*dic1}

print(dic3)

#结果为{'Chise', 'Kate', 'Jason', 'Rose', 'ONE'}
```
吆西，全部印证了  

那么为什么同样要访问两次，字典要用两个`*`呢？  

根据之前列表的经验，我猜测是和字典的结构体有关  

```
其中，PyDictKeysObject 的定义如下；

源文件：Include/dict-common.h

// Objects/dict-common.h
/* See dictobject.c for actual layout of DictKeysObject */
struct _dictkeysobject {
    Py_ssize_t dk_refcnt;　　　　　　　　　　　　　　　　　　// 引用计数

    /* Size of the hash table (dk_indices). It must be a power of 2. */
    Py_ssize_t dk_size;　　　　　　　　　　　　　　　　　　　// hash table 的大小必须是２的倍数

    /* Function to lookup in the hash table (dk_indices):

       - lookdict(): general-purpose, and may return DKIX_ERROR if (and
         only if) a comparison raises an exception.

       - lookdict_unicode(): specialized to Unicode string keys, comparison of
         which can never raise an exception; that function can never return
         DKIX_ERROR.

       - lookdict_unicode_nodummy(): similar to lookdict_unicode() but further
         specialized for Unicode string keys that cannot be the <dummy> value.

       - lookdict_split(): Version of lookdict() for split tables. */
    dict_lookup_func dk_lookup;                       // 哈希查找函数

    /* Number of usable entries in dk_entries. */
    Py_ssize_t dk_usable;                             // 可用的entry数量

    /* Number of used entries in dk_entries. */　
    Py_ssize_t dk_nentries;　　　　　　　　　            // 已经使用的entry数量

    /* Actual hash table of dk_size entries. It holds indices in dk_entries,
       or DKIX_EMPTY(-1) or DKIX_DUMMY(-2).

       Indices must be: 0 <= indice < USABLE_FRACTION(dk_size).

       The size in bytes of an indice depends on dk_size:

       - 1 byte if dk_size <= 0xff (char*)
       - 2 bytes if dk_size <= 0xffff (int16_t*)
       - 4 bytes if dk_size <= 0xffffffff (int32_t*)
       - 8 bytes otherwise (int64_t*)

       Dynamically sized, SIZEOF_VOID_P is minimum. */
    char dk_indices[];  /* char is required to avoid strict aliasing. */　　　// 存入的entries

    /* "PyDictKeyEntry dk_entries[dk_usable];" array follows:
       see the DK_ENTRIES() macro */
};

```

果然，字典只是一个普通结构体，所以当访问字典的value时，就要用`**`进行访问










