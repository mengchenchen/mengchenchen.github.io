---
title: 《Python学习系列》3、python基础
tag: python
---

##### 注释

```python
# 表示单行注释

''' 
这里多行注释
这里多行注释
...

"""
这里也多行注释
这里也多行注释
...

```

##### 输出函数 print()

```python
print("hello world")	# hello world
print(5)			# 10
print(5 + 8) 		# 13
print("5 + 8 = " , 13) 	# 5 + 8 = 13
# 打印多行
print('''
	你好
	我好
	大家好
''')

# 字符串不进行转义
print(r"\\\t\\")
```

##### 输入函数 input()

```python
age = input("请输入你的年龄：")	# 定义变量age，等待输入（术语阻塞）
print("age = ", age) # age = 20
```

##### 查看关键字

```python
import keyword
print(keyword.kwlist)
```

#### 标识符

对标识符这个概念一直都不太了解，今天看视频发现讲的很模糊，也不明白标识符到底和变量是什么区别和联系，这个答案对我来说完全就明白了[标识符和变量](https://zhidao.baidu.com/question/499395119.html) 

- 标识符由字母、数字、下划线组成
- 不能以数字开头
- 区分大小写
- 以下划线开头的标识符具有特殊意义
- 以双下划线开头的 __foo 代表类的私有成员，__foo(self)代表类的私有方法，不能直接从外部调用，需通过类里的其他方法调用
- 以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数

##### 关键字

我刚才把Python2.7给卸载了重装了3.6版本，2.7只有31个关键字

```shell
>>> help("keywords") # 方法一

Here is a list of the Python keywords.  Enter any keyword to get more help.

False               def                 if                  raise
None                del                 import              return
True                elif                in                  try
and                 else                is                  while
as                  except              lambda              with
assert              finally             nonlocal            yield
break               for                 not
class               from                or
continue            global              pass

>>> import keyword # 方法二
>>> keyword.kwlist # 方法二
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
>>>
```



#### 变量

程序运行期间可以改变的值，每个变量都有特定的类型

作用：将不同类型的数据存储到内存

##### 定义变量

```
# 标量名称 =  初始值
name  = 'bryce'
age   = 18
money = 5458.52 

# 连续定义多个变量
num1 = num2 = num3 = 1

# 交互式赋值定义变量
num4 , num5 = 1,2
```

##### 删除变量 del

```
age = 18
del age # age就相当于未定义
```

##### 查看变量类型 type()

```python
age   = 18 
money = 52053.562
name  = 'bryce'
print(type(age))	# <class 'int'>
print(type(money))	# <class 'float'>
print(type(name))	# <class 'str'>
```

##### 查看变量地址

```python
age = 18
print(id(age)) # 45641354652
```

----

#### 

### 数学函数

##### 绝对值 abs()

```python
money = -10000
print(abs(money))	# 10000
```

##### 最大值 max()

```python
print(max(1,2,3,4,5)) # 5
```

##### 最大值 min()

```python
print(min(1,2,3,4,5)) # 1
```

##### 次方 pow()

````python
print(pow(2,5)) # 2^5 二的五次方
````

##### 四舍五入round()

````python
# 默认整数部分四舍五入
print(round(2.521))	# 3
print(round(2.421))	# 2

# 指定小数点后几位四舍五入
print(round(2.521,2))	# 2.52
print(round(2.421,1))	# 2.4
print(round(5.561,1))	# 2.6
````

##### 数学库

```python
# 引入数学库
import math

# 向上取整
print(math.ceil(18.1))	# 19
print(math.ceil(18.9))  # 19

# 向下取整
print(math.ceil(18.1))	# 18
print(math.ceil(18.9))  # 18

# 获取整数部分与小数部分
print(math.modf(22.3)) #  (0.3000000000007, 22.0)

# 开方
print(math.sqrt(16)) 	# 4
```

##### 随机数库

```python
# 引入随机数库
import random

# 从序列元素中随机挑选一个元素
print(random.choice([1,3,5,7,9]))	# 随机值 1,3,5,7,9 其中一个
print(random.choice(range(100))	# 随机值 0 - 99 其中一个
print(random.choice("bryce")	# 随机值 b,r,y,c,e 其中一个

# 生成1~100 之间的随机数
r1 = random.choice(range) + 1 
print(r1)	

# 随机产生[0-1]之间的数
print(random.random())

# 取出1-100之间所有的奇数随机数
# randrange([start,]stop[,step])
# start--指定范围的开始值，包含在范围内，默认是0
# stop--指定范围的结束值，不包含在范围内
# step--制定范围内数值的递增，默认是1
print(random.randrange(1,100,2))

# 序列所有的元素随机排序
list = [1,2,3,4,5,6]
print(random.shuffle(list))	# 结果的排序是随机的

# 随机生成一个实数 uniform(a,b),范围a - b之间，可能是浮点数也可能是整数
print(random.uniform(3,9))	

```



#### 字符串

```python
# 字符串相加
str1 = 'wang'
str2 = 'gang'
print(str1 + str2) # wang gang

# 重复字符串
str3 = 'new'
print(str3 * 3) # newnewnew

# 获取字符串指定字符
print(str1[0]) # w 

# 获取指定字符索引之前所有字符
print(str1[:3]) # wan

# 获取指定字符所有之后所有字符
print(str1[3:]) # g

# 截取字符索引之间字符
print(str1[0:2]) # wa

# 指定字符是否存在字符串对象中
str4 = 'my name is meng'
print("my" in str4)		# true
print('my1' in str4)	# false

# 指定字符不存在字符串对象中
print('good' not in str4) #true

# 格式化输出
num = 10
money = 105.55411

# 占位符
# %d 代表整数，%s 代表字符串，%f 代表浮点数,%.3f 代表小数点后保留位数
print("num = %d,str4 = %s,money = $.3f" % (num,str4))	
# num = 10,str4 = my nmae is meng,money = 105.55411

# 换行符
# \n 占一个字节
print("num = %d\nstr4 = %s\nmoney = $.3f" % (num,str4))	

# 制表符 \t

# eval()
# 将字符创当成表达式执行
print(eval("12-9")) # 3

# len()
# 字符串长度 
print(len("my name is meng"))	# 15

# lower()
# 字符串转换小写 
str5 = " My Name"
print(str5.lower()) # my name

# upper()
# 字符串转换大写 
print(str5.upper())	# MY NAME

# swapcase()
# 将字符串中大小写转换 
print(str5.swapcase()) # mY nAME

# capitalize()
# 字符串首字母大写 
print(str5.capitalize()) # My name

# title()
# 每个单词的首字母大写
print(str5.title()) # My Name

# center(width[,fillcahr]) 
# 字符串居中，指定字符填充左右空格，默认空格填充
str6 = "kaige is a dog"
print(str6.center(40,'*')) # **************kaige is a dog**************

# ljust(width[,fillchar])
# 字符串左对齐，指定字符填充右侧空格 
print(str6.ljust(40, "*")) # kaige is a dog ****************

# rjust(width[,fillchar])
# 字符串右对齐，指定字符填充左侧空格
print(str6.rjust(40, "*")) # ****************kaige is a dog 

# zfill(width)
# 指定字符长度右对齐字符串，用0填充 
print(str6.zfill(40)) # 0000000000000kaige is a dog

# count(str[,start][,end])
# 返回字符创中指定字符串的出现次数，可以指定范围，默认从头到尾
str7 = "this is a very very very nice box"
print(str7.count("very",10,len(str7)))

# find(str[,start][,end])
# 从左向右检测指定str是否包含在字符串中，可以范围，默认从头到尾。得到的是第一次出现的开始所有,没有范围 -1
print(str7.find("very"))	# 10
print(str7.find("good")) 	# -1
print(str7.find("very",10,len(str7)))

# rfind(str[,start][,end])
# 从右向左检测指定str是否包含在字符串中，可以范围，默认从头到尾。得到的是第一次出现的开始所有,没有范围 -1
print(str7.find("very"))	# 10
print(str7.find("good")) 	# -1
print(str7.find("very",0,10))

# index(str,start=0,end=len(str))
# 从左往右和find()功能一致，但是指定字符查找不到会报错
# print(str7.index("good"))	# 报错

# rindex(str,start=0,end=len(str))
# 从右往左和find()功能一致，但是指定字符查找不到会报错
# print(str7.rindex("good"))	# 报错
     
# lstrip()
# 截取字符串左侧指定的字符，默认为空格
str8 = "*****kaiig*****"
print(str8.lstrip("*")) # kaiig*****

# rstrip()
# 截取字符串右侧指定的字符，默认为空格
print(str8.lstrip("*")) # *****kaiig

# strip()
# 去掉所有字符串指定字符，默认为空格
print(str8.strip("*")) # kaiig

```

##### 列表 list

```python
​```
创建列表
列表名 = [选项1，选项2...，选项n]
​```

# 创建空列表
list1 = []
print(list1)	# []

# 创建带有元素的列表
list2  = [18,19,"sumk",True,225.53,23]
print(list2) 	# [18,19,"sumk",True,225.53,23]

# 列表元素的访问
print(list2[2])		# sumk

# 替换 索引值不能溢出，否则报错
list2[2] = 'meng'
print(list2)	# [18,19,"meng",True,225.53,23]

# 列表相加
print(list1 + list2)	# [18,19,"sumk",True,225.53,23]

# 列表重复
print(list2 * 2)	# [18,19,"sumk",True,225.53,23,18,19,"sumk",True,225.53,23]

# 元素是否存在 in
print(18 in list2)	# True

# 列表截取
print(list2[1:4])	# 索引1-3 [19,"sumk",True]
print(list2[3:])	# 索引3之后的 [225.53,23]
print(list2[:3])	# 索引3之前的  [18,19,"meng"]

# 二维列表
list3 = [[1,2,3],[4,5,6],[7,8,8]];
print(list3[1][1])	# 5

# list.append()
# 在列表末尾添加一个新的元素
list2.append(6)			# [18,19,"sumk",True,225.53,23,6]
list2.append([7,8,9]) 	 # [18,19,"sumk",True,225.53,23,6,[7,8,9]]

# extend()
# 在列表末尾追加新的列表
list4 = [1,2,3]
list4.extend([4,5,6])
print(list4)	# [1,2,3,[4,5,6]]

# insert()
# 在指定索引出插入一个新的元素,可以添加列表
list5 = [1,2,3]
list5.insert(2,100)	
print(list5)		# [1,2,100,3]

# pop(x=list[-1])
# 移除列表中指定索引元素，默认移除最后一个元素
# list[-1] 代表最后一个元素
list5.pop()		#  [1,2,100,3]
list5.pop(2)	#  [1,2,3]

# remove()
# 移除列表中的指定元素第一个
list5.remove(1)		# [2,3]

# clear()
# 清楚列表中所有的元素
list5.clear()

# index(value[,start=None][,stop=None])
# 寻找列表中指定元素的第一个匹配的索引值
list6 = [1,2,3,5,6,5,6]
print(list6.index(3))	# 2

# len(list)
# 获取列表元素个数
print(len(list6))	# 7

# max(list)
# 获取列表中最大的元素
print(max(list6))	# 6

# min(list)
# 获取列表中最小的元素
print(min(list6))	# 1

# count()
# 查看指定元素在列表出现的次数
list6.count(6)	# 2

# reverse() 倒序
list6.reverse()	# [6,6,5,5,3,2,1]

# sort() 正序
list6.sort()

# 浅拷贝 引用拷贝
list7 = list6	# 如果修改list7的值会直接改变list6，因为他们在内存中指向同一个地址

# 深拷贝 内存拷贝
list8 = list6.copy()	# 可以使用id() 获取内存地址，会开辟一个新空间

# 将元组转换成列表
print(list((1,2,3,4)))








```

