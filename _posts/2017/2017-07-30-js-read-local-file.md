---
categories:
- Program
date: 2017-07-30 08:02:34
description: Reading in a local csv file in javascript?
layout: post
tags:
- Javascript
- Js
title: Reading in a local csv file in javascript?
update_date: 2020/05/23 23:56:51

---

# 
Here is how to use the `readAsBinaryString()` from the `FileReader` API to load a local file.

```html
<p>Select local CSV File:</p>
<input id="csv" type="file">

<output id="out">
    file contents will appear here
</output>
```

Basically, just need to listen to change event in `<input type="file">` and call the `readFile` function.

```js
var fileInput = document.getElementById("csv"),

    readFile = function () {
        var reader = new FileReader();
        reader.onload = function () {
            document.getElementById('out').innerHTML = reader.result;
        };
        // start reading the file. When it is done, calls the onload event defined above.
        // reader.readAsBinaryString(fileInput.files[0]);
        reader.readAsText(fileInput.files[0], 'utf8');
    };

fileInput.addEventListener('change', readFile);
```