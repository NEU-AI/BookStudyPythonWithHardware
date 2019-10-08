.. _android:

安卓结算APP
============================

基本功能
----------------------------


- **软件基本流程**


.. image:: ../picture/android5.png
    :alt: snake
    :width: 540px


- **首页**

  + 进入首页连接服务器认证
  + 认证成功后等待框消失

.. image:: ../picture/android1.png
    :alt: snake
    :width: 540px
	
.. image:: ../picture/android2.png
    :alt: snake
    :width: 540px
	
- **商品信息页**

  + 商品放在扫描设备识别范围内
  + 通过服务器获取设备信息
  + 左侧显示商品基本信息
  + 右侧显示汇总信息
  
.. image:: ../picture/android3.png
    :alt: snake
    :width: 540px

- **结算页**

  + 点击结算按钮
  + 弹出二维码支付页面
  + 手机支付成功后页面关闭回到首页


.. image:: ../picture/android4.png
    :alt: snake
    :width: 540px


代码分析
----------------------------

- **BaseActivity基类**

页面基类，实现网络的调用，实现弹出等待窗体，提示窗体以及记录窗体状态。
::

	
	
