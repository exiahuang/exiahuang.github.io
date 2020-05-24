---
categories:
- Salesforce
date: 2017-07-20 08:08:34
description: DateTime in local Time Zone
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC DateTime in local Time Zone
update_date: 2020/05/23 23:56:51

---

# try this
```
public class Utility {
 
    public static Datetime getLocalDateTime(Datetime z)
    {    
        Datetime l = z.Date();
        l = l.addHours(z.hour());
        l = l.addMinutes(z.minute());
        l = l.addSeconds(z.second());
        
        return l;
    }
}
 
Datetime gmt = Datetime.Now();
Datetime local = Utility.getLocalDateTime(Datetime.Now());
System.Debug('GMT Time: ' + gmtNow);
System.Debug('Local Time: ' + local);
```

# Here is an alternate method, straight forward.
```
Datetime current = System.now(); // returns date time value in GMT time zone.
 
Date currDate = current.date();
Date currTime = current.time();
 
Datetime local = datetime.newinstance(currDate,currTime); // This will return date time in my local time zone.
```