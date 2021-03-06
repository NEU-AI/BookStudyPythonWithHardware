

第3章 制作简单计算器
=========

3.1 字符与字符串
----------------

3.1.1 什么是字符串

字符串是一种表示文本的数据类型，字符串中的字符可以是ASCII字符，各种符号以及各种Unicode字符。Python中的字符串有如下三种表现形式：

1. 使用单引号包含字符。示例代码如下：
::

'a' , '123 '

注意，单引号表示的字符串中不能包含单引号，如let’s go不能使用单引号包含。

2. 使用双引号包含字符。示例代码如下：
::

"a ", "123 "

注意，双引号表示的字符串里不能包含双引号，并且只能有一行。

3. 使用三引号（三对单引号或者三对双引号）包含字符。示例代码如下：
::

   """
   Hello,
   Welcome to China
   """
   
或者
::

   '''
   你好，欢迎来到中国
   '''

需要注意的是，三个引号能包含多行字符串，在这个字符串中可以包含换行符、制表符或者其他特殊的字符。通常情况下，三引号表示的字符串出现在函数声明的下一行，用来注释函数。与C语言的字符串不同的是，Python字符串不能被改变。向一个索引位置赋值，例如，word[0]
= ‘m’会导致错误。

【案例3-1】 字符串使用

>>> word="hello!"
>>> word[0]
'h'
>>> word[0]='a'
Traceback (most recent call last):
File "<pyshell#14>", line 1, in <module>
word[0]='m'
TypeError: 'str' object does not support item assignment

3.1.2 转义字符

不管使用单引号还是双引号包含，使用print输出字符串的时候，值都是一样的。至于为什么两种情况都可以表示字符串，是因为某些情况下它们会派上用场。

【案例3-2】 字符串转义
::

   >>>"let's go!"
   "let's go!"
   >>>'"nice to meet you!",he said'
   '"nice to meet you!",he said'

上面的代码中，第1行代码的字符串内容有单引号，所以要使用双引号包含。而第3行代码的字符串内容有双引号，所以要使用单引号包含。如果不这么做，当解释器在根据单引号或者双引号辨别字符串的结果符时，难免会发生错误。例如，下面的代码就会报错：

>>> 'let's go! go'
SyntaxError: invalid syntax

当然，对于单引号或者双引号这些特殊的符号，我们可以对它们进行转义，例如，对字符串中的单引号进行转义，代码如下：

>>> 'let\'s go! go'
"let's go! go"

上述代码中，使用斜线的方式，对单引号进行了转义，这样当解释器遇到这个转义字符的时候，会明白这不是字符串的结束标记。而像这样的转义符号有很多种，接下来，通过一张表来列举，如表3-1所示：

表3-1 转义字符

.. image:: /Chapter/picture/image138.jpg

续表

.. image:: /Chapter/picture/image139.jpg

当然，如果你不想使用反斜杠（\）转义特殊字符，可以在字符串前面添加一个“r”，表示原始的字符串，示例代码如下：

>>> print('ru\noob')
ru
oob
>>> print(r'ru\noob')
ru\noob

3.1.3 字符串的输入和输出

1. 字符串输出

例如有以下代码：
::

   print("我今年10岁")
   print("我今年11岁")
   print("我今年12岁")

Python支持字符串的格式化输出，尽管这样可能会用到非常复杂的表达式，但是了基本的用法就是将一个值插入到一个有字符串格式符%s的字符串中。上述代码多次输出"我今年XX岁"，其中只有XX代表内容是可变的，其余的内容都是固定不变的。大家试想一下，有没有简化上述程序的方式呢？当然有，可以在字符串中使用格式字符串来完成。例如下面的代码：
::

   name="小明"
   print("大家好，我叫%s"%name)

在上述的程序中，看到了%s这样的操作符，这就是Python中字符串的格式化符号。

除此以外，还可以使用%符号对其他类型的数据进行格式化，常见的格式化符号如表3-2所示

表3-2 格式化符号

.. image:: /Chapter/picture/image140.jpg

2. 字符串输入

Python
3提供了input函数从标准输入读取一行文本，默认的标准输入是键盘，示例代码如下：
::

   user_name = input("请输入用户名")
   print(user_name)

上述示例中，input函数传入字符串信息，用于获取数据前给用户提示，并且将接收的输入直接赋值给等号左边的变量user_name。需要注意的是，input获取的数据，即使是数字，也是以字符串的方式进行保存的。

3.1.4 访问字符串中的值

1. 字符串的存储方式

Python不支持单字符类型，单字符在Python也是作为一个字符串使用。如果希望访问字符串中的值，需要使用下标来实现。例如：
::

   name = "abcdef"

如果要从字符串中取出字符，可以通过下标来读取。例如，如果要取出字符a，对应的下标位置为0，所以用name[0]读取出来，如果想读取字符d，它对应的下标位置是3，所以用name[3]取出来。

2. 使用切片截取字符串

切片是指对操作的对象截取其中一部分的操作。字符串，列表，元组都支持切片操作。这里，我们以字符串为例讲解切片的作用。切片的语法格式如下：

[起始：结束：步长]

需要注意的事，切片选取的区间属于左闭右开型，即从“开始”位开始，到“结束”位的前一位结束（不包含结束位本身）。接下来，通过一个案例来演示如何使用切片截取字符串name= "abcdef"。

【案例3-3】 字符串切片使用
::

   name = "abcdef"
   print(name[0:3]) #取下标为0-2的字符
   print(name[3:5]) #取下标为3，4的字符
   print(name[1:-1]) #取下标为1开始到倒数第2个之间的字符
   print(name[2:]) #取下标为2开始到最后的字符
   print(name[::-2]) #倒序从后往前，取步长为2的字符

结果如下：
::
   
      abc
      de
      bcde
      cdef
      fdb

3.1.5 python的字符串内建函数

字符串方法是从python1.6到2.0慢慢加进来的——它们也被加到了Python中。这些方法实现了string模块的大部分方法，如下表所示列出了目前字符串内建支持的方法，所有的方法都包含了对Unicode的支持，有一些甚至是专门用于Unicode的。部分内建函数如表3-3所示：

表3-3 Python内建字符串函数

.. image:: /Chapter/picture/image141.jpg

续表

.. image:: /Chapter/picture/image142.jpg
.. image:: /Chapter/picture/image143.jpg

续表

.. image:: /Chapter/picture/image144.jpg

3.2 基本的数学运算
------------------

3.2.1 运算符

运算符用于执行程序代码运算，会针对一个以上操作数项目来进行运算。例如：2+3，其操作数是2和3，而运算符则是“+”。在Python中运算符大致可以分为6种类型：算术运算符、比较运算符、赋值运算符、逻辑运算符、成员运算符和位运算符下面将介绍各种运算符的使用方法，其中逻辑运算符会在第四章介绍分支结构时具体介绍。

1. 算术运算符

算术运算符主要用于计算，例如，+、-、*、/都是算术运算符。接下来，假设a =
10，b = 20，运算具体如表3-4：

表3-4 算术运算符

.. image:: /Chapter/picture/image145.jpg

为了让大家更好地理解算术运算符，通过实例演示Python运算符的操作，如下所示：

【案例3-3】 算术运算符的使用。
::

   a = 3
   b = 5
   c = 10
   c = a + b
   print ("1 ：c 的值为：", c)
   c = a - b
   print ("2 ：c 的值为：", c )
   c = a \* b
   print ("3 ：c 的值为：", c )
   c = a / b
   print( "4 ：c 的值为：", c)
   c = a % b
   print ("5 ：c 的值为：", c)
   # 修改变量 a 、b 、c
   a = 4
   b = 7
   c = a**b
   print ("6 ：c 的值为：", c)
   a = -5
   b = 5
   c = a//b
   print ("7 ：c 的值为：", c)
   
运算结果为：
::

   1 ：c 的值为： 8
   2 ：c 的值为： -2
   3 ：c 的值为： 15
   4 ：c 的值为： 0.6
   5 ：c 的值为： 3
   6 ：c 的值为： 16384
   7 ：c 的值为： -1

2. 比较运算符

比较运算符用于比较两个数，其返回的结果只能是True或者False。表中列举了Python中的比较运算符，以下假设变量a为10，变量b为20，描述如表3-5：

表3-5 比较运算符

.. image:: /Chapter/picture/image146.jpg

为了让大家更好的理解比较运算符，通过举例如下：
::

   a = 21
   b = 10
   c = 0
   if a == b :
      print( "1 ：a 等于 b")
   else:
      print ("1 ：a 不等于 b")
   if a != b :
      print ("2 ：a 不等于 b")
   else:
      print ("2 ：a 等于 b")
   if a < b :
      print ("3 ：a 小于 b" )
   else:
      print ("3 ：a 大于等于 b")
   if a > b :
      print ("4 ：a 大于 b")
   else:
      print ("4 ：a 小于等于 b")
   # 修改变量 a 和 b 的值
   a = 5
   b = 20
   if a <= b :
      print ("5 ：a 小于等于 b")
   else:
      print( "5 ：a 大于 b")
   if b >= a :
      print( "6 ：b 大于等于 a")
   else:
      print ("6 ：b 小于 a")
   
结果：
::

   1 ：a 不等于 b
   2 ：a 不等于 b
   3 ：a 大于等于 b
   4 ：a 大于 b
   5 ：a 小于等于 b
   6 ：b 大于等于 a

3. 赋值运算符

以下假设变量a = 10，变量b = 20，赋值运算符如表3-6所示：

表3-6 赋值运算符

.. image:: /Chapter/picture/image147.jpg

以下实例演示了Python所有赋值运算符的操作：

【案例3-4】赋值运算符使用
::

   a = 21
   b = 10
   c = 0
   c = a + b
   print ("1 : c 的值为：", c)
   c += a
   print ("2 : c 的值为：", c )
   c \*= a
   print( "3 : c 的值为：", c )
   c /= a
   print ("4 : c 的值为：", c )
   c = 2
   c %= a
   print ("5 : c 的值为：", c)
   c \**= a
   print( "6 : c 的值为：", c)
   c //= a
   print( "7 : c 的值为：", c)
 
结果：
::

   1 : c 的值为： 31
   2 : c 的值为： 52
   3 : c 的值为： 1092
   4 : c 的值为： 52.0
   5 : c 的值为： 2
   6 : c 的值为： 2097152
   7 : c 的值为： 99864

4. 位运算

按位运算符是把数字看作二进制来进行计算的。下表中变量 a 为 60，b 为13，二进制格式如表3-7所示。

表3-7 位运算符

.. image:: /Chapter/picture/image148.jpg

以下实例演示了Python所有位运算符的操作：

【案例3-5】位运算符使用
::

   a = 60 # 60 = 0011 1100
   b = 13 # 13 = 0000 1101
   c = 0
   c = a & b; # 12 = 0000 1100
   print ("1 : c 的值为：", c)
   c = a \| b; # 61 = 0011 1101
   print ("2 : c 的值为：", c)
   c = a ^ b; # 49 = 0011 0001
   print( "3 : c 的值为：", c)
   c = ~a; # -61 = 1100 0011
   print ("4 : c 的值为：", c)
   c = a << 2; # 240 = 1111 0000
   print ("5 : c 的值为：", c)
   c = a >> 2; # 15 = 0000 1111
   print( "6 : c 的值为：", c)
结果
::

   1 : c 的值为： 12
   2 : c 的值为： 61
   3 : c 的值为： 49
   4 : c 的值为： -61
   5 : c 的值为： 240
   6 : c 的值为： 15

6. 成员运算符

除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。如下表3-8所示

表3-8 成员运算符

.. image:: /Chapter/picture/image149.jpg

以下实例演示了Python所有成员运算符的操作：

【案例3-6】成员运算符使用
::

   a = 10 
   b = 20 
   list = [1, 2, 3, 4, 5 ]; 
   if ( a in list ): 
      print ("1 - 变量 a 在给定的列表中 list 中" )
   else:
      print ("1 - 变量 a 不在给定的列表中 list 中") 
   if ( b not in list ): 
      print ( "2 - 变量 b 不在给定的列表中 list 中" )
   else: 
      print ("2 - 变量 b 在给定的列表中 list 中")
   # 修改变量 a 的值 
   a = 2 
   if ( a in list ): 
      print ("3 - 变量 a 在给定的列表中 list 中" )
   else: 
      print ("3 - 变量 a 不在给定的列表中 list 中")
    
结果如下：
::

   1 - 变量 a 不在给定的列表中 list 中
   2 - 变量 b 不在给定的列表中 list 中
   3 - 变量 a 在给定的列表中 list 中

3.2.2 运算符优先级

表格3-9列出了从最高到最低优先级的所有运算符：

表3-9 运算符优先级

.. image:: /Chapter/picture/image150.jpg

以下实例演示了Python所有运算符优先级的操作：

【案例3-7】优先级操作
::

   a = 20
   b = 10
   c = 15
   d = 5
   e = 0
   e = (a + b) * c / d       #( 30 * 15 ) / 5
   print ("(a + b) * c / d 运算结果为：",  e)
   e = ((a + b) * c) / d     # (30 * 15 ) / 5
   print ("((a + b) * c) / d 运算结果为：",  e)
   e = (a + b) * (c / d);    # (30) * (15/5)
   print( "(a + b) * (c / d) 运算结果为：",  e)
   e = a + (b * c) / d;      #  20 + (150/5)
   print( "a + (b * c) / d 运算结果为：",  e)
结果：
::

   (a + b) * c / d 运算结果为： 90.0
   ((a + b) * c) / d 运算结果为： 90.0
   (a + b) * (c / d) 运算结果为： 90.0
   a + (b * c) / d 运算结果为： 50.0


3.3 类型的转换
--------------

Python支持的数据型数据类型有int，float，bool和complex。int类型指整数型值，float类型指既有整数又有小数部分的数据类型，这些都是理解的。Bool类型只True(真)和False（假）两种取值，因为bool继承了int类型，即在这两种类型中True可以等价于数值1，False可以等价于数值0，并且可以直接使用bool值进行数学运算。Complex类型由实数部分和虚数部分构成，Python
中的结构形式，如real+imag(J/j后缀)，实数和虚数部分都是浮点数。

3.3.1 各种类型转整型

可以通过下面这个例子来学习一下转换的规律：

>>> int(1.9)
1
>>> int(0.6)
0
>>> int(-1.9)
-1
>>> int( )
0

浮点数转换成整数过程中，只是简单地将小数部分剔除，保留整数部分，注意int()的结果为0。

>>> int(True)
1
>>> int(False)
0

布尔型转整型时，bool值True被转成整数1，False被转换成整数0。

>>> int(2+5j)
Traceback (most recent call last):
File "<pyshell#4>", line 1, in <module>
int(2+5j)
TypeError: can't convert complex to int

通过这个代码可以看出，复数类型无法转换成整型，强制转换会报错。

>>> int("12")
12
>>> int("1a")
>>> int("12.")

另外注意将字符串转为整形时，只有是整形的数字的才能转换，带有非数字符号或小数点等都会报错。

3.3.2 各种类型转浮点型

对于各种类型转换为浮点型，其规律和整形类似

>>> float(19)
19.0
>>> float(0)
0.0
>>> float(True)
1.0
>>> float(False)
0.0
>>> float("12")
12.0
>>> float("12.")
12.0
>>> float("12.a")

从上面的例子可以看出，整型转换后变为浮点型增加.0，bool值转换后True变成1.0
False
变成0.0，字符串转换时，整型字符串和浮点型字符串可以转，带有其他非数字字符的不能转。

3.3.3 各种类型值转布尔型

可以通过下面这个例子来总结一下各种类型值转换成布尔型的规律：

>>> bool(1)
True
>>> bool(2)
True
>>> bool(0)
False
>>> bool(3.5)
True
>>> bool(-0.9)
True
>>> bool(2-3j);
True
>>> bool(0+0j)
False
>>> bool()
False
>>> bool("")
False
>>> bool([])
False
>>> bool(())
False
>>> bool({})
False

从整数、浮点数、复数转布尔型的结果可以总结出一个规律：非0数值转布尔型都为True，数值0转布尔型为False。此外，用bool函数分别对空值、空字符、空列表、空元组、空字典（或者集合）进行转换时结果都为False。

这里要注意，bool("False")的结果是True，因为"False"是一个不为空的字符串，当被转换成bool类型之后，就得到True。bool("")的结果是True，因为一个空格也不能算作空字符串。

3.3.4 各种类型转字符串

>>> str(19)
'19'
>>> str(0)
'0'
>>> str(True)
'True'
>>> str(False)
'False'
>>> str("12.a")
'12.a'

各种类型转换为字符串比较简单，都是直接变成对应的字符串，注意布尔型不是变成"1"和"0"。

3.4 制作计算器
--------------

3.4.1 预备知识

计算器是现代人发明的可以进行数字运算的电子机器。现代的电子计算器能进行\ `数学运算的手持电子机器，如图3-1所示，拥有集成电路芯片，但结构比电脑简单得多，可以说是第一代的电子计算机(电脑)，且功能也较弱，但较为方便与廉价，可广泛运用于商业交易中，是必备的办公用品之一。计算器从形式来说可以分为两种：1.实物计算器,此类计算器一般是手持式计算器, 便于携带, 使用也较方便；2.软件计算器.此类计算器以软件形式存在,能在PC电脑或者智能手机,平板电脑上使用。
本章我们将从现存简单计算器出发，模拟其功能和特点，在SKIDS开发板上，如图3-2所示，通过屏幕模拟一个软件计算器，界面如图3-3所示，由于SKIDS暂时不支持触摸操作，所以我们用四个物理按键来实现计算器的按键操作功能。


.. image:: /Chapter/picture/image064.png


图3-1 计算器 图3-2 SKIDS开发板 图3-3 计算器界面

3.4.2 任务要求

1. 按图3-3所示画出图形界面；

2. 定义四个按键，实现移动，清零和确定键功能；

3. 能够支持浮点数运算；

4. 能够进行加减乘除运算；

5. 能够输出计算结果到指定屏幕位置；

3.4.3 任务实施

1. 导入相关库

在编写Python程序控制硬件时，往往需要加入硬件相关的库。第1行代码导入了与引脚控制相关的库，第2行代码导入了与时间相关的库，第3行代码导入了与屏幕控制相关的库，第4行代码导入了屏幕显示文字相关的库。
::

   from machine import Pin import time import screen import text

2. 变量定义和初始化

本项目中，首先创建了一个类calculator（计算器类），在该类中定义了一些成员变量，并进行初始化操作。共有三部分类的变量初始化，分别是布局变量，按键变量和计算器变量。创建类的代码如下：
::

   class calculator()

布局变量主要用来定义计算器的屏幕位置、边缘、按钮位置等。self代表计算器本身的类的实例，定义了屏幕的宽度是240，高度是320，边缘是5。值得注意的是，这些数值是与硬件屏幕相关的，要根据具体的LCD屏幕决定数值的大小。注意：这里面的数值单位是像素。
::

   self.screen_width = 240 self.screen_height = 320 self.margin = 5
   self.button_width = (self.screen_width - self.margin \* 7) / 4
   self.button_height = (self.screen_height - self.margin \* 8) / 5

按键变量定义了与按键相关的一些变量，self.keys定义了按键所对应硬件的MCU的IO口线。四个按键分别对应的IO口分别是35，36，39，34。self.keymatch是类中定义的一个列表，用于存储四个物理按键所对应的名称；self.keyboard定义了一个二维列表，用于计算器每个按键的名称；self.keydict定义了一个字典，存储了计算器每个键所对应的数值；最后，定义了画图的起始位置信息。
::

   self.keys = [Pin(p, Pin.IN) for p in [35, 36, 39, 34]]
   self.keymatch = ["Key1", "Key2", "Key3", "Key4"]
   self.keyboard = [[1, 2, 3, 123], [4, 5, 6, 456],[7, 8, 9, 789],[10,0, 11, 12]]
   self.keydict = {1: '1', 2: '2', 3: '3', 123: '+', 4: '4', 5: '5', 6:'6', 456: '-', 7: '7', 8: '8', 9: '9', 789: '×', 10: '.', 0: '0',11:'=', 12: '÷'}
   self.startX = self.margin \* 2
   self.startY = self.margin \* 2 + self.button_height + self.margin
   self.selectXi = 0
   self.selectYi = 0

计算器变量定义了一些标志位，包括操作数1，操作数2，操作符号，操作结果，小数点标记等，代码如下：
::

   self.l_operand = 0 self.r_operand = 0
   self.operator = 123 self.result = 0 self.dotFlag = 0 self.dotLoc = 0

3. 清屏
::

   screen.clear()

4. 画界面

.. image:: /Chapter/picture/image135.jpg

图3-4 界面

计算器界面如图3-4所示：最上面蓝色的长矩形是显示区，用于显示操作的结果。显示区下面的16个绿色小矩形所在区域是按键区，是计算器的虚拟键盘。

LCD显示屏幕是由许多像素点组成的，每个像素点都有对应的坐标值。左上角为坐标原点（0，0），X轴向右为正方向，Y轴向下为正方向。这里面定义了一个边缘的变量margin的值是5。按键区与屏幕边缘距离是margin\*2个像素。因此，显示区蓝色矩形的左上角和右下角的坐标分别是（self.margin\* 2，self.margin \* 2）和（self.screen_width - self.margin \*2，self.margin \* 2 +self.button_height）。通过调用画矩形函数self.drawRect()，实现矩形的绘制。

同理，按键区16个绿色矩形，分别确定左上角和右下角的坐标，然后利用循环嵌套，调用画矩形函数self.drawRect()实现界面的绘制功能，示例代码如下：
::

   def drawInterface(self):
   # 显示框
      x1 = self.margin \* 2
      y1 = self.margin \* 2
      x2 = self.screen_width - self.margin \* 2
      y2 = self.margin \* 2 + self.button_height
      self.drawRect(x1, y1, x2, y2, 2, 0x00ffff)
      # 16个按键
      for i in range(4):
         y = self.startY + i \* (self.button_height + self.margin)
      for j in range(4):
         x = self.startX + j \* (self.button_width + self.margin)
         self.drawRect(x, y, x + self.button_width, y + self.button_height, 2,0x00ff00)

画矩形函数drawRect( )利用直线画出矩形，是为画界面函数服务的。drawRect()通过调用drawline()函数实现矩形的绘制，绘制前要确定直线起点和终点的坐标。画矩形的函数示例代码如下：
::

   def drawRect(self, x1, y1, x2, y2, lineWidth, lineColor):
      x = int(x1)
      y = int(y1)
      w = int(x2 - x1)
      h = int(y2 - y1)
      screen.drawline(x, y, x + w, y, lineWidth, lineColor)
      screen.drawline(x + w, y, x + w, y + h, lineWidth, lineColor)
      screen.drawline(x + w, y + h, x, y + h, lineWidth, lineColor)
      screen.drawline(x, y + h, x, y, lineWidth, lineColor)

5. 显示键盘字符

界面图形完成后，就要进行数字的编码。利用循环嵌套，分别读取keyboard[]列表里对应的值，并计算各个矩形中心的坐标，利用text.draw()函数，在LCD屏幕上显示出键盘上的数字。屏幕显示文字的函数定义如下：

定义：text.draw(str, x, y, textColor, bgColor)

参数说明：待输出的字符串、横坐标、纵坐标、文字颜色、背景颜色。

示例代码如下：
::

   def showKeyboard(self):
      for i in range(4):
         for j in range(4):
            num = self.keyboard[j][i]
            x = i \* (self.button_width + self.margin) + 28
            y = (j + 1) \* (self.button_height + self.margin) + 30
            text.draw(self.keydict[num], int(x), int(y), 0x000000, 0xffffff)

6. 按键事件的处理

1）按键定义，如图3-5所示。

.. image:: /Chapter/picture/image066.png

图3-5 按键定义

.. image:: /Chapter/picture/image067.png
.. image:: /Chapter/picture/image068.jpg
图3-6 按键对应的MCU引脚 图3-7 按键外围电路

SKIDS开发板上一共有四个按键，在程序中分别命名为key1，key2，key3，key4。分别对应MCU的第4，5，6，7引脚，如图3-6所示，相关代码如下：
::

   self.keys = [Pin(p, Pin.IN) for p in [35, 36, 39, 34]]
   self.keymatch = ["Key1", "Key2", "Key3", "Key4"]

self.keys是计算器类中定义的一个列表，里面存放了四个按键在按下或抬起时所对应的MCU端口号。在这里，电路设计成按下时值为“0”，抬起时值为“1”。self.keymatch是计算器类中定义的一个匹配列表，当按下相应的键时，将与列表中某个值相匹配，从而进行相应的操作，按键外围电路如图3-7所示。

2）按键的扫描

当某个按键被按下时，需要被系统及时的捕捉到，并对按键事件进行处理。在这里采用的是轮循的方式，利用一个无限循环，不断的扫描各个按键所对应的引脚电压值，当某个按键被按下，电压值变为“0”，即可被检测到，并进行相应的处理。扫描关键代码如下：
::

   while True:
      i = 0
      j = -1
      for k in self.keys:
         if (k.value() == 0):
            if i != j:
               j = i
               self.keyboardEvent(i)
               i = i + 1
               if (i > 3):
               i = 0

在while循环中，首先定义了两个变量i，j。变量j用于存储上一次是哪一个按键被按下，初值分别为-1。变量i的值会在0-3之间不断的循环，分别用来对应四个按键，初值分别为0。变量k用于循环地检测四个引脚的输入值，当某个按键按下后，j的值被替换为现在被按下的值。同时，启动keyboardEvent(i)函数，通过变量i，来决定用哪个事件处理函数去处理该事件。

3）横向移动按键事件的处理

横向移动所对应的铵键为key1，当上面的扫描值i=0时，通过查找self.keymatch[i]列表，就可以确定执行哪个事件处理函数。需要注意的是变量i，在程序中会传值给变量k。
::

   if self.keymatch[i] == "Key1": # 取消前一个选择 
      num =self.keyboard[self.selectYi][self.selectXi] x = self.selectXi \*(self.button_width + self.margin) + self.startX y =      self.selectYi \*(self.button_height + self.margin) + self.startY self.drawRect(x, y,x + self.button_width, y + self.button_height, 2, 0x00ff00) #选择右边一个 
   self.selectXi = (self.selectXi + 1) % 4 num =self.keyboard[self.selectYi][self.selectXi] x = self.selectXi \*(self.button_width + self.margin) + self.startX self.drawRect(x, y, x+ self.button_width, y + self.button_height, 2, 0xff0000)

横向按键的处理主要分成两个步骤：首先应取消前一个选择键。因为前一个按键被选择时，会在屏幕上对应的计算器按键周围画一个红色方框，用来表示这个按键被选中，因此在按键横向移动后，要在屏幕上用绿色方框取代原来被选中的按键的红色方框，把原来的红色方框覆盖掉。self.keyboard是类中的一个列表，定义了计算器各个键的键名字，是一个二维的形式，self.selectYi和self.selectXi分别记录了要取消的键当前在二维列表中的脚标，并把当前所对应的键名存放到变量num中。在这里面，初始的脚标是0，所以对应到计算器键盘中的数字“1”。变量x，y会根据当前数字键所对应列表中的脚标，计算出当前方框的左上角和右下角的屏幕坐标，并重新在屏幕上画一个绿色方框，覆盖掉原来代表选中的红色方框，来实现“取消选中”的功能。

其次，要在屏幕上新选中的计算器按键周围画红色方框，表示这个按键被选中。先计算出当前按键在列表中的坐标，由于是右移，所以横坐标加1，纵坐标不变。num依然存储了当前的键名，根据坐标列表，计算右移后的左上角和右下角坐标，并利用self.drawRect()函数画出红色方框，代表该按键被选中。

同理，横向移动所对应的铵键为key2，取消选中与重新选中的方式与按键key1相同，仅仅是参数略有差异，不再赘述。

4) 确认按键事件的处理

确认按键用于选定按键数值和运算符号，内容在字典self.keydict中进行了定义。在选中两个操作数和一个运算符号后，选择“=”，即可在显示区看到计算结果。主要代码如下：
::

   elif self.keymatch[key] == "Key3":
   num = self.keyboard[self.selectYi][self.selectXi] self.sendData(num)
   # 清空显示区 
   x = self.margin \* 3 y = self.button_height -self.margin \* 3 text.draw(' ', int(x), int(y), 0x000000, 0xffffff) 
   #显示结果 
   results = str(self.result) length = len(results) if length>= 13: length = 13 x = self.screen_width - self.margin \* 3 - 16 \*length y = self.button_height - self.margin \* 3
   text.draw(results[0:13], int(x), int(y), 0x000000, 0xffffff)

该部分事件处理函数分三个步骤进行：

步骤1：获取当前计算器键盘中的键，并发送给变量num，由sendData(num)函数处理计算结果。如果num的值是0-9的数，进行操作数的赋值，如果num的值是运算符号，把之前右操作数的值赋值给左操作数，然后等待再一次给右操作数赋值，并完成运算操作。这部分的代码包括两个方法的调用，分别是sendData()函数和calculate()函数。
::

   # 计算器四则运算
   def calculate(self, op1, ope, op2):
      if self.keydict[ope] == '+':
         res = op1 + op2
      elif self.keydict[ope] == '-':
         res = op1 - op2
      elif self.keydict[ope] == '×':
         res = op1 \* op2
      elif self.keydict[ope] == '÷':
         res = op1 / op2
      else:
         res = op2
      return res
   # 计算器算法
   def sendData(self, num):
   # 数字0-9
      if num < 10:
         if self.operator == 11:
            self.r_operand = 0
            self.operator = 123
            if self.dotFlag == 0:
               self.r_operand = self.r_operand \* 10 + num
            else:
               self.dotLoc = self.dotLoc + self.dotFlag
               self.r_operand = self.r_operand + num / (10 \*\* self.dotLoc)
               self.result = self.r_operand
            # 小数点.
         elif num == 10:
            if self.dotFlag == 0:
               self.dotFlag = 1
   # 等号=
         elif num == 11:
            self.dotFlag = 0
            self.dotLoc = 0
            self.r_operand = self.calculate(self.l_operand, self.operator,
            self.r_operand)
            self.l_operand = 0
            self.operator = num
            self.result = self.r_operand
            # 运算符+-*/
         elif num > 11
            self.dotFlag = 0
            self.dotLoc = 0
            self.l_operand = self.calculate(self.l_operand, self.operator,
            self.r_operand)
            self.r_operand = 0
            self.operator = num
            self.result = self.l_operand
         else:
            print('input error')

步骤2：清空显示区，首先确定显示部分的坐标，然后调用text.draw(
)函数对该区域进行清除。

步骤3：最后，将计算结果result进行显示，详见案例代码。

.. _本章小结-2:

3.5 本章小结
------------

本章首先讲述了Python中关于数字、数据类型、数据运算及数据类型转换等基础知识，使读者具备了一定的Python编程基础知识。然后以一个项目设计计算器为例，讲述了设计计算器的思路，过程以及实现过程。通过本章学习，达到巩固基础知识，并进一步提高实践能力，为后面列表、字典以及类的学习打下了一定的基础。

.. _练习题目-2:

3.6 练习题目
------------

1.
在LCD屏幕上设计一个十字路口的交通信号灯，利用上下按键实现南北方向的倒计时控制，利用左右按键实现东西方向的倒计时控制。
