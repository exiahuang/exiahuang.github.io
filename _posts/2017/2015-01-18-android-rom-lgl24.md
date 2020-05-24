---
categories:
- AndroidRom
date: 2015-01-18 08:01:34
description: AndroidRom LGL24 LGFlashTool
layout: post
tags:
- AndroidRom
title: Android LGL24 LGFlashTool
update_date: 2020/05/23 23:56:51

---

# Introduce
1. 本方法需要重新刷新底包，机器内的所有信息都将完全丢失，之前请做好备份
2. 本教程的起点是双网版的L24，手持纯au机的朋友需要先用NCK CODE把网络锁解掉，方法另寻。淘宝购入的朋友基本可以无视这条。
3. 本人综合网络上流传的各教程，可能在进行破解过程中存在个人差异
4. 在任何操作前请一定明白自己在干什么，线刷有风险，刷坏就是砖，请事先学习救砖技能。
5. 本人不对任何因参照本文而变成砖头的设备负责。
6. 具体方法参考自windson223 大神的帖子：日本au版G3 LGL24破解电信3G教程http://bbs.gfan.com/android-7653788-1-1.html，想要破解电信的请参考此帖。


# 需要准备的：

## 硬件：
- au LG L24手机
- MicroUSB数据线
- 预装windows系统的个人电脑

## 文件：
1. LGFlashTools v1.8.1：Setup_LGFlashTool_1.8.1.1023.exe
2. 破解文件 Megalock.DLL
3. LG手机驱动程序：LGUnitedMobileDriver_S51MAN312AP22_ML_WHQL_Ver_3.12.3.exe
4. LGL24_20140617_LGFLASHv160.dll
5. LGL22AT-01-V20c-440-50-JUL-01-2014+0.tot（4.4.2原版系统，下载后解压得到的tot文件）
6. D802TOT.exe
7. 4.4.2下的root工具：g2_support_tool-2.0c
8. 确保开启windows下的文件后缀显示，参见http://jingyan.baidu.com/article/c146541354adfb0bfcfc4ca0.html


文件综合http://yunpan.cn/cgfLzEkHcYRMv 
（提取码：a601）。


rom、dll文件也可以去这个贴下载http://bbs.gfan.com/forum.php?mod=viewthread&tid=7550556&extra=page%3D1%26filter%3Dtypeid%26typeid%3D10913%26typeid%3D10913

# 操作：

安装L24手机驱动程序LGUnitedMobileDriver_S51MAN312AP22_ML_WHQL_Ver_3.12.3.exe是前提。可以连接手机后，查看设备管理器是否成功识别LG L24.

0. 手机先不要连接电脑
1. 安装LGFlashTools v1.8文件，比如选择安装Setup_LGFlashTool_1.8.1.1023.exe
2. 将MegaLock.dll文件覆盖到LGFlashToolsV1.8.1的安装文件夹下，完成破解。
3. 下载LGL24AT-01-V10a-440-50-JUN-19-2014+0.tot文件，例如放在E:\L24 tot  文件夹下。并复制一个相同文件，命名为D802_32G_20A.tot
4. 将D802TOT.exe与D802_32G_20A.tot放在同一目录下。例如都放在E:\L24刷机  文件夹下
5. 打开LGFlashTools v1.8.1
   LGFlashTools刷机设置方法可以参考G3，此帖http://bbs.gfan.com/android-7502599-1-1.html有详细设置方法。
   L24进入刷机界面方法： `关机后，用力按住后背上的音量+键，然后插入usb数据线`
6. 在跳出的Model config界面里选择好LGL24_20140617_LGFLASHv160.dll和LGL24AT-01-V10a-440-50-JUN-19-2014+0，其他不用修改。点OK。
7. 在主界面点击左上角的黄色向右箭头，开始验证TOT文件。（等到显示ready）
   如果跳出警告的话，你肯定有哪里设置不对了，请仔细核对上面几条。
8. 验证完成后先不要刷，打开D802TOT.exe工具，输入“1”，等待补丁。（等到界面显示cracking end）
9. 补丁打完，将LGL24AT-01-V10a-440-50-JUN-19-2014+0.tot改名（比如改成LGL22AT-01-V20c-440-50-JUL-01-2014+222.tot），而将E:\L24刷机文件夹下的D802_32G_20A.tot改名为LGL24AT-01-V10a-440-50-JUN-19-2014+0.tot
之后，将E:\L24刷机文件夹里的新命名的LGL24AT-01-V10a-440-50-JUN-19-2014+0.tot复制到E:\L24 tot 文件夹内
（必须确保新、老，命名为LGL22AT-01-V20c-440-50-JUL-01-2014+0.tot文件的位置不变）

10. 回到LGFlashTools，这时才设置手机为刷机模式，连接手机，将固件正常刷入手机，耗时约260s至300s不等，请务必等到刷机过程完全结束，flashtool显示pass完成后,。才手动重启手机。
    这个时候手机应该开始进AU界面，然后到LG界面了。继续等到语言界面，到了语言界面就说明刷好了，然后拔线。
    重点：刷好后拔完线，记得关闭LG FlashTool！请一定要关闭！否则之后解锁开发者模式，连入电脑又会再次开始刷机。

11. 解锁手机的开发者模式（(设置-常规-关于设备-软件信息-内部版本号狂点7次 然后返回就有开发者选项） ，然后把usb调试打勾。
    连接手机，选择PTP模式
    执行4.4.2下的root工具g2_support_tool-2.0c，进入文件夹下选择runme_KK.bat后，参考说明，获得root权限（这期间手机应该会重启3次）。
    root成功后，supersu就会显示授权项目

LG L24自带软件卸载可以参考L22，参见http://bbs.gfan.com/forum.php?mod=viewthread&tid=7385300&extra=page%3D2%26filter%3Dtypeid%26typeid%3D10825%26typeid%3D10825
本人认为和au有关的都能卸载了。保留google服务框架、isai、LG相关软件就可以了。不放心的可以选择禁止开机自启动。
其实卸载au附加的软件或者禁止启动之后，开机会快了。内存使用量一般还是在60%至80%左右比较高的水平。

如果还是觉得卡顿，

在常规设置中选择开发人员选项：下拉找到“动画持续时间比例”并进入点选关闭动画或动画缩放0.5倍（如果选择关闭就没有过渡动画了了）

或者继续下拉到底找到“后台进程限制”并进入，选择“至多3道流程”或者“至多4道流程”。如果选择不允许后台进程可能会出bug。


# 进入recovery
-出现ISAI界面2S后松开音量键下和电源键一瞬间 再次按住音量键下和电源键
-然后选YES（不会恢复出厂设置），再选择YES，即可进入REC!