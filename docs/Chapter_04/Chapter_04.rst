第4章 制作猜拳游戏
=========

4.1 认识分支结构
----------------

前面所学习的程序都是顺序结构，程序在执行时是一句句往下运行的。这种一句句顺序执行的语句是程序中第一种类型的顺序结构语句。

程序结构除了这种简单的顺序结构外，还有一种会转弯的分支结构，它可以根据执行条件来决定该执行哪些语句，不该执行哪些语句，分支语句是程序中的第二类语句，又称为条件语句。

所谓的分支，其实就是一种判断，指的是只有满足某些条件，才允许做某件事情，而不满足条件时，是不允许做的。例如，现实生活中，过马路要看红绿灯，如果是绿灯才能过马路，否则需要停止等待。其实，不仅生活中需要判断，在程序开发中，也经常会用到判断，例如，用户登录的时候，只有用户名和密码全部正确，才被允许登录，否则就会提示登录错误信息。

4.1.1 单分支结构

举个生活中的例子，我们早上去学校，天气是晴天，我们直接出门。如果是下雨天，我们出门前需要带把雨伞。雨天就会把我们的日常生活打乱。

按照题目描述，先用伪代码实现，大致思路如下：
::

    起床

      吃早餐

      出门前准备

      if 天气是下雨天:
   
      带伞

      出门

当我们起床、吃早餐、出门前准备三步都执行完时候，我们需要对天气进行判断，当天气是下雨天的时候，我们执行带伞操作，执行完以后跳出了分支结构，继续执行最后的出门（总共5步操作）。如果天气不是下雨天，那么我们就跳过分支结构，直接执行分支结构后面的出门（总共4步操作）。

4.1.2 二分支结构

举个生活中的例子，我们去ATM机取款时，在插入银行卡后，机器上会提示用户输入银行卡的密码。如果密码输入正确，则系统进入业务办理主界面。否则，系统会提示用户密码输入错误的信息。

按照题目描述，先用伪代码实现，大致思路如下：
::

   插入银行卡
   输入密码
   if 密码正确:
        业务主界面
   else:
        密码输入错误提示
   取回银行卡

当我们在ATM机器上插入银行卡后，根据界面提示输入银行卡的密码以后，系统会对输入的密码进行校验，当密码输入正确时，则执行进入业务主界面操作，执行完以后跳出了分支结构，继续执行取回银行卡。如果密码输入错误时，则会执行密码输入错误提示操作。若此时用户忘记了银行卡的密码，最后只能执行取回银行卡的操作。

4.1.3 多分支结构

举个生活中的例子，在某些情况下，我们需要将学生的考试成绩转换成等级的形式存入数据库。比如，考试成绩在90-100分之间的，输出等级为“A”，考试成绩在80-89分之间的，输出等级为“B”，考试成绩在70-79分之间的，输出等级为“C”，考试成绩在60-69分之间的，输出等级为“D”，考试成绩在60以下的，输出等级为“E”。

按照题目描述，先用伪代码实现，大致思路如下：
::

   输入考试成绩
   if 成绩在90-100:
        等级为“A”
   elif 成绩在80-89:
        等级为“B”
   elif 成绩在70-79:
        等级为“C”
   elif 成绩在60-69:
        等级为“D”
   elif 成绩在0-59:
        等级为“E”
   保存数据库

当我们输入学生考试成绩后，系统将根据输入的成绩自动转换成相应的等级，并存入数据库中。当用户输入的考试成绩在90-100分之间，则会执行第一个分支，将等级“A”写入数据库中，当输入的成绩在80-89分之间，则会执行第二个分支，将等级“B”写入数据库，此次类推，当输入的成绩在0-59分之间，则会执行最后一个分支，将等级“E”写入数据库，最后执行保存数据库的操作。

4.2 认识逻辑表达式
------------------

在程序开发中，执行结果有时可能和多个条件相关联。比如在多个条件都成立时才能执行，或者有一个条件成立就可执行，这时候就需要使用逻辑运算符。

4.2.1 逻辑运算符

逻辑运算符常用来表示日常交流中的“并且”“或者”“除非”等思想。逻辑运算符可以把多个条件按照逻辑进行连接，从而变成更加复杂的条件。Python中的逻辑运算符主要有与（and）、或（or）、非（not）3种。这三种运算的关系如表4-1所示。

表4-1 逻辑运算符

+--------+---------+-------------------------------------------------------------+
| 运算符 | 举例    | 说明                                                        |
+--------+---------+-------------------------------------------------------------+
| and    | a and b | 二元运算，仅当a、b两者都为True时结果才为True，不然为False   |
+--------+---------+-------------------------------------------------------------+
| or     | a or b  | 二元运算，只要a、b两者之一为True，结果就为True，不然为False |
+--------+---------+-------------------------------------------------------------+
| not    | not a   | 一元运算，当a为True时，结果为False；                        |
|        |         |                                                             |
|        |         | 当a为False时，结果为True                                    |
+--------+---------+-------------------------------------------------------------+

为了便于大家更好地理解逻辑运算符，接下来通过实例演示Python逻辑运算符的操作，如例4-1所示。

【案例4-1】 逻辑运算符。

1. 定义一个整数变量 age，要求人的年龄在0-120之间。
::

   age>=0 and age<=120

2. 定义两个整数变量 python_score、c_score，要求只要有一门成绩>60分就算合格。

::

   python_score>60 or c_score>60

3. 定义一个布尔型变量 is_employee，判断是否是本公司员工，如果不是提示不允许入内。

::

   not is_employee

在and、or、not这3种运算中，非运算not级别最高，and次之，or运算级别最低。例如，逻辑式a
and b or not c中，先运算not c，之后运算a and b，最后才运算or。

优先级别（从低到高）：or------>and------>not。

4.2.2 逻辑表达式

逻辑运算常常与关系运算相结合，形成逻辑运算表达式。逻辑表达式的值是一个逻辑值，即“True”或“False”。在Python编译系统中，判断一个量是否为“真”时，以0表示“假”，以非0表示“真”。

在逻辑表达式中，关系运算要先于逻辑运算，例如：
::

   1. a+b>c and a+c>b and b+c>a；

只有当a+b>c，同时a+c>b，同时b+c>a这3个条件都成立时，表达式的结果才为True。
::

   2. a>b or a>c;

只要a>b与a>c中的任意一个条件成立，表达式的结果就为True。
::

   3. not a or b>c;

只要not a为True（即a为False）与b>c之一成立，结果就为True。

【案例4-2】 逻辑表达式应用。

1. 判断一个整数n是否为偶数。

分析：n是否为偶数，只需要看它除以2的余数是否为0，因此：

若n%2==0，则n是偶数；

若n%2!=0，则n不是偶数，是奇数。

2. 判断年份y是否为闰年。

分析：根据年历知识，年份y是否为闰年的条件是下列条件之一成立：

   1) 年份可被4整除，同时不能被100整除。
   2) 年份可被400整除。

因此，年份y是否是闰年的条件，可以通过以下逻辑表达式来进行判定：
::

   (y%4==0)and(y%100!=0)or(y%400==0)

若表达式的值为True，则年份y为闰年，若值为False，则年份y为非闰年。

3. 判断一个变量c是否为小写字母。

分析：变量c是否是小写，就要看它是否在“a”~“z”之间，由于Unicode码中小写字母的值是连续的，因此只要满足c>=“a”and
c<=“z”,则变量c就是小写字母。注意：这里不能写成“a”<=c<=“z”的形式，这种形式是数学中的表达方式，在Python程序中不支持连续不等式的写法。

4.3 条件判断语句
----------------

Python条件语句是通过一条或多条语句的执行结果（True或者False）来决定执行的代码块。可以通过图4-1来简单了解条件语句的执行过程。

.. image:: /Chapter/picture/image069.png

图4-1 条件语句执行过程

当条件成立（True）时，执行后面的条件代码块，若条件不成立（False）时，则会跳过条件代码块，转而执行后面的语句。

4.3.1 条件语句

简单条件的格式有以下几种。

◆格式1
::

   if 条件：
     语句

其中条件后面有“:”号，执行的语句要向右边缩进。这种格式的含义是当条件成立（True）时，便执行指定的语句，执行完后接着执行if后下一条语句；如果条件不成立，则该语句不执行，转去if后的下一条语句，如图4-2所示。


.. image:: /Chapter/picture/image070.png


图4-2 if语句的执行流程

第1种格式中“语句”一般只有一条语句，if语句也是一条语句，它在一行写完。第2种格式的“语句”可以是一条语句或多条语句，这样形成一个语句块。

◆格式2
::

   if 条件：
     语句1
   else:
     语句2

它的含义是当条件成立（True）时，便执行指定的语句1，执行完后接着执行if后的下一条语句；如果条件不成立（False）时，则执行指定的语句2，执行完后接着执行if后的下一条语句，程序流程如图4-3所示。其中“语句1”与“语句2”都可以是语句块。

.. image:: /Chapter/picture/image071.png


图4-3 if-else语句的执行流程

其中else后面有“:”号，语句1、语句2都向右边缩进，而且要对齐。一般语句1、语句2都可以包含多条语句。

【案例4-3】比较两个数的大小。

分析：这是求两个数中最大值的问题，假设输入的数为a与b，当a>b时，最大值是a，否则为b。
::

    a = input(“a=”)
    b = input(“b=”)
    a = float(a)
    b = float(b)
    if a>b :
        c = a
    else:
        c = b
    print(c)

◆格式3
::

   if 条件1：
     语句1
   elif 条件2:
     语句2
   ……
   elif 条件n:
     语句n
   else:
     语句n+1

它的含义当条件1成立时，便执行指定的语句1，执行完后，接着执行if后的下一条语句；如果条件1不成立，则判断条件2，当条件2成立时，执行指定的语句2，执行完后，接着执行if后的下一条语句；如果条件2不成立，则继续判断条件3，以此类推，判断条件n，如果成立，执行语句n，接着执行if后的下一条语句；如条件n还不成立，则最后只有执行语句n+1，执行完毕后，接着执行if后的下一条语句。程序流程图如图4-4所示。

.. image:: /Chapter/picture/image072.png

图4-4 if-elif语句的执行流程

其中每个条件后有“:”号，语句1、语句2、…语句n+1等都向右边缩进，而且要对齐。一般语句1、语句2、……都可以包含多条语句。

elif是else
if的缩写。if语句执行有个特点，它是从上往下判断，如果程序中判断条件很多，全部用if的话，会遍历整个程序，而使用elif语句后程序在运行时，只要if条件或者后续某一个elif条件满足逻辑值为True，则程序执行完对应语句后自动结束本轮if-elif判断，不会再去冗余地执行后续的elif或else语句，从而提高了程序的整体运行效率。

【案例4-4】输入一个学生的整数成绩m，按[90,100]、[80,89]、[70,79]、[60,69]、[0,59]的范围分别给出A、B、C、D、E的等级。

分析：输入的成绩可能不合法（小于0或者大于100），也可能在[90,100]、[80,89]、[70,79]、[60,69]、[0,59]的其中一段之内，可以用负责分支的if-elif语句来处理。
::

   score = input(“Enter mark:”)
   if score<0 or score>100:
        print(“Invalid”)
   elif score>=90 and score<=100:
        print(“A”)
   elif score>=80 and score<=89:
        print(“B”)
   elif score>=70 and score<=79:
        print(“C”)
   elif score>=60 and score<=69:
        print(“D”)
   elif score>=0 and score<=59:
        print(“E”)

当然，if-elif语句可以和else语句一起使用。在上面的例子中，也可以将最后0~59分的条件判断，直接改成else判断。

【案例4-5】输入0~6的整数，并把它作为星期，其中0对应星期日，1对应星期一，以此类推，最终在屏幕上输出Sunday，Monday，Tuesday，Wednesday，Thursday，Friday，Saturday。

分析：假设输入的整数为w，根据w的值可以用if-elif-else语句分为多种情况，当输入的值不在0~6范围内，直接输出“Error”。
::

   w = input(“w=”)
   w = int(w)
   if w==0:
        s = “Sunday”
   elif w==1:
        s = “Monday”
   elif w==2:
        s = “Tuesday”
   elif w==3:
        s = “Wednesday”
   elif w==4:
        s = “Thursday”
   elif w==5:
        s = “Friday”
   elif w==6:
        s = “Saturday”
   else:
         s = “Error”
         print(s)

4.4 条件语句的嵌套使用
----------------------

if嵌套指的是在if或者if-else语句里面包含if或者if-else语句。其嵌套的格式如下：
::

    if 条件1：
        满足条件1做的事情1
        满足条件1做的事情2
        …（省略）…   
        if 条件2:
            满足条件2做的事情1
            满足条件2做的事情2
            …（省略）…

上述格式中，外层的if和内层的if判断，到底使用if语句还是if-else语句，我们可以根据实际开发的情况进行选择。

4.4.1 if嵌套

例如，当我们乘坐火车或者地铁时，必须得先买票，只有买到票，才能进入车站进行安检，只有安检通过了才可以正常乘车。在乘坐火车或者地铁的过程中，后面的判断条件是在前面的判断成立的基础上进行的，针对这种情况，可以使用if嵌套来实现。
::

   ticket = 1 #用1代表有车票，0代表没有车票
   knifeLength = 0 #刀子的长度，单位为cm
   if ticket == 1:
        print(“有车票，可以进站”)
        if knifeLength < 10:
            print(“通过安检”)
            print(“终于可以见到Ta了，美滋滋~~~”)
        else:
            print(“没有通过安检”)
            print(“刀子的长度超过规定，等待警察处理…”)
   else:
        print(“没有车票，不能进站”)
        print(“亲爱的，那就下次见了，一票难求啊~~~~(>_<)~~~~”)

1. 假设ticket = 1 、knifeLength = 9，程序的运行结果如图4-5所示。

.. image:: /Chapter/picture/image073.jpg

图4-5 ticket = 1，knifeLength = 9的运行结果

2. 假设ticket = 1 、knifeLength = 20，程序的运行结果如图4-6所示。

.. image:: /Chapter/picture/image074.jpg

图4-6 ticket = 1，knifeLength = 20的运行结果

3. 假设ticket = 0 、knifeLength = 9，程序的运行结果如图4-7所示。

.. image:: /Chapter/picture/image075.jpg

图4-7 ticket = 0，knifeLength = 9的运行结果

4. 假设ticket = 0 、knifeLength = 20，程序的运行结果如图4-8所示。

.. image:: /Chapter/picture/image076.jpg

图4-8 ticket = 0，knifeLength = 20的运行结果

【案例4-6】输入a、b、c三个参数，求解ax\ :sup:`2`\ +bx+c=0的方程的根。

分析：根据数学知识，只有当a不为0时，才满足该方程为一元二次方程，然后再判断Δ的值，如果b\ :sup:`2`-4ac>0，则方程有两个不相等的实数根，.. image:: /Chapter/picture/image077.png，如果b\ :sup:`2`-4ac=0，则方程有两个相等的实数根，x1
= x2 = .. image:: /Chapter/picture/image078.png ，如果b\ :sup:`2`-4ac<0，则方程无实数根。
::

   import math
   a = input(“a=”)
   b = input(“b=”)
   c = input(“c=”)
   a = float(a)
   b = float(b)
   c = float(c)
   if a!=0:
        d = b*b-4*a*c
   if d>0:
        d = math.sqrt(d)
        x1 = (-b+d) / 2 / a
        x2 = (-b-d) / 2 / a
        print(“x1=”,x1, “x2=”,x2)
   elif d==0:
        print(“x1,x2=”,-b/2/a)
   else:
        print(“无实数解”)
   else:
        print(“不是一元二次方程！”)
   
程序运行结果：
::

   a = 1
   b = 2
   c = 1
   x1,x2= -1.0

.. image:: /Chapter/picture/image079.jpg

图4-9 石头、剪刀、布

4.5 制作猜拳游戏
----------------

相信大家都玩过猜拳游戏，通过不同的手势分别表示“石头、剪刀、布”。在游戏规则中，石头胜剪刀，剪刀胜布，布胜石头，如图4-9所示。

猜拳游戏跟“掷硬币”、“掷骰子”的原理类似，就是用产生的随机结果来作决策。在游戏中，用户通过按下Skids开发板上不同的按键来表示不同的手势，分别代表石头、剪刀或布；而电脑从“石头、剪刀、布”三者中随机选择一个手势，和用户的手势进行对比，从而确定最终的胜负情况。

4.5.1 预备知识

我们模拟一个用户和计算机进行猜拳比赛，比赛的流程如图4-10所示。

具体流程为：

1. 程序启动后，首先进行硬件初始化，主要是对显示屏和按键进行设置。

2. 完成硬件初始化后，进入一个无限循环中，等待用户按键操作。

3. 当用户按下按键后，判断是否为结束按键；如果是，则结束游戏；如果不是，则获取用户输入的手势信息，同时为计算机随时生成一个手势，和用户输入进行对比，确定胜负关系。

4. 更新界面显示。

5. 等待用户的下一次按键操作。

.. image:: /Chapter/picture/image080.png

图4-10 猜拳游戏流程图

4.5.2 任务要求

为了保证能有较好的用户体验，精心设计了猜拳游戏界面，效果如图4-11所示。

.. image:: /Chapter/picture/image081.jpg

图4-11 猜拳游戏界面

游戏界面中所罗列的按键1~按键4分别对应Skids开发板上的4个物理按键，具体排列顺序如图4-12所示。其中，右侧按键为“按键1”，下方的按键为“按键2”，左侧按键为“按键3”，上方的按键为“按键4”。每个按键分别代表“剪刀”、“石头”、“布”以及“结束”，具体的对应关系也可通过程序进行设置。

.. image:: /Chapter/picture/image082.png

图4-12 Skids开发板的按键

游戏界面主要分为三个区域：

1. 最顶部的区域显示游戏规则和操作说明。

2. 间区域显示每次猜拳的情况，包括玩家手势、电脑手势和胜负结果。玩家手势通过不同的按键来表示。

3. 最下面的区域显示游戏胜负情况的汇总结果。

4.5.3 任务实施

1. 硬件初始化

通过类的构造函数，从而实现对硬件（屏幕显示和按键设置）进行初始化，同时将游戏的一些统计数据进行清零。
::

   def __init__(self, playerName, computerName):
        #将游戏的统计数据进行清零
        self.gameStart = False
        self.playerName = playerName
        self.computerName = computerName
        self.playerScore = 0
        self.computerScore = 0
        self.equalNum = 0
        self.playerStatus = 0
        self.playerMessage = ""
        self.computerStatus = 0
        self.computerMessage = ""
        #设置按键数组
        for p in pins:
            keys.append(Pin(p,Pin.IN))
            #初始化屏幕
            self.displayInit()
   
在构造函数__init__()中，调用了displayInit()函数来进行屏幕初始化工作，主要负责完成屏幕顶部的游戏规则和操作说明显示。
::

   def displayInit(self, x=10, y=10, w=222, h=303):#显示游戏规则信息
      mentionStr1 = "游戏规则："
      mentionStr2 = "按键1.剪刀 按键2.石头"
      mentionStr3 = "按键3.布 按键4.结束"
      text.draw(mentionStr1, 20, 20, 0x000000, 0xffffff)
      text.draw(mentionStr2, 20, 36, 0x000000, 0xffffff)
      text.draw(mentionStr3, 20, 52, 0x000000, 0xffffff)
      text.draw("-------------", 20, 68, 0x000000, 0xffffff) #更新界面显示
      self.updateTotolArea()#设置游戏运行状态
      self.gameStart = True

2. 开启游戏

通过类的成员函数startGame()负责启动游戏的主流程，并等待用户的按键操作。
::

   def startGame(self):
      print("-------猜拳游戏开始-------")
   while True:
      i = 0
      j = -1
      for k in keys:
        if(k.value() == 0):
         if i!=j:
            j = i
            self.pressKeyboardEvent(i)
            i = i+1;
         if(i > 3):
            i = 0
   time.sleep_ms(100) #按键防抖

3. 处理用户按键事件

当用户按下按键后，类的成员函数pressKeyboardEvent()负责进行具体的处理。在该函数中，首先判断游戏是否已经开始，如果游戏未开始，则不必处理键盘输入，函数直接返回。该函数是整个程序中最重要的函数，负责完成具体的游戏过程处理。
::

   def pressKeyboardEvent(self, key):
      keymatch=["Key1","Key2","Key3","Key4"]

#游戏还未开始，不必处理键盘输入
::

   if(self.gameStart == False):
      return

一旦监听到用户有输入，则对用户按下的按键进行判断，这里设定按键1代表剪刀、按键2代表石头、按键3代表布，按键4代表游戏结束；用数字1、2、3分别代表剪刀、石头和布。
::

   if(keymatch[key] == "Key1"):
      self.playerStatus = 1
      self.playerMessage = "%s出拳为：剪刀"%self.playerName
      bmp_jiandao.draw(40, 140)
   elif(keymatch[key] == "Key2"):
      self.playerStatus = 2
      self.playerMessage = "%s出拳为：石头"%self.playerName
      bmp_shitou.draw(40, 140)
   elif(keymatch[key] == "Key3"):
      self.playerStatus = 3
      self.playerMessage = "%s出拳为：布 "%self.playerName
      bmp_bu.draw(40, 140)
   else:
      text.draw("游戏结束", 90, 210, 0x000000, 0xffffff)#设置游戏运行状态
      self.gameStart = False
      return

4. 为计算机选择随机数

确定用户的出拳情况后，为计算机选择一个随机数（1~3），分别代表剪刀、石头和布，并作为计算机的出拳情况。
::

   #电脑的出拳为一个随机值
   self.computerStatus = random.randint(1,3)
   print(self.computerStatus)
   if(self.computerStatus == 1):
      self.computerMessage = "%s出拳为：剪刀"%self.computerName
      bmp_jiandao.draw(150, 140)
   if(self.computerStatus == 2):
      self.computerMessage = "%s出拳为：石头"%self.computerName
      bmp_shitou.draw(150, 140)
   if(self.computerStatus == 3):
      self.computerMessage = "%s出拳为：布 "%self.computerName
      bmp_bu.draw(150, 140)
   #显示电脑和玩家的出拳信息
      text.draw(self.playerMessage, 20, 84, 0x000000, 0xffffff)
      text.draw(self.computerMessage, 20, 100, 0x000000, 0xffffff)

5. 判断胜负情况

确定了用户和计算机的出拳后，对胜负情况进行判断，并记录结果。
::

   #判断胜负并显示结果
   resultMessage = " 平局 "
   #出拳相同，为平局
   if(self.playerStatus == self.computerStatus):
      self.equalNum+=1 #平局次数加1
   #用户剪刀、计算机布，用户胜
   elif(self.playerStatus==1 and self.computerStatus==3):
      resultMessage = "%s胜出"%self.playerName
      self.playerScore+=1 #用户获胜次数加1
   #用户石头、计算机剪刀，用户胜
   elif(self.playerStatus==2 and self.computerStatus==1):
      resultMessage = "%s胜出"%self.playerName
      self.playerScore+=1
   #用户布、计算机石头，用户胜
   elif(self.playerStatus==3 and self.computerStatus==2):
      resultMessage = "%s胜出"%self.playerName
      self.playerScore+=1
   else: #其它情况，计算机胜
      resultMessage = "%s胜出"%self.computerName
      self.computerScore+=1 #计算机获胜次数加1
   #更新界面显示
      text.draw(resultMessage, 90, 210, 0x000000, 0xffffff)
      self.updateTotolArea()

6. 更新界面显示

在游戏界面的汇总区域，计算并显示电脑和用户玩家的胜平负次数。
::

   def updateTotolArea(self):
     #汇总区域用于显示电脑和玩家的胜平负次数
     print("-------更新汇总区域--------")
     playerTotal = "%s赢了%d局" % (self.playerName, self.playerScore)
     computerTotal = "%s赢了%d局" % (self.computerName, self.computerScore)
     equalTotal = "平局%d次" % self.equalNum
     text.draw("-------------", 20, 240, 0x000000, 0xffffff)
     text.draw(playerTotal, 20, 256, 0x000000, 0xffffff)
     text.draw(computerTotal, 20, 272, 0x000000, 0xffffff)
     text.draw(equalTotal, 20, 288, 0x000000, 0xffffff)

7. 完整程序

在Skids开发板上实现猜拳游戏的完整代码如下所示：
::

   from machine import Pin
   import random
   import time
   import screen
   import ubitmap
   import text
   #清除屏幕显示
   screen.clear()
   #定义图片文件
   bmp_shitou = ubitmap.BitmapFromFile("shitou")
   bmp_jiandao = ubitmap.BitmapFromFile("jiandao")
   bmp_bu = ubitmap.BitmapFromFile("bu")
   #定义Skids开发板的按键引脚数组
   pins = [36,39,34,35]
   keys = []
   class Game():
      def __init__(self, playerName, computerName):
         self.gameStart = False
         self.playerName = playerName
         self.computerName = computerName
         self.playerScore = 0
         self.computerScore = 0
         self.equalNum = 0
         self.playerStatus = 0;
         self.playerMessage = ""
         self.computerStatus = 0
         self.computerMessage = ""
         for p in pins:
            keys.append(Pin(p,Pin.IN))
            self.displayInit()
      def displayInit(self, x=10, y=10, w=222, h=303):
   #显示游戏规则信息
         mentionStr1 = "游戏规则："
         mentionStr2 = "按键1.剪刀 按键2.石头"
         mentionStr3 = "按键3.布 按键4.结束"
         text.draw(mentionStr1, 20, 20, 0x000000, 0xffffff)
         text.draw(mentionStr2, 20, 36, 0x000000, 0xffffff)
         text.draw(mentionStr3, 20, 52, 0x000000, 0xffffff)
         text.draw("-------------", 20, 68, 0x000000, 0xffffff)
         self.updateTotolArea()
   #设置游戏运行状态
         self.gameStart = True
      def pressKeyboardEvent(self, key):
         keymatch=["Key1","Key2","Key3","Key4"]
   #游戏还未开始，不必处理键盘输入
      if(self.gameStart == False):
         return
         print(keymatch[key])
         if(keymatch[key] == "Key1"):
            self.playerStatus = 1
            self.playerMessage = "%s出拳为：剪刀"%self.playerName
            bmp_jiandao.draw(40, 140)
         elif(keymatch[key] == "Key2"):
            self.playerStatus = 2
            self.playerMessage = "%s出拳为：石头"%self.playerName
            bmp_shitou.draw(40, 140)
         elif(keymatch[key] == "Key3"):
            self.playerStatus = 3
            self.playerMessage = "%s出拳为：布 "%self.playerName
            bmp_bu.draw(40, 140)
         else:
            text.draw("游戏结束", 90, 210, 0x000000, 0xffffff)
   #设置游戏运行状态
            self.gameStart = False
            return
   #电脑的出拳为一个随机值
            self.computerStatus = random.randint(1,3)
            print(self.computerStatus)
      if(self.computerStatus == 1):
         self.computerMessage = "%s出拳为：剪刀"%self.computerName
         bmp_jiandao.draw(150, 140)
      if(self.computerStatus == 2):
         self.computerMessage = "%s出拳为：石头"%self.computerName
         bmp_shitou.draw(150, 140)
      if(self.computerStatus == 3):
         self.computerMessage = "%s出拳为：布 "%self.computerName
         bmp_bu.draw(150, 140)
   #显示电脑和玩家的出拳信息
         text.draw(self.playerMessage, 20, 84, 0x000000, 0xffffff)
         text.draw(self.computerMessage, 20, 100, 0x000000, 0xffffff)
   #判断胜负并显示结果
         resultMessage = " 平局 "
      if(self.playerStatus == self.computerStatus):
         self.equalNum+=1
      elif(self.playerStatus==1 and self.computerStatus==3):
         resultMessage = "%s胜出"%self.playerName
         self.playerScore+=1
      elif(self.playerStatus==2 and self.computerStatus==1):
         resultMessage = "%s胜出"%self.playerName
         self.playerScore+=1
      elif(self.playerStatus==3 and self.computerStatus==2):
         resultMessage = "%s胜出"%self.playerName
         self.playerScore+=1
      else:
         resultMessage = "%s胜出"%self.computerName
         self.computerScore+=1
         text.draw(resultMessage, 90, 210, 0x000000, 0xffffff)
         self.updateTotolArea()
   def startGame(self):
      print("-------猜拳游戏开始-------")
      while True:
          i = 0
          j = -1
         for k in keys:
            if(k.value() == 0):
               if i!=j:
                   j = i
                   self.pressKeyboardEvent(i)
               i = i+1
               if(i > 3):
                   i = 0
               time.sleep_ms(100) #按键防抖
   def updateTotolArea(self):
   #汇总区域用于显示电脑和玩家的胜平负次数
      print("-------更新汇总区域-------")
      playerTotal = "%s赢了%d局" % (self.playerName, self.playerScore)
      computerTotal = "%s赢了%d局" % (self.computerName, self.computerScore)
      equalTotal = "平局%d次" % self.equalNum
      text.draw("-------------", 20, 240, 0x000000, 0xffffff)
      text.draw(playerTotal, 20, 256, 0x000000, 0xffffff)
      text.draw(computerTotal, 20, 272, 0x000000, 0xffffff)
      text.draw(equalTotal, 20, 288, 0x000000, 0xffffff)
    if __name__ == '__main__':
          newGame = Game("玩家", "电脑")
         newGame.startGame()

实践练习：

1. 修改按键的处理规则，将Key4、Key3和Key2分别对应剪刀、石头和布，Key1对应结束游戏。

2. 调整游戏流程：当出现平局的时候，提示让用户重新按下某个按键，并为计算机重新选择一个随机数，再次将两者进行比较，直到分出胜负。

.. _本章小结-3:

4.6 本章小结
------------

在本章节中，主要学习了Python语言中的分支结构，认识了分支结构的多种表现形式。在程序开发中，分支结构主要通过if语句来实现，当分支情况较复杂时，可以借助if-elif-else等语句来实现。

在进行分支选择时，所附加的条件往往需要借助算术运算符、逻辑运算符等，从而形成更复杂的条件判断。

分支结构在Python开发中，经常会碰到，if语句的使用频率非常高，希望读者可以多加以理解，并熟练掌握它们的使用。

.. _练习题目-3:

4.7 练习题目
------------

1. 输入两个整数，判断哪个大并输出结果。

2. 输入a、b、c三个参数，以它们作为三角形的三条边，判断是否可以构成一个三角形，如能则进一步计算其面积。三角形的面积s可以用以下表达式计算：
::

    s = sqrt(p*(p-a)*(p-b)*(p-c))

其中：p = (a+b+c)/2。

3. 输入一个字母，如果它是一个小写英文字母，则把它转换为对应的大写字母输出，如果它是一个大写英文字母，则把它转换为对应的小写字母输出。

4. 输入一个年份，判断它是否为闰年，并输出相关信息。

5. 输入a、b、c三个整数，按照从大到小的顺序输出到屏幕上。

6. 某企业发放的奖金是根据利润提成的。利润低于或等于10万元时，奖金可提12%；利润高于10万元，低于20万元时，高于10万元的部分，可提成8.5%；20万元~40万元之间时，高于20万元的部分，可提成6%；40万元~60万元之间时，高于40万元的部分，可提成4%；60万元~100万元之间时，高于60万元的部分，可提成2.5%；高于100万元时，超过100万元的部分按1%提成，从键盘输入当月利润，求应发放奖金的总数。
