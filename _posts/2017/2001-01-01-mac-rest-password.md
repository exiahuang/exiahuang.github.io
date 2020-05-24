---
categories:
- Program
date: 2001-01-01 01:00:00
description: mac rest password Mac单用户模式重设管理员密码
layout: post
tags:
- mac
- IT
title: mac rest password Mac单用户模式重设管理员密码
update_date: 2020/05/23 23:56:51

---

# 如果 Mac 设备的当前系统为 El Capitan、Yosemite、Mavericks、Mountain Lion 或者 Lion 的话可以通过以下操作步骤来实现：

　　1. 在单用户模式下启动 Mac 设备。

　　2. 打开终端窗口，然后输入以下命令：

　　mount -uw /

　　3. Capitan 或 Yosemite 系统用户分别输入以下两个命令：

　　launchcti load /System/Library/LaunchDaemons/com.apple.taskgated.plist

　　launchctl load /System/Library/LaunchDaemons/com.apple.opendirectoryd.plist

　　而 Mavericks、Mountain Lion 或 Lion 系统用户则输入以下命令：

　　launchctl load /System/Library/LaunchDaemons/com.apple.opendirectoryd.plist

　　需要注意的是，如果你不知道用户的短名称，可以输入以下命令来获取用户列表(短名称位于左侧，完整名称位于右侧)：

　　dscl localonly ls /Local/Default/Users realname

　　4. 输入以下命令，并将 shortname 替换为管理员用户的短名称(用户个人文件夹的名称)：

　　passwd shortname

　　系统提示时，输入新的帐户密码，但是你可能看不到任何表明正在键入的指示。

　　5. 输入 reboot 命令以重新启动 Mac。

# 如果你的 Mac 设备当前的系统为 Snow Leopard，则可以通过以下步骤来重设密码：

　　1. 在单用户模式下启动 Mac。

　　2. 打开终端窗口，然后输入以下命令：

　　mount -uw /

　　如果你不知道用户的短名称，输入以下命令以获取短名称的列表：

　　ls /Users

　　3. 输入以下命令：

　　launchctl load /System/Library/LaunchDaemons/com.apple.DirectoryServices.plist

　　4. 输入以下命令，并将 shortname 替换为用户的短名称(用户个人文件夹的名称)：

　　passwd shortname

　　5. 系统提示时，输入新的帐户密码，同样，你可能看不到任何表明正在键入的指示。

　　6. 输入 reboot 命令以重新启动 Mac。