---
categories:
- Program
date: 2017-08-01 08:03:34
description: JS Papaparse Read CSV
layout: post
tags:
- js
title: JS Papaparse Read CSV
update_date: 2020/05/23 23:56:51

---

# JS Read CSV

```
<html>
<meta charset="utf-8"/>
  <head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
  <script type="text/javascript" src="./papaparse.min.js"></script>

  </head>
  <body>

<script>
  var data;
 
  function handleFileSelect(evt) {
    var file = evt.target.files[0];
 
    Papa.parse(file, {
      header: true,
      encoding: 'Shift-JIS',
      dynamicTyping: true,
      skipEmptyLines: true,
      complete: function(results) {
        data = results;
        console.log(data);
      }
    });
  }
 
  $(document).ready(function(){
    $("#csv-file").change(handleFileSelect);
  });
</script>
<input type="file" id="csv-file" name="files"/>

  </body>
</html>
```