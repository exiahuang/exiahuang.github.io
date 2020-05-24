---
categories:
- Javascript
- Program
date: 2017-04-11 08:02:34
description: jQuery - selectors on a html string, javascript, js, jquery
layout: post
tags:
- Javascript
- Program
title: jQuery - selectors on a html string
update_date: 2020/05/23 23:56:51

---

# jQuery - selectors on a html string

<div class="note primary">use `jQuery.parseHTML` to parse the HTML into an array of elements; then you’ll be able to convert it to a jQuery collection and use `filter` to restrict the collection to elements matching a selector.</div>

```js
var html =
    '<td class="test">asd</td>' +
    '<!-- -->' +
    '<td class="second">fgh</td>' +
    '<td class="last">jkl</td>';

var obj = $($.parseHTML(html)).filter('.test');
console.log(obj);

var text = $($.parseHTML(html)).filter('.test').text();
console.log(text);
```

# jquery parseHTML not working as expected

<div class="note primary">My guess is that your data.description is escaped and the method parseHTML isn't going to handle that. Check out this post for a solution:</div>

Javascript decoding html entities

```js
var text = '&lt;p&gt;name&lt;/p&gt;&lt;p&gt;&lt;span style="font-size:xx-small;"&gt;ajde&lt;/span&gt;&lt;/p&gt;&lt;p&gt;&lt;em&gt;da&lt;/em&gt;&lt;/p&gt;';
var decoded = $('<div/>').html(text).text();
console.log(decoded);
```

So in your case:

```js
var decoded = $('<div/>').html(data.description).text();
$('#gbFullPic').html(decoded);
```


#  jQuery - selectors on a html string
```js
var url = 'https://developer.salesforce.com/docs/get_document_content/api_tooling/tooling_api_objects_apexcodecoverageaggregate.htm/en-us/206.0';
$.get(url, function(result){
     console.log('>>>result');
     console.log(result);
     console.log(result.id);
     console.log(result.title);
     console.log('>>>>result.content');
     // console.log($.parseHTML(result.content.toString()));
     var decoded = $('<div/>').html(result.content);
     // console.log(decoded);
     // console.log(decoded.text());
     // console.log(decoded.html());

     var html = $(decoded.html()).find('td > span.keyword');
     html.each(function(){
        console.log($(this).text());
     });
});
```