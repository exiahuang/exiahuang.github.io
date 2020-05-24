---
categories:
- Program
date: 2001-01-01 00:00:00
description: How to setup windows to share wifi?
layout: post
tags:
- windows
- IT
title: windows dos wifi share
update_date: 2020/05/23 23:56:53

---

### start wifi share

```bash
netsh wlan set hostednetwork mode=allow ssid=yourssid key=password
netsh wlan start hostednetwork
pause
```

### stop wifi share

```bash
netsh wlan stop hostednetwork
pause
```