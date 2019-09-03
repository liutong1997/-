

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



## 时间函数

```python
from datetime import *

today = date.today()#此刻时间

today.year#今年，以此类推


timedelta(参数)#时间增量函数
#参数举例：days=1，hours=-8
```



### for循环else

- else语句可以对应的是for，不是if，这个是python特有的语句。

- 即在for 循环中，如果没有从任何一个break中退出，则会执行和for对应的else

- 只要从break中退出了，则else部分不执行。



## 终端用户输入方法

- import sys

  sys.argv[参数]

  参数0表示脚本名称



# 数据处理

## 使用panda处理csv文件

```python
import panda as pd

date_frame=pd.read_csv(文件路径)

date_frame.to_csv(文件路径，index=False)

#有很多参数，index:write row name，默认为True
```

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

