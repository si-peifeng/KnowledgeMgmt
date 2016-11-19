*args and **kwargs
==================

*args
-----
- 使用方式一
```python
def fun_var_args(farg, *args):
    print "arg:", farg
    for value in args:
        print "another arg:", value

fun_var_args(1, "two", 3) # *args可以当作可容纳多个变量组成的list
```

执行结果:
```
arg: 1
another arg: two
another arg: 3
```

- 使用方式二
```python
def fun_var_args_call(arg1, arg2, arg3):  
    print "arg1:", arg1  
    print "arg2:", arg2  
    print "arg3:", arg3  
  
args = ["two", 3] #list  
  
fun_var_args_call(1, *args)  
```

执行结果：
```
arg1: 1
arg2: two
arg3: 3
```

**kwargs
--------
- 使用方式一
```python
def fun_var_kwargs(farg, **kwargs):
    print "arg:", farg
    for key in kwargs:
        print "another keyword arg: %s: %s" % (key, kwargs[key])


fun_var_kwargs(farg=1, myarg2="two", myarg3=3) # myarg2和myarg3被视为key， **kwargs可以当作容纳多个key和value的dictionary
```

执行结果：
```
arg: 1
another keyword arg: myarg2: two
another keyword arg: myarg3: 3
```

- 使用方式二
```python
def fun_var_args_call(arg1, arg2, arg3):  
    print "arg1:", arg1  
    print "arg2:", arg2  
    print "arg3:", arg3  
  
kwargs = {"arg3": 3, "arg2": "two"} # dictionary  
  
fun_var_args_call(1, **kwargs)
```

执行结果：
```
arg1: 1
arg2:"two"
arg3:3
```

docopt
======
docopt根据你写的文档描述，可以自动为你生成解析器，可以非常容易的为你的python程序创建命令行界面

安装
----
```
pip install docopt==0.6.1
```

一个简单的例子
--------------
```python
"""Naval Fate.

Usage:
  naval_fate.py ship new <name>...
  naval_fate.py ship <name> move <x> <y> [--speed=<kn>]
  naval_fate.py ship shoot <x> <y>
  naval_fate.py mine (set|remove) <x> <y> [--moored | --drifting]
  naval_fate.py (-h | --help)
  naval_fate.py --version

Options:
  -h --help     Show this screen.
  --version     Show version.
  --speed=<kn>  Speed in knots [default: 10].
  --moored      Moored (anchored) mine.
  --drifting    Drifting mine.

"""
from docopt import docopt

if __name__ == '__main__':
    arguments = docopt(__doc__, version='Naval Fate 2.0')
    print(arguments)
```

naval_fate.py ship Guardian move 100 150 --speed=15
```
{'--drifting': False,    'mine': False,
 '--help': False,        'move': True,
 '--moored': False,      'new': False,
 '--speed': '15',        'remove': False,
 '--version': False,     'set': False,
 '<name>': ['Guardian'], 'ship': True,
 '<x>': '100',           'shoot': False,
 '<y>': '150'}
 ```
 
 if-else 的多种写法
 ==================
- 常规
```python
if a>b:
    c = a
else:
    c = b
```
- 表达式
```python
c = a if a>b else b
```
- 二维列表
```python
c = [b,a][a>b]
```
- 传说是源自某个黑客
```python
c = (a>b and [a] or [b])[0]
```

virtualenv
==========
- 安装
```
pip install virtualenv
```

- 创建虚拟环境
```
root@kali:/recall/code# virtualenv test_env
New python executable in test_env/bin/python
Installing setuptools, pip...done.
root@kali:/recall/code# 
```

默认情况下，虚拟环境会依赖系统环境中的site packages，就是说系统中已经安装好的第三方package也会安装在虚拟环境中，

如果不想依赖这些package，那么可以加上参数 

```
--no-site-packages　
```
建立虚拟环境

即变成了：
```
root@kali:/recall/code# virtualenv test_env --no-site-packages
New python executable in test_env/bin/python
Installing setuptools, pip...done.
root@kali:/recall/code# 
```

- 启动虚拟环境
创建成功后，会在当前目录下生成对应的目录文件。

```
root@kali:/recall/code# ls -l test_env/
总用量 16
drwxr-xr-x 2 root root 4096  4月 29 20:03 bin
drwxr-xr-x 2 root root 4096  4月 29 19:58 include
drwxr-xr-x 3 root root 4096  4月 29 19:58 lib
drwxr-xr-x 2 root root 4096  4月 29 19:58 local
root@kali:/recall/code# 
```

我们先进入到该目录下：
```
cd test_env/
```
然后启动
```
root@kali:/recall/code/test_env# source ./bin/activate
```
启动成功后，会在前面多出 test_env 字样，如下所示
```
(test_env)root@kali:/recall/code/test_env# 
```

- 使用测试
```
(test_env)root@kali:/recall/code/test_env# pip install requests
Downloading/unpacking requests
  Downloading requests-2.2.1-py2.py3-none-any.whl (625kB): 625kB downloaded
Installing collected packages: requests
Successfully installed requests
Cleaning up...
(test_env)root@kali:/recall/code/test_env# python
Python 2.7.3 (default, Jan  2 2013, 13:56:14) 
[GCC 4.7.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> 
>>> response = requests.get("http://www.baidu.com")
>>> response.status_code
>>>
```

-退出虚拟环境
```
deactivate
```

requirements.txt
================
python项目中包含一个 requirements.txt文件，用于记录所有依赖包及其精确的版本号，以便新环境部署。

- 导出依赖
```
pip freeze >requirements.txt
```
文件的内容类似
```
CherryPy==4.0.0
MySQL-python==1.2.3
Paste==2.0.2
PasteDeploy==1.5.2
PasteScript==2.0.2
SQLAlchemy==0.8.4
```

- 安装依赖
```
pip install -r requirements.txt
```

最简单web server
================
python -m SimpleHTTPServer 80

r'string'
========
在python的string前面加上‘r’， 是为了告诉编译器这个string是个raw string，不要转意backslash '\' 。 例如，\n 在raw string中，是两个字符，\和n， 而不会转意为换行符。由于正则表达式和 \ 会有冲突，因此，当一个字符串使用了正则表达式后，最好在前面加上'r'。
```python
>>> print 'it\'s good'
it's good
>>> print r'it\'s good'
it\'s good
```


glob
====
用它可以查找符合特定规则的文件路径名。查找文件只用到三个匹配符：”*”, “?”, “[]”。”*”匹配0个或多个字符；”?”匹配单个字符；”[]”匹配指定范围内的字符，如：[0-9]匹配数字。

- glob.glob

返回所有匹配的文件路径列表。它只有一个参数pathname，定义了文件路径匹配规则，这里可以是绝对路径，也可以是相对路径。下面是使用glob.glob的例子：
```
import glob

#获取指定目录下的所有图片
print glob.glob(r"E:/Picture/*/*.jpg")

#获取上级目录的所有.py文件
print glob.glob(r'../*.py') #相对路径
```

- glob.iglob

获取一个可编历对象，使用它可以逐个获取匹配的文件路径名。与glob.glob()的区别是：glob.glob同时获取所有的匹配路径，而glob.iglob一次只获取一个匹配路径。
```
import glob

#父目录中的.py文件
f = glob.iglob(r'../*.py')

print f #<generator object iglob at 0x00B9FF80>

for py in f:
    print py
```

struct
======
该模块的主要作用就是对python基本类型值与用python字符串格式表示的C struct类型间的转化。
- 基本的pack和unpack

struct提供用format specifier方式对数据进行打包和解包（Packing and Unpacking）。例如:
```python
import struct
import binascii
values = (1, 'abc', 2.7)
s = struct.Struct('I3sf')
packed_data = s.pack(*values)
unpacked_data = s.unpack(packed_data)
 
print 'Original values:', values
print 'Format string :', s.format
print 'Uses :', s.size, 'bytes'
print 'Packed Value :', binascii.hexlify(packed_data)
print 'Unpacked Type :', type(unpacked_data), ' Value:', unpacked_data
```
输出：
```
Original values: (1, 'abc', 2.7) 
Format string : I3sf 
Uses : 12 bytes 
Packed Value : 0100000061626300cdcc2c40 
Unpacked Type : <type 'tuple'>  Value: (1, 'abc', 2.700000047683716)
```
代码中，首先定义了一个元组数据，包含int、string、float三种数据类型，然后定义了struct对象，并制定了format‘I3sf’，I 表示int，3s表示三个字符长度的字符串，f 表示 float。最后通过struct的pack和unpack进行打包和解包。通过输出结果可以发现，value被pack之后，转化为了一段二进制字节串，而unpack可以把该字节串再转换回一个元组，但是值得注意的是对于float的精度发生了改变，这是由一些比如操作系统等客观因素所决定的。打包之后的数据所占用的字节数与C语言中的struct十分相似。定义format可以参照官方api提供的对照表：
![image](c:\201112171613441943.png)

- 字节顺序

另一方面，打包的后的字节顺序默认上是由操作系统的决定的，当然struct模块也提供了自定义字节顺序的功能，可以指定大端存储、小端存储等特定的字节顺序，对于底层通信的字节顺序是十分重要的，不同的字节顺序和存储方式也会导致字节大小的不同。在format字符串前面加上特定的符号即可以表示不同的字节顺序存储方式，例如采用网络端存储 s = struct.Struct('!I3sf')就可以了。官方也提供了相应的对照列表:

![image](F:\222.png)

- 利用buffer，使用pack_into和unpack_from方法

使用二进制打包数据的场景大部分都是对性能要求比较高的使用环境。而在上面提到的pack方法都是对输入数据进行操作后重新创建了一个内存空间用于返回，也就是说我们每次pack都会在内存中分配出相应的内存资源，这有时是一种很大的性能浪费。struct模块还提供了pack_into() 和 unpack_from()的方法用来解决这样的问题，也就是对一个已经提前分配好的buffer进行字节的填充，而不会每次都产生一个新对象对字节进行存储。
```python
import struct
import binascii
import ctypes
 
values = (1, 'abc', 2.7)
s = struct.Struct('I3sf')
prebuffer = ctypes.create_string_buffer(s.size)
print 'Before :',binascii.hexlify(prebuffer)
s.pack_into(prebuffer,0,*values)
print 'After pack:',binascii.hexlify(prebuffer)
unpacked = s.unpack_from(prebuffer,0)
print 'After unpack:',unpacked
```
输出：
```
Before : 000000000000000000000000 
After pack: 0100000061626300cdcc2c40 
After unpack: (1, 'abc', 2.700000047683716) 
```

对比使用pack方法打包，pack_into 方法一直是在对prebuffer对象进行操作，没有产生多余的内存浪费。另外需要注意的一点是，pack_into和unpack_from方法均是对string buffer对象进行操作，并提供了offset参数，用户可以通过指定相应的offset，使相应的处理变得更加灵活。例如，我们可以把多个对象pack到一个buffer里面，然后通过指定不同的offset进行unpack：
```python
import struct
import binascii
import ctypes
 
values1 = (1, 'abc', 2.7)
values2 = ('defg',101)
s1 = struct.Struct('I3sf')
s2 = struct.Struct('4sI')
 
prebuffer = ctypes.create_string_buffer(s1.size+s2.size)
print 'Before :',binascii.hexlify(prebuffer)
s1.pack_into(prebuffer,0,*values1)
s2.pack_into(prebuffer,s1.size,*values2)
print 'After pack:',binascii.hexlify(prebuffer)
print s1.unpack_from(prebuffer,0)
print s2.unpack_from(prebuffer,s1.size)
```
输出：
```
Before : 0000000000000000000000000000000000000000 
After pack: 0100000061626300cdcc2c406465666765000000 
(1, 'abc', 2.700000047683716) 
('defg', 101)
```

collections
===========

multiprocessing
===============
> from multiprocessing.dummy import Pool as ThreadPool 
多线程进程池，绑定一个cpu核心
from multiprocessing import Pool 
多进程，运行于多个cpu核心


multiprocessing.dummy
---------------------
> Python中线程multiprocessing模块与进程使用的同一模块。使用方法也基本相同，唯一不同的是，from multiprocessing import Pool这样导入的Pool表示的是进程池； 
from multiprocessing.dummy import Pool这样导入的Pool表示的是线程池。这样就可以实现线程里面的并发了。

```python
import time
from multiprocessing.dummy import Pool as ThreadPool
#给线程池取一个别名ThreadPool
def run(fn):
  time.sleep(2)
  print fn

if __name__ == '__main__':
  testFL = [1,2,3,4,5]
  pool = ThreadPool(10)#创建10个容量的线程池并发执行
  pool.map(run, testFL)
  pool.close()
  pool.join()
```
执行结果
```
53412
```
这里的pool.map()函数，跟进程池的map函数用法一样，也跟内建的map函数一样。

```python
# -*- coding: utf-8 -*-
# from multiprocessing import Pool 多进程
from multiprocessing.dummy import Pool as ThreadPool #多线程
import time
import urllib2

urls = [
    'http://www.baidu.com/',
    'http://www.163.com/',
    'http://www.sohu.com/',
    'http://www.csdn.net/',
    'http://www.qq.com/',
    'http://www.taobao.com/',
    'http://www.jd.com/'
    ]

# 单线程
start = time.time()
results = map(urllib2.urlopen, urls)
print 'Normal:', time.time() - start

# 多线程
start2 = time.time()
# 开4个 worker，没有参数时默认是 cpu 的核心数
pool = ThreadPool(4)
# 在线程中执行 urllib2.urlopen(url) 并返回执行结果
results2 = pool.map(urllib2.urlopen, urls)
pool.close()
pool.join()
print 'Thread Pool:', time.time() - start2

```
执行结果
```
Normal: 0.381999969482
Thread Pool: 0.106000185013
```

Queue
=====

subprocess
==========

threading
=========
> threading.Thread
Thread是threading模块中最重要的类之一，可以使用它来创建线程。创建新的线程有两种方法：

- 方法一：直接创建threading.Thread类的对象，初始化时将可调用对象作为参数传入。

- 方法二：通过继承Thread类，重写它的run方法。

> Thread类拥有的实例方法：

- isAlive()：返回线程是否在运行。正在运行指的是启动后，终止前。

- getName(name)/setName(name)：获取/设置线程名。

- isDaemon(bool)/setDaemon(bool)：获取/设置是否为守护线程。初始值从创建该线程的线程继承而来，当没有非守护线程仍在运行时，程序将终止。

- start()：启动线程。

- join([timeout])：阻塞当前上下文环境的线程，直到调用此方法的线程终止或到达指定的等待时间timeout（可选参数）。即当前的线程要等调用join()这个方法的线程执行完，或者是达到规定的时间。

> 直接创建threading.Thread类的对象

```python
#　-*- coding: utf-8 -*-
from threading import Thread
import time
def run(a = None, b = None) :
  print a, b
  time.sleep(5)

# __init__(group=None, target=None, name=None, args=(), kwargs=None, verbose=None)
t = Thread(target = run, args = ("this is a", "thread"))
#此时线程是新建状态

print t.getName()   #获得线程对象名称
print t.isAlive()   #判断线程是否还活着。
t.start()           #启动线程
t.join()            #等待其他线程运行结束
```
执行结果
```
Thread-1
False
this is a thread
```

> 通过继承Thread类

```python
from threading import Thread
import time

class MyThread(Thread) :
  def __init__(self, a) :
    super(MyThread, self).__init__()
    #调用父类的构造方法
    self.a = a

  def run(self) :
    print "sleep :", self.a
    time.sleep(self.a)

t1 = MyThread(2)
t2 = MyThread(4)
t1.start()
t2.start()
t1.join()
t2.join()
```
执行结果
```
sleep : 2
sleep : 4
```

sched
=====

pycharm快捷键
=============
跳出双引号：shift + "

跳出单引号：'

跳出括号：shift + )

跳出中括号：]

自动关闭 ctrl + shift + enter

不关闭，跳到下一行 shift + enter


map()函数
=========
> map(function, iterable, ...)

- 对可迭代函数'iterable'中的每一个元素应用‘function’方法，将结果作为list返回。
```
>>> def add100(x):
...     return x+100
... 
>>> hh = [11,22,33]
>>> map(add100,hh)
[111, 122, 133]
```

- 如果给出了额外的可迭代参数，则对每个可迭代参数中的元素‘并行’的应用‘function’。
```python
>>> def abc(a, b, c):
...     return a*10000 + b*100 + c
... 
>>> list1 = [11,22,33]
>>> list2 = [44,55,66]
>>> list3 = [77,88,99]
>>> map(abc,list1,list2,list3)
[114477, 225588, 336699]
```

- 如果'function'给出的是‘None’，自动假定一个‘identity’函数。
```python
>>> list1 = [11,22,33]
>>> map(None,list1)
[11, 22, 33]
>>> list1 = [11,22,33]
>>> list2 = [44,55,66]
>>> list3 = [77,88,99]
>>> map(None,list1,list2,list3)
[(11, 44, 77), (22, 55, 88), (33, 66, 99)]
```

python 线程，GIL 和 ctypes
==========================
GIL 与 Python 线程的纠葛
------------------------
GIL 是什么东西？它对我们的python程序会产生什么样的影响？我们先来看一个问题。运行下面这段 python 程序，CPU 占用率是多少？

```python
def dead_loop():
    while True:
        pass

dead_loop() 
```

答案是什么呢，占用 100％ CPU？那是单核！还得是没有超线程的古董 CPU。在我的双核 CPU 上，这个死循环只会吃掉我一个核的工作负荷，也就是只占用50％CPU。那如何能让它在双核机器上占用 100％ 的 CPU 呢？答案很容易想到，用两个线程就行了，线程不正是并发分享 CPU 运算资源的吗。可惜答案虽然对了，但做起来可没那么简单。下面的程序在主线程之外又起了一个死循环的线程
```python
import threading

def dead_loop():
    while True:
        pass

#新起一个死循环线程
t = threading.Thread(target=dead_loop) t.start()
#主线程也进入死循环
dead_loop()
t.join()
```
按道理它应该能做到占用两个核的 CPU资源，可是实际运行情况却是没有什么改变，还是只占了 50％ CPU 不到。这又是为什么呢？难道 python 线程不是操作系统的原生线程？打开 system monitor 一探究竟，这个占了50%的python进程确实是有两个线程在跑。那这两个死循环的线程为何不能占满双核 CPU 资源呢？其实幕后的黑手就是 GIL。

GIL 的迷思：痛并快乐着
----------------------
GIL 的全程为 Global Interpreter Lock ，意即全局解释器锁。在 Python 语言的主流实现 CPython 中，GIL 是一个货真价实的全局线程锁，在解释器解释执行任何Python代码时，都需要先获得这把锁才行，在遇到 I/O 操作时会释放这把锁。如果是纯计算的程序，没有 I/O 操作，解释器会每隔 100 次操作就释放这把锁，让别的线程有机会执行（这个次数可以通过 sys.setcheckinterval 来调整）。所以虽然CPython的线程库直接封装操作系统的原生线程，但 CPython 进程做为一个整体，同一时间只会有一个获得了GIL的线程在跑，其它的线程都处于等待状态等着 GIL 的释放。这也就解释了我们上面的实验结果：虽然有两个死循环的线程，而且有两个物理 CPU 内核，但因为 GIL 的限制，两个线程只是做着分时切换，总的 CPU 占用率还略低于 50％。


看起来 python 很不给力啊。GIL直接导致CPython不能利用物理多核的性能加速运算。那为什么会有这样的设计呢？我猜想应该还是历史遗留问题。多核 CPU 在1990年代还属于类科幻，Guido van Rossum 在创造 python 的时候，也想不到他的语言有一天会被用到很可能 1000＋ 个核的 CPU 上面，一个全局锁搞定多线程安全在那个时代应该是最简单经济的设计了。简单而又能满足需求，那就是合适的设计（对设计来说，应该只有合适与否，而没有好与不好）。怪只怪硬件的发展实在太快了，摩尔定律给软件业的红利这么快就要到头了。短短20年不到，代码工人就不能指望仅仅靠升级 CPU 就能让老软件跑的更快了。在多核时代，编程的免费午餐没有了。如果程序不能用并发挤干每个核的运算性能，那就意谓着会被淘汰。对软件如此，对语言也是一样。那 Python 的对策呢？

Python 的应对很简单，以不变应万变。在最新的python3中依然有GIL。之所以不去掉，原因嘛，不外以下几点：

- 欲练神功，挥刀自宫：

CPython 的 GIL 本意是用来保护所有全局的解释器和环境状态变量的。如果去掉GIL，就需要多个更细粒度的锁对解释器的众多全局状态进行保护。或者采用Lock-Free算法。无论哪一种，要做到多线程安全都会比单使用 GIL 一个锁要难的多。而且改动的对象还是有 20 年历史的 CPython 代码树，更不论有这么多第三方的扩展也在依赖GIL。对Python社区来说，这不异于挥刀自宫，重新来过。

- 就算自宫，也未必成功：

有位牛人曾经做了一个验证用的CPython，将GIL去掉，加入了更多的细粒度锁。但是经过实际的测试，对单线程程序来说，这个版本有很大的性能下降，只有在利用的物理CPU超过一定数目后，才会比 GIL 版本的性能好。这也难怪。单线程本来就不需要什么锁。单就锁管理本身来说，锁 GIL 这个粗粒度的锁肯定比管理众多细粒度的锁要快的多。而现在绝大部分的 python 程序都是单线程的。再者，从需求来说，使用python绝不是因为看中它的运算性能。就算能利用多核，它的性能也不可能和C/C++比肩。费了大力气把GIL拿掉，反而让大部分的程序都变慢了，这不是南辕北辙吗。


难道 Python 这么优秀的语言真的仅仅因为改动困难和意义不大就放弃多核时代了吗？其实，不做改动最最重要的原因还在于：不用自宫，也一样能成功！

- 其它神功

那除了切掉 GIL 外，果然还有方法让Python在多核时代活的滋润？让我们回到本文最初的那个问题：如何能让这个死循环的Python脚本在双核机器上占用100％的CPU？其实最简单的答案应该是：运行两个 python 死循环的程序！也就是说，用两个分别占满一个 CPU 内核的 python 进程来做到。确实，多进程也是利用多个CPU的好方法。只是进程间内存地址空间独立，互相协同通信要比多线程麻烦很多。有感于此，Python 在 2.6 里新引入了 multiprocessing 这个多进程标准库，让多进程的 python 程序编写简化到类似多线程的程度，大大减轻了 GIL 带来的不能利用多核的尴尬。

这还只是一个方法，如果不想用多进程这样重量级的解决方案，还有个更彻底的方案，放弃 Python，改用 C/C++。当然，你也不用做的这么绝，只需要把关键部分用 C/C++ 写成 Python 扩展，其它部分还是用 Python来写，让Python的归Python，C的归C。一般计算密集性的程序都会用 C 代码编写并通过扩展的方式集成到Python脚本里（如NumPy模块）。在扩展里就完全可以用 C 创建原生线程，而且不用锁 GIL，充分利用 CPU 的计算资源了。不过，写 Python 扩展总是让人觉得很复杂。好在 Python 还有另一种与 C 模块进行互通的机制 : ctypes

- 利用 ctypes 绕过 GIL

ctypes 与 Python 扩展不同，它可以让 Python 直接调用任意的 C 动态库的导出函数。你所要做的只是用 ctypes 写些 python 代码即可。最酷的是，ctypes 会在调用 C 函数前释放 GIL。所以，我们可以通过 ctypes 和 C 动态库来让 python 充分利用物理内核的计算能力。让我们来实际验证一下，这次我们用 C 写一个死循环函数

```
extern"C" {
    void DeadLoop() {
        while (true); 
    } 
} 
```
用上面的 C 代码编译生成动态库 libdead_loop.so （Windows 上是 dead_loop.dll）
，接着就要利用 ctypes 来在python里load这个动态库，分别在主线程和新建线程里调用其中的 DeadLoop
```python
from ctypes import * 
from threading import Thread

lib = cdll.LoadLibrary("libdead_loop.so") 
t = Thread(target=lib.DeadLoop) 
t.start()
lib.DeadLoop() 
```

这回再看看 system monitor，Python 解释器进程有两个线程在跑，而且双核 CPU 全被占满了，ctypes 确实很给力！需要提醒的是，GIL 是被ctypes在调用C函数前释放的。但是 Python 解释器还是会在执行任意一段 Python 代码时锁 GIL 的。如果你使用Python的代码做为 C 函数的 callback，那么只要Python的callback方法被执行时，GIL还是会跳出来的。比如下面的例子：

```
extern"C" {
    typedef void Callback(); 
    void Call(Callback callback) { 
        callback(); 
    } 
} 
```
```python
from ctypes import *
from threading import Thread

def dead_loop(): 
    while True: 
        pass

lib = cdll.LoadLibrary("libcall.so") 
Callback = CFUNCTYPE(None) 
callback = Callback(dead_loop)

t = Thread(target=lib.Call, args=(callback,)) 
t.start()

lib.Call(callback) 
```

注意这里与上个例子的不同之处，这次的死循环是发生在 Python 代码里 (DeadLoop 函数) 而 C 代码只是负责去调用这个 callback 而已。运行这个例子，你会发现 CPU 占用率还是只有 50％ 不到。GIL 又起作用了。

其实，从上面的例子，我们还能看出ctypes的一个应用，那就是用Python写自动化测试用例，通过 ctypes 直接调用 C 模块的接口来对这个模块进行黑盒测试，哪怕是有关该模块C接口的多线程安全方面的测试，ctypes 也一样能做到。

- 结语

虽然 CPython 的线程库封装了操作系统的原生线程，但却因为GIL的存在导致多线程不能利用多个 CPU 内核的计算能力。好在现在 Python 有了易经筋（multiprocessing）, 吸星大法（C 语言扩展机制）和独孤九剑（ctypes），足以应付多核时代的挑战，GIL切还是不切已经不重要了，不是吗。
