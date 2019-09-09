

# python随笔



## 字符串相关处理



### find（）函数

- Python find() 方法检测字符串中是否包含子字符串 str ，如果指定 beg（开始） 和 end（结束） 范围，则检查是否包含在指定范围内，如果包含子字符串返回开始的索引值，否则返回-1。

```python
#!/usr/bin/python
str1 = "this is string example....wow!!!";
str2 = "exam";
print str1.find(str2);
print str1.find(str2, 10);
print str1.find(str2, 40);
```



### format()函数

- print('{参数:数据类型}'.format(输出数据))

- print('{参数0:数据类型}{参数1:数据类型}{参数2:数据类型}'.format(输出数据0，输出数据1，输出数据2))



### split()字符串拆分函数

- split('参数'，次数)以参数为准，拆分字符串n次，为n+1个子字符串.无参数默认以空白(包括转义字符)分割。



### join()函数

- 将列表的子字符串组合成一个字符串

- str.join(列表)将用字符串str在子字符串之间进行组合

- join可以对字符串操作



### startswith()函数

```python
str.startswith(substr[,start=0,end=0])
```

用于检测字符串是否以子字符串开头。同理endswith(),可设置开始和起始位置。



### replace()函数

- replace(string1,string2)

- 用string2取代字符串中的子字符串string1



### eval()函数

- 可以执行字符串里的表达式。

```python
test=eval('3+5')

print(test)

>>>8
```

- 去掉字符串引号



## 列表相关处理

### sorted()函数

#### key关键字

- sorted(iterable[, key,reverse])

  从 iterable 中的项目返回新的排序列表。

  有两个可选参数，必须指定为关键字参数。

  key 指定一个参数的函数，用于从每个列表元素中提取比较键：key=str.lower。默认值为 None （直接比较元素）。

  reverse 是一个布尔值。如果设置为 True，那么列表元素将按照每个比较反转进行排序

  ```python
  示例：创建由元组构成的列表：a = [('b',3), ('a',2), ('d',4), ('c',1)]
  
  按照第一个元素排序
            sorted(a, key=lambda x:x[0])  
  
            >>> [('a',2),('b',3),('c',1),('d',4)]
  
  按照第二个元素排序
            sorted(a, key=lambda x:x[1]) 
  
            >>> [('c',1),('a',2),('b',3),('d',4)]
  
  ```


- sorted()排序，不改变原有数据容器。关键字参数key，被赋予一个索引值，决定排序基准。reverse参数控制升序降序。



#### 匿名函数

- lambda为匿名函数，运行时返回一个表达式。例子中的x为唯一参数，x[3]为返回值。

```python
from operator import itemgetter

sorted(列表名，key=itemgetter(3，0))
#先按照索引值3排序，再按照0排序。
```



字典:用keys，values，items获得相应列表再进行操作。

### sort（）函数

- sorted（）临时性排序

- sort（）永久排序

用法：列表名.sort()



### range()函数

- 常用于创建整数列表

- range(起点，终点，步长)步长默认为1，列表不包含终点



### 切片

- [起始索引:终止索引]应用于列表

- 到终止索引为止不包含终止索引



### map()函数

- 例如：map(str，list)将列表list中的所有数据类型全部转换为string，即全部元素使用str()方法



## 字典相关处理

### copy()

- 复制字典



### 键值对添加

```python
dictionary[key]=value
```



## 基本数学函数

### count()

- count(参数)，统计参数在列表中的出现次数

## 迭代

### iter（）

而迭代器是指，你能用 `next` 函数不断的去获取它的下一个值，直到迭代器返回 `StopIteration`异常。所有的可迭代对象都可以通过 `iter` 函数去获取它的迭代器，比如上面的 `letters` 是一个可迭代对象，那么这样去迭代它

```python
>>> letters = ['a', 'b', 'c']
>>> it = iter(letters)
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

所有的迭代器其实都实现了 `__iter__` 和 `__next__` 这俩个魔法方法，`iter` 与 `next` 函数实际上调用的是这两个魔法方法，上面的例子背后其实是这样的：

```python
>>> letters = ['a', 'b', 'c']
>>> it = letters.__iter__()
>>> it.__next__()
'a'
>>> it.__next__()
'b'
>>> it.__next__()
'c'
>>> it.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

迭代器的另一种实现方式，`__iter__` + `__next__`：

```python
>>> class Test:
...     def __init__(self, a, b):
...         self.a = a
...         self.b = b
...     def __iter__(self):
...         return self
...     def __next__(self):
...         self.a += 1
...         if self.a > self.b:
...             raise StopIteration()
...         return self.a
... 
>>> test = Test(0, 5)   # Test 类的实例就是迭代器
>>> next(test)
1
>>> next(test)
2
>>>
```

### for循环else

- else语句可以对应的是for，不是if，这个是python特有的语句。
- 即在for 循环中，如果没有从任何一个break中退出，则会执行和for对应的else
- 只要从break中退出了，则else部分不执行。

## 生成器

### yield

yield` 的使用方法和 `return` 类似。不同的是，`return` 可以返回有效的 Python 对象，而 `yield` 返回的是一个生成器，函数碰到 `return` 就直接返回了，而使用了 `yield` 的函数，到 `yield` 返回一个元素，当再次迭代生成器时，会从 `yield` 后面继续执行，直到遇到下一个 `yield` 或者函数结束退出。

```python
>>> def fib(n):
...     current = 0
...     a, b = 1, 1
...     while current < n:
...         yield a
...         a, b = b, a + b
...         current += 1
```

### zip()

```python
>>> g = (x**x for x in range(1, 4),y for y in range(0,3))
  File "<stdin>", line 1
    g = (x**x for x in range(1, 4),y for y in range(0,3))
                                  ^
SyntaxError: invalid syntax
>>> g = (x**x for x in range(1, 4))
>>> h = (y for y in range(0,3))
>>> k = [(m,n) for m,n in g,h]
  File "<stdin>", line 1
    k = [(m,n) for m,n in g,h]
                           ^
SyntaxError: invalid syntax
>>> k = zip(g,h)
>>> k
<zip object at 0x7f6e97e6eec8>
>>> print(list(k))
[(1, 0), (4, 1), (27, 2)]
>>> l = ((m,n) for m,n in k)
>>> l
<generator object <genexpr> at 0x7f6e9639d7c8>

```

## 装饰器

### 语法糖

@* 是 Python 提供的语法糖，语法糖指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。

```python
>>> from datetime import datetime
>>> def log(func):
...     def decorator(*args, **kwargs):
...         print('Function ' + func.__name__ + ' has been called at ' + datetime.now().strftime('%Y-%m-%d %H:%M:%S'))
...         return func(*args, **kwargs)
...     return decorator
...
>>> @log
... def add(x, y):
...     return x + y
...
>>> add(1, 2)
Function add has been called at 2017-08-29 13:11:48
3
```

也就是说，调用了 `log` 函数，把 `add` 函数作为参数，传了进去。`log` 函数返回了另外一个函数 `decorator` ，在这个函数中，首先打印了日志信息，然后回调了传入的 `func` ，也就是 `add` 函数。

你可能已经发现了，执行完 `add = log(add)` ，或者说用 `@log` 装饰 `add` 后，`add` 其实已经不再是原来的 `add` 函数了，它已经变成了`log` 函数返回的 `decorator` 函数：

```python
>>> add.__name__
'decorator'
```

这也是装饰器带来的副作用，Python 提供了方法解决这个问题：

```python
>>> from functools import wraps
>>> def log(func):
...     @wraps(func)
...     def decorator(*args, **kwargs):
...         print('Function ' + func.__name__ + ' has been called at ' + datetime.now().strftime('%Y-%m-%d %H:%M:%S'))
...         return func(*args, **kwargs)
...     return decorator
...
>>> @log
... def add(x, y):
...     return x + y
...
>>> add.__name__
'add'
```



## 时间函数

```python
from datetime import *

today = date.today()#此刻时间

today.year#今年，以此类推


timedelta(参数)#时间增量函数
#参数举例：days=1，hours=-8
```

## 多进程、多线程

我们常见的 Linux、Windows、Mac OS 操作系统，都是支持多进程的多核操作系统。所谓多进程，就是系统可以同时运行多个任务。例如我们的电脑上运行着 QQ、浏览器、音乐播放器、影音播放器等。在操作系统中，每个任务就是一个进程。每个进程至少做一件事，多数进程会做很多事，例如影音播放器，要播放画面，同时要播放声音，在一个进程中，就有很多线程，每个线程做一件事，多个线程同时运行就是多线程。可以在实验环境终端执行 `ps -ef` 命令来查看当前系统中正在运行的进程。

```python
import os
from multiprocessing import Process

def hello(name):
    # os.getpid() 用来获取当前进程 ID
    print('child process: {}'.format(os.getpid()))
    print('Hello ' + name)

# 当我们运行一个 Python 程序，系统会创建一个进程来运行程序，被称为主进程或父进程
# 前面课程中，我们写的程序都是单进程程序，即所有代码都运行在一个主进程中
# 下面的 main() 函数就运行在主进程中
def main():  
    # 打印当前进程即主进程 ID
    print('parent process: {}'.format(os.getpid()))
    # Process 对象只是一个子任务，运行该任务时系统会自动创建一个子进程
    # 注意 args 参数要以 tuple 方式传入
    p = Process(target=hello, args=('shiyanlou', ))
    print('child process start')
    # 启动一个子进程来运行子任务，该进程运行的是 hello() 函数中的代码
    p.start()
    p.join()
    # 子进程完成后，继续运行主进程
    print('child process stop')
    print('parent process: {}'.format(os.getpid()))

if __name__ == '__main__':
    main()
```

计算机的两大核心为运算器和存储器。常说的手机配置四核、八核，指的就是 CPU 的数量，它决定了手机的运算能力；128G、256G 超大存储空间，指的就是手机存储数据的能力。当我们运行一个程序来计算 3 + 5，计算机操作系统会启动一个进程，并要求运算器派过来一个 CPU 来完成任务；当我们运行一个程序来打开文件，操作系统会启动存储器的功能将硬盘中的文件数据导入到内存中。

一个 CPU 在某一时刻只能做一项任务，即在一个进程（或线程）中工作，当它闲置时，会被系统派到其它进程中。单核计算机也可以实现多进程，原理是第 1 秒的时间段内运行 A 进程，其它进程等待：第 2 秒的时间段内运行 B 进程，其它进程等待。。。第 5 秒的时间段内又运行 A 进程，往复循环。当然实际上 CPU 在各个进程间的切换是极快的，在毫秒（千分之一）、微秒（百万分之一）级，以至于我们看起来这些程序就像在同时运行。现代的计算机都是多核配置，四核八核等，但计算机启动的瞬间，往往就有几十上百个进程在运行了，所以进程切换是一定会发生的，CPU 在忙不迭停地到处赶场。注意，什么时候进行进程切换是由操作系统决定的，无法人为干预。

```python
import time

def io_task():
    # time.sleep 强行挂起当前进程 1 秒钟
    # 所谓 ”挂起“，就是进程停滞，后续代码无法运行，CPU 无法进行工作的状态
    # 相当于进行了一个耗时 1 秒钟的 IO 操作
    # 上文提到过的，IO 操作可能会比较耗时，但它不会占用 CPU
    # 在这一秒时间内，CPU 可能被运算器派往其它进程 / 线程中工作
    time.sleep(1)

def main():
    start_time = time.time()
    # 循环 IO 操作 5 次
    for i in range(5):
        io_task()
    end_time = time.time()
    # 打印运行耗时，保留 2 位小数
    print('程序运行耗时：{:.2f}s'.format(end_time-start_time))

if __name__ == '__main__':
    main()
```

```python
import time
# 引入 Process 类
from multiprocessing import Process

def io_task():
    # time.sleep 强行挂起当前进程 1 秒钟
    # 所谓”挂起“，就是进程停滞，后续代码无法运行，CPU 无法进行工作的状态
    # 相当于进行了一个耗时 1 秒钟的 IO 操作
    # 上文提到过的，IO 操作可能会比较耗时，但它不会占用 CPU
    time.sleep(1)

def main():
    start_time = time.time()
    '''
    for i in range(5):
        io_task()
    '''
    # 创建一个列表存放子任务备用
    process_list = []
    # 创建 5 个多进程任务并加入到任务列表中
    for i in range(5):
        process_list.append(Process(target=io_task))
    # 启动所有子任务
    # 此时操作系统会创建 5 个子进程并派出闲置的 CPU 来运行 io_task() 函数
    for process in process_list:
        process.start()
    # join 方法将主进程挂起并释放 CPU，在一旁候着，直到所有子进程运行完毕
    for process in process_list:
        process.join()
    # 子进程运行完毕，以下代码运行在主进程中
    end_time = time.time()
    print('程序运行耗时：{:.2f}s'.format(end_time-start_time))

if __name__ == '__main__':
    main()
```

#### 进程间通信

进程有自己独立的运行空间，它们之间所有的变量、数据是隔绝的，A 进程中的变量 test 与 B 进程的变量没有任何关系，这就意味要使用一些特殊的手段才能实现它们之间的数据交换。`multiprocessing` 模块提供了管道 `Pipe` 和队列 `Queue` 两种方式。

这两种方式的基本概念和实现机制可以通过后续的实验代码进行学习

##### pipe

如果把两个进程想象成两个密封的箱子，那 `Pipe` 就像是连接两个箱子的一个管道，借助它可以实现两个箱子之间简单的数据交换。看一下它的使用方法：

```python
from multiprocessing import Process, Pipe

conn1, conn2 = Pipe()

def send():
    data = 'hello shiyanlou'
    conn1.send(data)
    print('Send Data：{}'.format(data))

def recv():
    data = conn2.recv()
    print('Receive Data：{}'.format(data))

def main():
    Process(target=send).start()
    Process(target=recv).start()

if __name__ == '__main__':
    main()
```

##### queue

除了 Pipe 外，`multiprocessing` 模块还实现了一个可以在多进程下使用的队列结构 `Queue`，改写上面的程序：

```python
from multiprocessing import Process, Queue

# 创建队列实例
queue = Queue()

# 该函数的任务是向队列中发送数据
def f1(q):
    i = 'Hello shiyanlou'
    q.put(i)
    print('Send Data: {}'.format(i))

# 该函数的任务是从队列中获取数据
def f2(q):
    data = q.get()
    print('Receive Data: {}'.format(data))

def main():
    Process(target=f1, args=(queue,)).start()
    Process(target=f2, args=(queue,)).start()

if __name__ == '__main__':
    main()
```

另外通过 `Queue.empty()` 方法可以判断队列中是否为空，是否还有数据可以读取，如果返回为 True 表示已经没有数据了。

#### 进程同步

##### Value

看一个例子，有一个计数器 i，初始值为 0，现在创建并运行 10 个进程，每个进程对 i 进行 50 次加 1 操作，也就是说理论上最后的结果是 500。

`Value` 是一个方法，可以实现数据在多进程之间共享，该方法的返回值即 `Value` 对象可以看做是一个全局共享的变量。使用 `help(Value)` 查看参数，第一个参数是共享的数据类型，`'i'` 指的是 ctyps.c_int 就是整数，第二个参数是 `Value` 对象的值，在进程中可以通过 `Value` 对象的 `value` 属性获取。

```python
import time
from multiprocessing import Process, Value

# 该函数运行在子进程中，参数 val 是一个 Value 对象，是全局变量
def func(val):
    # 将 val 这个全局变量的值进行 50 次 +1 操作
    for i in range(50):
        time.sleep(0.01)
        val.value += 1

def main():
    # 多进程无法使用全局变量，multiprocessing 提供的 Value 是一个代理器，可以实现在多进程中共享这个变量
    # val 是一个 Value 对象，它是全局变量，数据类型为 int，初始值为 0
    val = Value('i', 0)
    # 创建 10 个任务，备用
    processes = [Process(target=func, args=(val,)) for i in range(10)]
    # 启动 10 个子进程来运行 procs 中的任务，对 Value 对象进行 +1 操作
    for p in processes:
        p.start()
    # join 方法使主进程挂起，直至所有子进程运行完毕
    for p in processes:
        p.join()
    print(val.value)

if __name__ == '__main__':
    for i in range(5):
        main()
```

```python
$ python3 multi_value.py
250
269
231
201
213
```

![webwxgetmsgimg](/home/liutong/桌面/学习笔记/python/webwxgetmsgimg.jpeg)

以上是value的字符种类

　如果共享的是字符串，则在上表是找不到映射关系的，就是没有code可用。所以我们需要使用原始的ctype类型

　　例如 

　　

```python
from ctypes import c_char_p

　　ss = Value(c_char_p, 'ss')
```

![472792-20160529154604397-1174164140](/home/liutong/桌面/学习笔记/python/472792-20160529154604397-1174164140.png)

##### 进程锁

正确的做法是每次进行加 1 操作时候，为 i 加一把锁，也就是说当前的进程在操作 i 时，其它进程不能操作它。`multiprocessing` 模块的 `Lock` 方法封装的锁操作，使用 `acquire()` 方法获取锁，`release()` 方法释放锁。下面是修正后的代码：

```python
import time
from multiprocessing import Process, Value, Lock

def func(val, lock):
    for i in range(50):
        time.sleep(0.01)
        # with lock 语句是对下面语句的简写：
        '''
        lock.acquire()
        val.value += 1
        lock.release()
        '''
        # 为 val 变量加锁，结果就是任何时刻只有一个进程可以获得 lock 锁
        # 自然 val 的值就不会同时被多个进程改变
        with lock:
            val.value += 1

def main():
    val = Value('i', 0)
    # 初始化锁
    # Lock 和 Value 一样，是一个函数或者叫方法，Lock 的返回值就是一把全局锁
    # 注意这把全局锁的使用范围就是当前主进程及其子进程，也就是在运行当前这个 Python 文件过程中有效
    lock = Lock()
    processes = [Process(target=func, args=(val, lock)) for i in range(10)]
    for p in processes:
        p.start()
    for p in processes:
        p.join()
    print(val.value)

if __name__ == '__main__':
    for i in range(5):
        main()
```

加锁的作用是保证变量的修改是稳定可预期的，副作用就是多个进程无法同时运行，因为某个时刻只有一个进程可以获得锁，结果程序运行耗时就会增加。由于我们的代码计算量较小，看不出明显的运行耗时区别。

##### 进程池

进程池 `Pool` 可以批量创建子进程，进程池内维持一个固定的进程数量，当有任务到来时，就去池子中取一个进程处理任务，处理完后，进程被返回进程池。如果一个任务到来而池子中的进程都被占用了，那么任务就需要等待某一个进程执行完。

```python
import os, time, random
from multiprocessing import Pool

# 该函数将运行在子进程中
def task(name):
    # 打印进程 ID
    print('任务{}启动运行, 进程ID：{}'.format(name, os.getpid()))
    start = time.time()
    # 假设这里有一个比较耗时的 IO 操作
    # random.random() 的值是一个 0 到 1 区间内的（左闭右开）随机小数
    time.sleep(random.random() * 3)
    end = time.time()
    print('任务{}结束运行，耗时：{:.2f}s'.format(name, (end-start)))

if __name__=='__main__':
    print('当前为主进程，进程ID：{}'.format(os.getpid()))
    print('-----------------------------------')
    # 创建进程池，池子里面有 4 个子进程可用
    p = Pool(4)
    # 将 5 个任务加入到进程池
    for i in range(1, 6):
        # apply_async 方法异步启动进程池
        # 即池子内的进程是随机接收任务的，直到所有任务完成
        p.apply_async(task, args=(i,))
    # close 方法关闭进程池
    p.close()
    # join 方法挂起主进程，直到进程池内任务全部完成
    print('开始运行子进程...')
    p.join()
    print('-----------------------------------')
    print('所有子进程运行完毕，当前为主进程，进程ID：{}'.format(os.getpid()))
```

##### 多线程

前面我们讲到多任务可以由多进程来完成，而且在一些时候能够明显地提高代码的运行效率，多线程也可以实现类似的功能。一个进程中可以有一个或多个线程，进程内的线程共享内存空间。线程是程序执行的最小单元，一个进程中至少有一个线程（主线程）。因为解释器的设计原因，多线程在 Python 中使用得较少。

Python 的 `threading` 模块提供了对多线程的支持，接口和 `multiprocessing` 提供的多进程接口非常类似，下面我们用多线程改写一开始的多进程例子。

```python
import threading

def hello(name):
    # get_ident() 方法获取当前线程 ID
    print('当前为子线程，线程ID: {}'.format(threading.get_ident()))
    print('Hello ' + name)

def main():
    print('当前为主线程，线程ID：{}'.format(threading.get_ident()))
    print('----------------------------')
    # 初始化一个子线程，参数传递和使用 Process 一样
    t = threading.Thread(target=hello, args=('shiyanlou',))
    # 启动线程和等待线程结束，和 Process 的接口一样
    t.start()
    t.join()
    print('----------------------------')
    print('当前为主线程，线程ID：{}'.format(threading.get_ident()))

if __name__ == '__main__':
    main()
```



## 终端用户输入方法

- import sys

  sys.argv[参数]

  参数0表示脚本名称



# 数据处理

## panda模块

### 使用panda处理csv文件

```python
import panda as pd

date_frame=pd.read_csv(文件路径)

date_frame.to_csv(文件路径，index=False)

#有很多参数，index:write row name，默认为True
```

### Pandas 基本介绍

#### Numpy 和 Pandas 有什么不同 

如果用 python 的列表和字典来作比较, 那么可以说 Numpy 是列表形式的，没有数值标签，而 Pandas 就是字典形式。Pandas是基于Numpy构建的，让Numpy为中心的应用变得更加简单。

要使用pandas，首先需要了解他主要两个数据结构：Series和DataFrame。

#### Series 

```python
import pandas as pd
import numpy as np
s = pd.Series([1,3,6,np.nan,44,1])

print(s)
"""
0     1.0
1     3.0
2     6.0
3     NaN
4    44.0
5     1.0
dtype: float64
"""
```

`Series`的字符串表现形式为：索引在左边，值在右边。由于我们没有为数据指定索引。于是会自动创建一个0到N-1（N为长度）的整数型索引。



#### DataFrame 

```python
dates = pd.date_range('20160101',periods=6)
df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=['a','b','c','d'])

print(df)
"""
                   a         b         c         d
2016-01-01 -0.253065 -2.071051 -0.640515  0.613663
2016-01-02 -1.147178  1.532470  0.989255 -0.499761
2016-01-03  1.221656 -2.390171  1.862914  0.778070
2016-01-04  1.473877 -0.046419  0.610046  0.204672
2016-01-05 -1.584752 -0.700592  1.487264 -1.778293
2016-01-06  0.633675 -1.414157 -0.277066 -0.442545
"""
```

`DataFrame`是一个表格型的数据结构，它包含有一组有序的列，每列可以是不同的值类型（数值，字符串，布尔值等）。`DataFrame`既有行索引也有列索引， 它可以被看做由`Series`组成的大字典。

我们可以根据每一个不同的索引来挑选数据, 比如挑选 `b` 的元素:

#### DataFrame 的一些简单运用 

```python
print(df['b'])

"""
2016-01-01   -2.071051
2016-01-02    1.532470
2016-01-03   -2.390171
2016-01-04   -0.046419
2016-01-05   -0.700592
2016-01-06   -1.414157
Freq: D, Name: b, dtype: float64
"""
```

我们在创建一组没有给定行标签和列标签的数据 `df1`:

```python
df1 = pd.DataFrame(np.arange(12).reshape((3,4)))
print(df1)

"""
   0  1   2   3
0  0  1   2   3
1  4  5   6   7
2  8  9  10  11
"""
```

这样,他就会采取默认的从0开始 index. 还有一种生成 `df` 的方法, 如下 `df2`:

```python
df2 = pd.DataFrame({'A' : 1.,
                    'B' : pd.Timestamp('20130102'),
                    'C' : pd.Series(1,index=list(range(4)),dtype='float32'),
                    'D' : np.array([3] * 4,dtype='int32'),
                    'E' : pd.Categorical(["test","train","test","train"]),
                    'F' : 'foo'})
                    
print(df2)

"""
     A          B    C  D      E    F
0  1.0 2013-01-02  1.0  3   test  foo
1  1.0 2013-01-02  1.0  3  train  foo
2  1.0 2013-01-02  1.0  3   test  foo
3  1.0 2013-01-02  1.0  3  train  foo
"""
```

这种方法能对每一列的数据进行特殊对待. 如果想要查看数据中的类型, 我们可以用 `dtype`这个属性:

```python
print(df2.dtypes)

"""
df2.dtypes
A           float64
B    datetime64[ns]
C           float32
D             int32
E          category
F            object
dtype: object
"""
```

如果想看对列的序号:

```python
print(df2.index)

# Int64Index([0, 1, 2, 3], dtype='int64')
```

同样, 每种数据的名称也能看到:

```python
print(df2.columns)

# Index(['A', 'B', 'C', 'D', 'E', 'F'], dtype='object')
```

如果只想看所有`df2`的值:

```python
print(df2.values)

"""
array([[1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo']], dtype=object)
"""
```

想知道数据的总结, 可以用 `describe()`:

```python
df2.describe()

"""
         A    C    D
count  4.0  4.0  4.0
mean   1.0  1.0  3.0
std    0.0  0.0  0.0
min    1.0  1.0  3.0
25%    1.0  1.0  3.0
50%    1.0  1.0  3.0
75%    1.0  1.0  3.0
max    1.0  1.0  3.0
"""
```

如果想翻转数据, `transpose`:

```python
print(df2.T)

"""                   
0                    1                    2  \
A                    1                    1                    1   
B  2013-01-02 00:00:00  2013-01-02 00:00:00  2013-01-02 00:00:00   
C                    1                    1                    1   
D                    3                    3                    3   
E                 test                train                 test   
F                  foo                  foo                  foo   

                     3  
A                    1  
B  2013-01-02 00:00:00  
C                    1  
D                    3  
E                train  
F                  foo  

"""
```

如果想对数据的 `index` 进行排序并输出:

```python
print(df2.sort_index(axis=1, ascending=False))

"""
     F      E  D    C          B    A
0  foo   test  3  1.0 2013-01-02  1.0
1  foo  train  3  1.0 2013-01-02  1.0
2  foo   test  3  1.0 2013-01-02  1.0
3  foo  train  3  1.0 2013-01-02  1.0
"""
```

如果是对数据 值 排序输出:

```python
print(df2.sort_values(by='B'))

"""
     A          B    C  D      E    F
0  1.0 2013-01-02  1.0  3   test  foo
1  1.0 2013-01-02  1.0  3  train  foo
2  1.0 2013-01-02  1.0  3   test  foo
3  1.0 2013-01-02  1.0  3  train  foo
"""
```

查看行数据

```python
df2 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(4)), dtype='float32'),
                    'D': np.array([3] * 4, dtype='int32'),
                    'E': pd.Categorical(["test", "train", "test", "train"]),
                    'F': 'foo'}, index=['a', 'b', 'c', 'd'])

# print(pd.Series(1, index=list(range(4)), dtype='float32'))
# print(df2)
print(df2.loc['a'])
print(df2.iloc[0])
```

### panda处理excel

#### 读取

```python
 # coding=gbk

   import pandas as pd

   df = pd.read_excel('C:/Users/enuit/Desktop/data_test.xlsx')
```



#### 写入

```python
# 任务：输出满足成绩大于等于90的数据

writer = pd.ExcelWriter('C:/Users/enuit/Desktop/out_test.xlsx')
temp = []
for i in range(len(df.index.values)):
    if df.iloc[i, 3] >= 90:
        temp.append(df.iloc[i].values)
df2 = pd.DataFrame(data=temp, columns=df.columns.values)

# 不写index会输出索引

df2.to_excel(writer, 'Sheet', index=False)
writer.save()


```

#### 处理字典

**data**:字典形式为{field：array-like}或{field：dict}。
**orient**:{‘columns’，‘index’}，默认’列’数据的“方向”。如果传递的dict的键应该是结果DataFrame的列，则传递’columns’（默认值）。否则，如果键应该是行，则传递’index’。
**dtype：dtype**:默认无数据类型强制，否则推断。
**columns**：list默认无要使用的列标签orient=‘index’。如果使用，则引发ValueError orient=‘columns’。

## csv模块

```python
import csv

csv.reader(filename,delimiter=',')

csv.writer(filename,delimiter=',')

#参数delimiter指定默认分隔符
```

## next()函数

- next(可迭代参数，默认值参数)

- 当迭代完成，没有值返回时，返回默认参数，而不会报错。默认参数可以不写。



## enumerate()函数

- enumerate(可迭代数据容器，[start=index value])，同时获得索引值和元素值，生成由元组组成的列表。

```python
>>>seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```



```python
>>>seq = ['one', 'two', 'three']
>>> for i, element in enumerate(seq):
...     print i, element
... 
0 one
1 two
2 three
```



## xlrd、xlwt、xlsxwriter模块

### cell_type()函数

- 有6种类型:一、0:空值。二、1:字符串。三、2:数字。四、3:日期。五、4:布尔值。六、5:error。

### 重置时间

方法一xlwt

```python


 if worksheet.cell_type(row_index,column_index) == 3:
 
date_cell=xldate_as_tuple(worksheet.cell_value(row_index,column_index),workbook.datemode)

 date_cell = date(*date_cell[0:3]).strftime('%Y/%m/%d')
 output_worksheet.write(row_index,column_index,date_cell)
```




方法二xlsxwriter

```python
date_format = output_workbook.add_format({'num_format': 'yyyy/mm/dd'})

 if worksheet.cell_type(row_index,column_index) == 3:
 
date_cell=xldate_as_tuple(worksheet.cell_value(row_index,column_index),workbook.datemode)

 date_cell = str(date_cell[0])+'/'+str(date_cell[1])+'/'+str(date_cell[2])
 
date_cell = datetime.strptime(date_cell, "%Y/%m/%d")
            output_worksheet.write(row_index,column_index,date_cell,date_format)
```



## 正则表达式简单应用

```python
import re

re.search(子字符串,字符串,re.I)

#检测字符串中是否含有子字符串，re.I的作用是不区分大小写。结果可用bool()转化成布尔型。
```



# 数据可视化

## 添加横线

```python
plt.axhline(0.5,-2,2,c='red')
```




## 移动坐标轴位置

```python
plt.gca().spines['right'].set_color('none')plt.gca().spines['top'].set_color('none')

plt.gca().spines['bottom'].set_position(('data',0))

plt.gca().spines['left'].set_position(('data',0))
```




## 添加图例

```python
o1, = plt.plot(x1,y1,label='sin')#将线段传递给图例对象名后必须加，

o2,=plt.plot(x1,y2,c='yellow',label='cos',linestyle='--')

plt.axhline(0.5,-2,2,c='red',label='straight_line')

plt.legend(handles=[o1,o2,],loc='best')#最佳位置
```





  

## matplotlib添加子图

### subplot2grid（）网格化

```python
ax2 = subplot2grid((3,3),(1,1),colspan=2)

＃总画布行与列，从第几行第几列开始，列之间的空格。

ax2.scatter([2,5,8],[7,8,3])

ax2.set_title('hello')

ax2.set_xticks([1,3,5,7,9])

ax2.set_xticklabels(['a','b','c','d','e'])
```

### axes()

```python
ax_histx = plt.axes([left, bottom + width + spacing, height, 0.2])
```



- 自己的理解，要求四个参数，参数过多可以用‘+’连接，长宽交换影响不大，连接的边‘left’与‘bottom’，二者肯定有一个在加法式子里，哪边连接，哪边就在加法式子里，另一个为单独参数；数字影响比列。无比列就分开写四个参数，即为基底的坐标轴图像。四个参数归一化，分别为左右，上下，长，宽。



```python
import numpy as np
import matplotlib.pyplot as plt

#设定图像函数关系
x1 = np.linspace(-np.pi,np.pi,256)
y1 = np.sin(x1)
y2 = np.cos(x1)
y3 = 1.5+0*x1
#设地子图参数
left, width = 0.1, 0.65
bottom, height = 0.1, 0.65
spacing = 0.005

#创建画布
plt.figure()

plt.axes([left, bottom + width + spacing, height, 0.2]).plot(x1,y2,c='yellow',label='cos',linestyle='--',marker='>')

plt.axes([left + width + spacing, bottom, 0.2, height]).plot(x1,y3,label='straightline')

plt.axes([left,bottom,width,height]).plot(x1,y1,label='sin',linestyle='steps',marker='p')

plt.xticks([-np.pi,-np.pi/2,0,np.pi/2,np.pi],\
    [r'$-\pi$',r'$-\pi/2,0$',r'$0$',r'$\pi/2$',r'$\pi$'])
plt.show()
```

