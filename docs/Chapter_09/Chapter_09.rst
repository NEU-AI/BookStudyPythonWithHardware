第9章 网络编程制作表情发送器
=========

9.1 认识网络
------------

21世纪是一个以网络为核心的信息时代。我们无时无刻不在使用着网络，它可以非常迅速地传递信息。网络对社会生活的很多方面以及对社会经济的发展己经产生了不可估量的影响。

9.1.1 互联网概述

计算机网络由多个互连的结点和连接这些结点的链路组成。这些结点是计算机、集线器、交换机或路由器等。而计算机网络之间还可以用路由器连接，构成更大的计算机网络。这样的网络称为互联网。而互联网的核心是一系列的协议，称为“互联网协议”。

9.1.2 网络标准和网络协议

网络协议是为计算机网络中进行数据交换而建立的规则、标准或约定的集合。由于网络节点之间联系的复杂性，在制定协议时，通常把复杂成分分解成一些简单成分，然后再将它们复合起来。最常用的复合技术就是层次方式。不同的协议层次结构不同，目前主流的体系机构是TCP/IP和OSI，他们之间层次的对应关系如图9-1所示。

1. TCP/IP

TCP/IP（Transmission Control Protocol/InternetProtocol）是传输控制协议和网络协议的简称，它定义了电子设备如何连入因特网，以及数据如何在它们之间传输的标准。它是互联网的核心。在应用层中定义了很多面向应用的协议如FTP、TFTP、HTTP、SMTP、DHCP、Telnet、DNS和SNMP等。在传输层主要有两个协议，TCP和UDP，这些协议负责流量控制，错误校验和排序服务。在网络层中的协议主要有IP、ICMP、IGMP、ARP和RARP等，这些协议处理信息的路由和主机地址解析。

2. OSI协议

开放式系统互联通信参考模型（Open System Interconnection ReferenceModel，缩写为OSI），简称为OSI模型。OSI是七层体系结构，概念清晰，理论完整，但它即复杂又不实用。现在广泛使用的是TCP/IP体系结构，它是一个四层的体系结构,它包含应用层、运输层、网际层和网络接口层。不过从实质上讲，TCP/IP只有最上面的三层，因为最下面的网络接口层并没有什么具体内容，因此往往采取折中的办法，即综合OSI和TCP/IP的优点，采用一种只有五层协议的体系结构，这样既简洁又能将概念阐述淸楚，有时为了方便，也可把最底下两层称为网络接口层。

.. image:: /Chapter/picture/image123.png

图9-1 层次对应关系

3. IEEE 802

IEEE
802规范定义了网卡如何访问传输介质，以及如何在传输介质上传输数据的方法，还定义了传输信息的网络设备之间建立连接、维护和拆除的途径。IEEE
802 规范主要包括如下内容：

IEEE 802.1 ：局域网体系结构、寻址网络互联和网络。
IEEE 802.2：逻辑链路控制子层（LLC）的定义。
IEEE 802.3：以太网介质访问控制协议（CSMA/CD及物理层技术规范。
IEEE 802.4 ：令牌总线网（Token-Bus）的介质访问控制协议及物理层技术规范。
2.5 ：令牌环网（Token-Ring)的介质访问控制协议及物理层技术规范。
IEEE 802.6 ：城域网介质访问控制协议DQDB （Distributed Queue DualBus分布式队列双总线）及物理层技术规范。
IEEE 802.7 ：宽带技术咨询组，提供有关宽带联网的技术咨询。
IEEE 802.8 ：光纤技术咨询组，提供有关光纤联网的技术咨询。
IEEE 802.9 ：综合声音数据的局域网（IVDLAN）介质访问控制 协议及物理层技术规范。
IEEE 802.10：网络安全技术咨询组，定义了网络互操作的认证和加密方法。
IEEE 802.11 ：无线局域网（WLAN）的介质访问控制协议及物理层技术规范。

9.1.3 网络设备

信息在网络中的传输主要有以太网技术和网络交换技术。而网络交换技术使用的非常普遍。

网络交换是指通过一定的设备将不同的信号或者信号形式转换成对方能识别的信号类型，从而达到通信目的的一种交换形式，通常有数据交换、线路交换、报文交换和分组交换。

在网络互连时各个结点都需要使用一个中间设备相连，这个中间设备要实现不同网络之间的协议转换。这些设备有中继器、网桥、路由器、网卡、集线器、二层交换机、三层交换机和多层交换机。

网卡：安装在计算机上，使计算机连网的硬件设备，如图9-2所示。

中继器：是对信号进行再生和还原的网络设备，主要功能是通过对数据信号的重新发送或者转发，来扩大网络传输的距离。

网桥：是连接两个局域网的一种存储/转发设备，它能将一个大的局域网分割为多个网段，或将两个以上的局域网互联为一个逻辑局域网。

路由器：是网络的主要结点设备，通过路由决定数据的转发。转发策略称为路由选择，这也是路由器名称的由来。作为不同网络之间互相连接的枢纽，路由器系统构成了整个互联网的主体脉络，如图9-3所示。

交换机：负责统一网络内的数据帧的转发，交换机根据数据帧的MAC地址转发至相应的端口，如图9-2所示。

.. image:: /Chapter/picture/image124.jpg
.. image:: /Chapter/picture/image125.jpg

图9-2 网卡及交换机

无线技术已经使用非常广泛，相关的产品有无线网卡、无线AP、无线网桥和无线路由器等。

.. image:: /Chapter/picture/image126.jpg
.. image:: /Chapter/picture/image127.jpg

图9-3 家用路由器和核心路由器

9.2 认识ESP32芯片
-----------------

ESP-WROOM-32(ESP32)是乐鑫最新发布的新一代WiFi&蓝牙双模双核无线通信芯片。如图9-4所示，芯片集成蓝牙4.2和WiFi
HT40技术，拥有高性能Tensilica LX6 双核处理器，支持超低功耗待机。

相比于上一代的ESP8266，除了突破性地集成了低功耗蓝牙4.2 (BLE 4.2)
技术外，ESP32在性能和功能上也有了显著的提升，搭载了双核 32-bit
MCU，一核处理高速连接、一核独立应用开发。双核主频高达 240
MHz，计算能力高达 650 DMIPS。并且芯片拥有更多的管脚资源。

ESP32芯片集成了丰富的硬件外设，如图9-5所示，包括电容式触摸传感器、霍尔传感器、低噪声传感放大器，SD卡接口、以太网接口、高速SDIO／SPI、UART、I2S
和I2C 等。

.. image:: /Chapter/picture/image128.jpg

图9-4 ESP32芯片

.. image:: /Chapter/picture/image129.png

图9-5 芯片原理图

蓝牙和WIFI是ESP32的核心功能，蓝牙和wifi的共存也是esp32的独门武功，通过ESP32进行网络开发是非常好的选择，在ESP32上安装MicroPython固件，可以使用Python语法，运用Python进行简单的网络开发。Skids提供了丰富的Python网络接口，便于开发人员进行网络相关的设计开发。

网络相关接口封装在network库，主要用于WIFI相关的配置和连接，WIFI有两种配置模式，一个用于station（当ESP32连接到路由器时），一个用于热点（accesspoint）（用于其他设备与ESP32连接）。使用以下指令创建这些对象的实例：
::

   import network
   sta_if = network.WLAN(network.STA_IF) #STA模式
   ap_if = network.WLAN(network.AP_IF) #AP模式
   可使用以下指令检查接口是否有效：
   sta_if.active() # Ture表示接口有效，False表示无效
   ap_if.active() # Ture表示接口有效，False表示无效
   可使用以下指令检查接口的网络设置：
   ap_if.ifconfig()
   # 返回值为：IP地址、网络掩码、网关、DNS
   配置WIFI，让Skids可以连接某个热点实现上网的过程如下：
   sta_if = network.WLAN(network.STA_IF) #STA模式
   ap_if = network.WLAN(network.AP_IF) #AP模式
   if ap_if.active(): #如果AP模式开启了，则先关闭
      ap_if.active(False)
      if not sta_if.isconnected():
         print('Connecting to network...')
         sta_if.active(True) #激活STA
         sta_if.connect(wifi_name, wifi_SSID)
         #连接WiFi热点，参数为WiFi的SSID和密码
         while not sta_if.isconnected():
            pass
   
9.3 认识MQTT协议
----------------

MQTT全称Message Queuing Telemetry
Transport(消息队列遥测传输)是一种基于“发布/订阅”范式的“轻量级”消息协议，由IBM发布。

MQTT可以被解释为一种低开销，低带宽的即时通讯协议，可以用极少的代码和带宽为远程设备提供实时可行的消息服务，它适用于硬件性能低下的远程设备以及网络状况糟糕折环境。因此MQTT协议在IoT，小型设备应用，移动应用等方面有广泛的应用。

IoT设备要运作，就必须连接到互联网，设备才能相互协作，以及与后端服务协同工作。而互联网的基础网络协议是TCP/IP，MQTT协议是基于TCP/IP协议栈而构建的，因此它已经慢慢的成为了IoT通讯的标准。

9.3.1 基本特点

MQTT是一种发布/订阅传输协议，基本原理和实现如图9-6所示。

.. image:: /Chapter/picture/image130.jpg

图9-6 基本原理

MQTT协议提供一对多的消息发布，可以解除应用程序耦合，信息冗余小。该协议需要客户端和服务端，而协议中主要有三种身份：发布、代理、订阅者。其中，消息的发布者和订阅者都是客户端，消息代理是服务器，而消息发布者可以同时是订阅者，消息代理机制实现了生产者与消费者的脱耦。

MQTT使用TCP/IP提供网络连续，提供有序、无损、双向连接，并可以对消息订阅者所接收到的内容所屏蔽。

MQTT有三种消息发布的服务质量：

至多一次，消息发布完全依赖底层TCP/IP网络。会发生消息丢失或重复。

至少一次，确保消息到达，但消息重复可能会发生。

只有一次，确保消息到达一次。在一些要求比较严格的系统中会使用此级别，确保用户收到且只会收到一次。

MQTT是一种小型的数据传输协议，由于固定长度的头部是2字节，所以协议交换数据量很小，所耗费的网络流量自然也就很少。

目前各大互联网公司开始进军物联网领域，建立物联网平台，而MQTT是物联网中相当重要的角色，如图9-7所示，MQTT在物联网领域应用广泛。物联网环境下，大量的设备或传感器需要将很小的数据定期发送出去，并接受外部传回来的数据。这样的数据交换是大量存在的。

MQTT通过代理服务器转发消息，所以可以穿透NAT，类似的协议还有AMQP、XMPP等。MQTT协议里面是按照设备一直在线设计的，数据都是保存在内存里的，所以MQTT是比较耗费内存的。

.. image:: /Chapter/picture/image131.jpg

图9-7 物联网应用

9.3.2 基本概念

MQTT传输的消息分为：主题（Topic）和负载（payload）两部分。

MQTT客户端：一个使用MQTT协议的设备、应用程序等，它总是建立到服务器
的网络连接。可以发布消息，其他客户端可以订阅该消息；订阅消息；退订或删除消息。

MQTT服务器：也称为Broker，是一个应用程序或一个设备，它位于发布者和订阅者之间。它接收来自客户端的网络连接；接受客户端发布的应用消息；处理来自客户端的订阅和退订请求；向订阅的客户转发应用程序消息。

主题：连接到一个应用程序消息的标签，该标签与服务器的订阅相匹配。服务器会将消息发送给订阅所匹配标签的每个客户端。

主题筛选器：一个对主题名通配符筛选器，在订阅表达式中使用，表示订阅所匹配到的多个主题。

负载：消息订阅者所具体接收的内容。

MQTT工作流程如图9-8所示，发布者在某个主题上发布消息到服务端，订阅这一主题的订阅者就会收到服务端发送的相同消息。同时订阅者也可以是发布者。

MQTT服务端工作流程：

（1）接受来自客户的网络连接；

（2）接受客户发布的信息；

（3）处理来自客户端的订阅和退订请求；

（4）向订阅的客户转发其已经订阅的消息。

MQTT客户端工作流程：

（1）连接服务端

（2）发布消息，这些消息其他客户端可能会订阅；

（3）订阅其它客户端发布的消息；

（4）退订或删除消息；

（5）断开与服务器连接。

.. image:: /Chapter/picture/image132.jpg

图9-8 基本流程

9.3.3 基本方法

MQTT协议中定义了一些方法（也被称为动作），用来表示对确定的资源所进行的操作。这个资源可以是预先存在的数据也可以是动态生成的数据。这些资源一般是服务器上的文件或输出。主要方法有：

1. Connect：等待与服务器建立连接。
2. Disconnect：等待MQTT客户端完成所做的工作，并与服务器断开TCP/IP会话。
3. Subscribe：等待完成订阅。
4. UnSubscribe：等待服务器取消客户端的一个或多个topics（主题）订阅。
5. Publish：MQTT客户端发送消息请求，发送完成后返回应用程序线程。

9.3.4 MQTT协议数据包结构

在MQTT协议中，一个MQTT数据包由：固定头（Fixed header）、可变头（Variableheader）、负载（payload）三部分构成。MQTT数据包结构如下：

+-----------------------+-----------------------+-----------------------+
| **固定报头（fixed     | **可变报头（variable  | **负载（payload）**   |
| header）**            | header）**            |                       |
+-----------------------+-----------------------+-----------------------+
| 所有报文都包含        | 部分报文包含          | 部分报文包含          |
+-----------------------+-----------------------+-----------------------+

固定报头：长度8
bit，高4位是数据包类型如图9-9所示，低4位标识位。固定头的第二个字节是剩余长度用来保存变长头部和消息体的总合大小，但不直接保存。这一字节是可以扩展的，前7位用于保存长度后1位是标识位。当最后1位为1时，表示长度不足，需要另外使用一个字节继续保存。

可变头：它位于固定头和荷载之间，它的内容因数据包的类型不同而不同。比如CONNECT的可变报文头，由4部分组成协议名、协议级别、连接标识位、心跳时长。

负载：Payload消息体位MQTT数据包的第三部分，包含CONNECT、SUBSCRIBE、SUBACK、UNSUBSCRIBE四种类型的消息。

.. image:: /Chapter/picture/image133.jpg

图9-9 数据包类型

9.4 消息的发送与接收
--------------------

通过MQTT服务器建立桥梁，连接每个设备让其可以互相通信，因此我们需要创建一个MQTT服务器。

9.4.1 MQTT服务器的搭建

服务器搭建软件有emqtt和mqttbox，emqtt是MQTT服务端软件，mqttbox是客户端软件，下载地址如下：

   Emqtt下载地址： http://www.emqtt.com/downloads

   Mqttbox下载地址： http://workswithweb.com/html/mqttbox/downloads.html

下载好后解压“emqttd-windows10-v2.3.11.zip <http://www.emqtt.com/downloads/2318/windows10>”，并通过命令提示符启动服务，首先进入到bin目录下，然后输入命令“emqttd.cmd
start”成功启动服务，如图9-10所示。

.. image:: /Chapter/picture/image134.jpg

图9-10 启动服务

最后在浏览器中输入“http://127.0.0.1:18083”可以进入服务器页面。

如果提示输入用户名和密码，默认用户名是admin，密码是public。也可以通过命令emqttd_ctl来设置新的登录用户，命令是emqttd_ctl
admins add <Username><Password><Tags>。

停止服务输入命令“emqttd.cmd stop”。

安装mqttbox安装后打开如图9-11所示。

.. image:: /Chapter/picture/image135.png

图9-11 mqttbox界面

点击create mqtt client 按下图输入需要填入Mqtt client
Name，Protocol需要选择mqtt/tcp
，Host写服务器地址和端口号，mqtt服务端口号默认是1883，如图9-12所示。

.. image:: /Chapter/picture/image136.png

图9-12 MQTTBox配置界面

9.4.2 消息的发送与接收

在搭建好服务后，可以使用mqttbox测试服务的是否可用，首先运行mqttbox点击“Add
Publisher”，在Topic to Publish窗口输入Topic并发布，然后“Add
subscriber”输入相同的Topic并订阅。在左侧的Publisher的窗口中点击“Publish”，在右侧的Subscriber窗口中可以看到对应的信息。如图9-13所示：

.. image:: /Chapter/picture/image137.png

图9-13 mqttbox的使用

再使用mqttbox创建一个新的客户端同样添加Subscriber，创建的Topic同第一个客户端一样比如hello。这样客户端1发布Topic后，如图9-14所示，在客户端2的订阅窗口可以看到客户端1的发送信息，如图9-15所示。

.. image:: /Chapter/picture/image138.png

图9-14 发送方客户端1

.. image:: /Chapter/picture/image139.png

图9-15 订阅方客户端2

打开EMQ的管理员控制台，可以看到一些相关的统计数据已经发生了变化。比如在“Themessagesdata”表格中，“qos0/received”的值为1，说明EMQ收到了1条QoS0的消息；“qos0/sent”的值为1，表示EMQ转发了一条QoS0的消息。

【案例9-1】使用Python，编写一个发布者和订阅者在一起的客户端。

分析：使用python编写程序进行测试MQTT的发布和订阅功能。首先要在控制台安装paho-mqtt工具，具体命令为:pip
install paho-mqtt，并且自己搭建好服务端程序。客户端代码如下：
::

   import paho.mqtt.client as mqtt
   MQTTHOST = IP地址
   MQTTPORT = 1883
   mqttClient = mqtt.Client()
   # 连接MQTT服务器
   def on_mqtt_connect():
      mqttClient.connect(MQTTHOST, MQTTPORT, 60)
      mqttClient.loop_start()
      # publish 消息
   def on_publish(topic, payload, qos):
      mqttClient.publish(topic, payload, qos)
   # 消息处理函数
   def on_message_come(lient, userdata, msg):
      print(msg.topic + "" + ":" + str(msg.payload))
      # subscribe 消息
   def on_subscribe():
      mqttClient.subscribe("/server", 1)
      mqttClient.on_message = on_message_come # 消息到来处理函数
   def main():
      on_mqtt_connect()
      on_publish("/test/server", "Hello Python!", 1)
      on_subscribe()
      while True:
         pass
   if __name__ == '__main__':
      main()

程序启动后会调用on_mqtt_connect()方法连接服务端，然后在主题"/test/server"发布消息，订阅"/server"主题并设置回调函数on_message_come处理收到的消息。

9.5 制作表情互发游戏
--------------------

通过前面小节的讲述已经了解了什么是mqtt协议，怎么搭建mqtt服务，怎么发布和订阅消息，下面我们看看如何利用mqtt服务实现两个设备之间互发表情游戏。我们所要实现的是在一个设备上选择一个表情包后点击发送，将信息发送到MQTT服务器固定的主题上，订阅了些主题的其他设备就可以收到发送过来表情。

9.5.1 预备知识

我们模拟两个用户互发表情，流程如下图9-16所示。

具体流程为：

1. 程序启动后，首先进行硬件初始化，主要是对显示屏，按键以及mqtt服务进行设置。

2. 完成硬件初始化后，进行一个无限循环中，等待用户按键操作以及接收消息。

3. 当用户按下按键后，清空原来的焦点，重新画焦点在新的表情上，并判断用户是否点击“发送”。

4. 更新界面显示。

5. 等待用户的下一次按键操作。

.. image:: /Chapter/picture/image140.png

图9-16 流程图

9.5.2 任务要求

为了保证能有较好的用户体验，设计了游戏界面，效果如下图9-17所示。

.. image:: /Chapter/picture/image141.png

图9-17 游戏界面

游戏界面中所罗列的按键1~按键4分别对应Skids开发板上的4个物理按键，本游戏只使用了key1和key3如下图9-18所示。

.. image:: /Chapter/picture/image142.png

图9-18 Skids开发板的按键

游戏界面主要分为两个区域：

1. 最顶部的区域显示已经发送的表情。

2. 最下面的区域显示选择的表情。

9.5.3 任务实施

1. 硬件初始化

通过类的构造函数，从而实现对硬件（屏幕显示和按键设置）进行初始化，同时设置配制参数。
::

   def __init__(self):
      self.keys = [Pin(p, Pin.IN) for p in [35, 36, 39, 34]]
      self.keymatch = ["Key1", "Key2", "Key3", "Key4"]
      self.select=1
      self.displayInit()
      self.wifi_name = "wifi名称"
      self.wifi_SSID = "wifi密码"
      #MQTT服务端信息
      self.SERVER = "服务器地址"
      self.SERVER_PORT = MQTT服务器端口
      self.DEVICE_ID = "设备ID"
      self.TOPIC1 = b"/cloud-skids/online/dev/" + self.DEVICE_ID
      self.TOPIC2 = b"/cloud-skids/message/server/" + self.DEVICE_ID
      self.CLIENT_ID = "7e035cd4-15b4-4d4b-a706-abdb8151c57d"
      #设备状态
      self.ON = "1"
      self.OFF = "0"
      self.content=""#初始化要发送的信息
      self.client = MQTTClient(self.CLIENT_ID, self.SERVER, self.SERVER_PORT)

在构造函数__init__()中，和mqttbox一样我们需要设置服务器地址，端口号，客户端名称，发布的主题，订阅的主题，客户端id，以及需要连接的wifi名称和密码，调用了displayInit()函数来进行屏幕初始化工作。
::
   def displayInit(self):#初始化
      screen.clear()
      self.drawInterface()
      self.selectInit()
   def selectInit(self):#选择表情初始化
      screen.drawline(20, 200, 92, 200, 2, 0xff0000)
      screen.drawline(92, 200, 92, 272, 2, 0xff0000)
      screen.drawline(92, 272, 20, 272, 2, 0xff0000)
      screen.drawline(20, 272, 20, 200, 2, 0xff0000)
   def drawInterface(self):#界面初始化
      bmp1=ubitmap.BitmapFromFile("pic/boy")
      bmp2=ubitmap.BitmapFromFile("pic/girl")
      bmp1.draw(20,200)#显示boy图片
      bmp2.draw(140,200)#显示girl图片
      screen.drawline(0, 160, 240, 160, 2, 0xff0000)

2. 开始游戏

通过类的成员函数do_connect()负责连接wifi网络。
::
   def do_connect(self):
      sta_if = network.WLAN(network.STA_IF) #STA模式
      ap_if = network.WLAN(network.AP_IF) #AP模式
      if ap_if.active():
         ap_if.active(False) #关闭AP
         if not sta_if.isconnected():
            print('Connecting to network...')
            sta_if.active(True) #激活STA
            sta_if.connect(self.wifi_name, self.wifi_SSID) #WiFi的SSID和密码
            while not sta_if.isconnected():
            pass
            gc.collect()

通过类的成员函数esp()负责连接mqtt服务。
::

   def esp(self):
      self.client.set_callback(self.sub_cb) #设置回调
      self.client.connect()
      print("连接到服务器：%s" % self.SERVER)
      self.client.publish(self.TOPIC1, self.ON) #发布“1”到TOPIC1
      self.client.subscribe(self.TOPIC2) #订阅TOPIC
   通过start()类成员函数开始程序。
   def start(self):
      try:
         while True:
            self.client.check_msg()#检查是否收到信息
            i = 0#用来辅助判断那个按键被按下
            j = -1
            for k in self.keys:#检查按键是否被按下
                if (k.value() == 0):##如果按键被按下
                  if i != j:
                     j = i
                     self.keyboardEvent(i)#触发相应按键对应事件
                     i = i + 1
                  if (i > 3):
                     i = 0
                     time.sleep_ms(130)
      finally:
         self.client.disconnect()
         print("MQTT连接断开")

3. 处理用户按键事件

当用户按下按键后，类的成员函数keyboardEvent()负责进行具体的处理。在该函数中，首先判断游戏是按的key1还是key3。如果是key1则重新画焦点框，否则是key3发送表情。
::

   def keyboardEvent(self, key):
      if self.keymatch[key] == "Key1":#右移键，选择要发送的表情
         if self.select%2==1:#用红色框选中boy表情
            screen.drawline(20, 200, 92, 200, 2, 0xffffff)
            screen.drawline(92, 200, 92, 272, 2, 0xffffff)
            screen.drawline(92, 272, 20, 272, 2, 0xffffff)
            screen.drawline(20, 272, 20, 200, 2, 0xffffff)
            screen.drawline(140, 200, 212, 200, 2, 0xff0000)
            screen.drawline(212, 200, 212, 272, 2, 0xff0000)
            screen.drawline(212, 272, 140, 272, 2, 0xff0000)
            screen.drawline(140, 272, 140, 200, 2, 0xff0000)
            self.select+=1
         else:#用红色框选中girl表情
            screen.drawline(140, 200, 212, 200, 2, 0xffffff)
            screen.drawline(212, 200, 212, 272, 2, 0xffffff)
            screen.drawline(212, 272, 140, 272, 2, 0xffffff)
            screen.drawline(140, 272, 140, 200, 2, 0xffffff)
            screen.drawline(20, 200, 92, 200, 2, 0xff0000)
            screen.drawline(92, 200, 92, 272, 2, 0xff0000)
            screen.drawline(92, 272, 20, 272, 2, 0xff0000)
            screen.drawline(20, 272, 20, 200, 2, 0xff0000)
            self.select+=1
    if self.keymatch[key] == "Key3":#发送表情按键
         if self.select%2==1:#显示已发送boy表情
            bmp1=ubitmap.BitmapFromFile("pic/boy")
            bmp1.draw(140,40)
            self.content="001"
            self.client.publish(self.TOPIC2,self.content)
         else:#显示已发送girl表情
            bmp2=ubitmap.BitmapFromFile("pic/girl")
            bmp2.draw(140,40)
            self.content="002"
            self.client.publish(self.TOPIC2,self.content)

4. 接收到服务器的消息

通过类成员函数sub_cb()处理服务器的消息。
::

   def sub_cb(self,topic, message):#从服务器接受信息
      message = message.decode()
      print("服务器发来信息：%s" % message)
      #global count
      if message=="001":#收到boy表情号码显示boy表情
         bmp1=ubitmap.BitmapFromFile("pic/boy")
         bmp1.draw(140,40)
      elif message=="002":#收到girl表情号码显示girl表情
         bmp1=ubitmap.BitmapFromFile("pic/girl")
         bmp1.draw(140,40)

实践练习：

1.修改按键的处理规则，让Key2处理上下移动。

2.增加表情数量。

.. _本章小结-8:

9.6 本章小结
------------

在本章节中，主要学习了网络的基础知识，以及ESP32芯片的功能，最后介绍了MQTT协议以及使用的方法，并通过制作表情互发游戏深入学习在skids开发板上如何开发MQTT协议的网络程序。

网络开发是Python的基础应用，使用率很高，MQTT协议使用频率也非常高，希望读者可以多加以理解，并熟练掌握它们的使用。

.. _练习题目-8:

9.7 练习题目
------------

1.
修改猜拳游戏为网络版本，让两个设备可以通过mqtt实现互动，并显示出输赢结果。

2.
实现掷筛子游戏，两个设备互相发送自己的个数给对方，并显示出输赢结果。
