---
categories:
- Python
- Program
date: 2017-04-14 22:02:34
description: A Simple Sublime Addon Example
layout: post
tags:
- Python
- Program
title: A Simple Sublime Addon Example
update_date: 2020/05/23 23:56:51

---

# A Simple Sublime Addon Example

<div class="note primary">`addCurrentTime.py` is A Simple Sublime Addon Example.
You can add your comment quickly.
please put the file in `\Data\Packages\User\addCurrentTime.py`</div>

```python
import datetime
import sublime_plugin
class AddCurrentTimeCommand(sublime_plugin.TextCommand):
    def run(self, edit):
        self.view.run_command("insert_snippet", 
            {
                # "contents": "%s" % datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") 
                "contents": "%s" % datetime.datetime.now().strftime("%Y.%m.%d") + " exia.huang" 
            }
        )
```

You can add your hotkey, use `alt+i` and you can insert time and message

```json
[
    { "keys": ["alt+i"], "command": "add_current_time" }
]
```