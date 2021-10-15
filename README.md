## 使用方法：

在终端输入python -m dis test.py</br>
参考：https://blog.csdn.net/weixin_33888907/article/details/85835399</br>

## 探究

### dis解析

对反汇编的每个符号的意义有了新的兴趣,这种排列一定是有意义的，-m是什么？dis又是什么？所以我进行了查找，dis很好懂，就是一个输出过程函数，源代码如下：</br>
```
def dis(x=None, *, file=None):
    """Disassemble classes, methods, functions, generators, or code.
    With no argument, disassemble the last traceback.
    """
    if x is None:
        distb(file=file)
        return
    if hasattr(x, '__func__'):  # Method
        x = x.__func__
    if hasattr(x, '__code__'):  # Function
        x = x.__code__
    if hasattr(x, 'gi_code'):  # Generator
        x = x.gi_code
    if hasattr(x, '__dict__'):  # Class or module
        items = sorted(x.__dict__.items())
        for name, x1 in items:
            if isinstance(x1, _have_code):
                print("Disassembly of %s:" % name, file=file)
                try:
                    dis(x1, file=file)
                except TypeError as msg:
                    print("Sorry:", msg, file=file)
                print(file=file)
    elif hasattr(x, 'co_code'): # Code object
        disassemble(x, file=file)
    elif isinstance(x, (bytes, bytearray)): # Raw bytecode
        _disassemble_bytes(x, file=file)
    elif isinstance(x, str):    # Source code
        _disassemble_str(x, file=file)
    else:
        raise TypeError("don't know how to disassemble %s objects" %
                        type(x).__name__)

x参数可以是None、Method、Function、Generator、Class、module、Code object、Raw bytecode、Source code,如果x是Method、Function、Generator,只用返回对应的字节码,
如果x是Class或者module,那会返回x的所有元素(先排序)的字节码,这一句代码x.dict.items()有提现.如果x是Code object或者Raw bytecode,或者Source code,那么会调用对应的disassemble函数. disassemble函数是干嘛的呢,顾名思义,就是assemble的反义词, assemble是汇编的意思,那disassemble自然是有一个 反汇编 的意思,当然这里并不是真的反汇编,而是只是输出字节码.

disassemble的函数细节可以自己去看看源码,源码也在dis.py里


```
参考：https://www.jianshu.com/p/9553fa2c5c8b</br>

### -m解析

这个就没那么好懂了，涉及到许多东西，就我浏览完网页后的理解为，使用python命令编译时（注：是那种在终端写的命令），要先从环境变量找模块目录，而-m会把当前所在的路径传到环境变量，如果不写-m，直接python xxx.py，那样就会把文件所在目录传到环境变量。</br>

那么，这两种有什么区别呢？</br>

