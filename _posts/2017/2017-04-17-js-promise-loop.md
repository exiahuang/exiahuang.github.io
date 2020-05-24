---
categories:
- Javascript
- Program
date: 2017-04-17 22:02:34
description: Javascript promise loop, promisify, javascript
layout: post
tags:
- Javascript
- Program
title: Javascript promise loop
update_date: 2020/05/23 23:56:51

---

# ES6 Native Promise Loop

<div class="note primary">ES6 Native Promise Loop</div>

```js
Promise.resolve(0).then(function loop(i) {
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            console.log(i);
            resolve(i+1);
        }, 100);
    })
    .then(loop);
});
```

# ES6 Native Promise while Loop

```js
function action(i) {
    console.log(i);
    return {
        done: i > 9,
        value: i+1
    };
}

function loop(promise, fn) {
    return promise.then(fn).then(function(wrapper) {
        return !wrapper.done ? loop(Promise.resolve(wrapper.value), fn): wrapper.value;
    });
}

loop(Promise.resolve(0), action).then(function(value) {console.log('end: ' + value)});
```


# One more example
```js
function callFun(testclass){
    return new Promise(function (resolve, reject) {
      // Do some Async stuff
      // call resolve if it succeeded
      // reject if it failed
    });
}

Promise.resolve(0).then(function loop(i) {
    // The loop check
    if (i < arrayList.length) {              // The post iteration increment
        return callFun(arrayList[i]).then(function(){
            // console.log(i);
            return (i + 1);
        }).then(loop);
    }
}).then(function() {
    console.log('error', e);
}).catch(function(e) {
    console.log('error', e);
    appendError(e);
});
```