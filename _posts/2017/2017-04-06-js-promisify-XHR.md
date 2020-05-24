---
categories:
- Javascript
- Program
date: 2017-04-06 22:02:34
description: How do I promisify native XHR? XMLHttpRequest, promisify, javascript
layout: post
tags:
- Javascript
- Program
title: How do I promisify native XHR?
update_date: 2020/05/23 23:56:51

---

# Using callbacks

<div class="note primary">I want to use (native) promises in my frontend app to perform XHR request but without all the tomfoolery of a massive framework.</div>

```js
function makeRequest (method, url, done) {
  var xhr = new XMLHttpRequest();
  xhr.open(method, url);
  xhr.onload = function () {
    done(null, xhr.response);
  };
  xhr.onerror = function () {
    done(xhr.response);
  };
  xhr.send();
}

// And we'd call it as such:

makeRequest('GET', 'http://example.com', function (err, datums) {
  if (err) { throw err; }
  console.log(datums);
});
```

# How do I promisify native XHR?

## The promise constructor

We can construct a promise like so:

```js
new Promise(function (resolve, reject) {
  // Do some Async stuff
  // call resolve if it succeeded
  // reject if it failed
});
```

The promise constructor takes a function that will be passed two arguments (let's call them `resolve` and `reject`). You can think of these as callbacks, one for success and one for failure. Examples are awesome, let's update makeRequest with this constructor:

```js
function makeRequest (method, url) {
  return new Promise(function (resolve, reject) {
    var xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.onload = function () {
      if (this.status >= 200 && this.status < 300) {
        resolve(xhr.response);
      } else {
        reject({
          status: this.status,
          statusText: xhr.statusText
        });
      }
    };
    xhr.onerror = function () {
      reject({
        status: this.status,
        statusText: xhr.statusText
      });
    };
    xhr.send();
  });
}

// Example:

makeRequest('GET', 'http://example.com')
.then(function (datums) {
  console.log(datums);
})
.catch(function (err) {
  console.error('Augh, there was an error!', err.statusText);
});
```

Now we can tap into the power of promises, chaining multiple XHR calls (and the `.catch` will trigger for an error on either call):

```js
makeRequest('GET', 'http://example.com')
.then(function (datums) {
  return makeRequest('GET', datums.url);
})
.then(function (moreDatums) {
  console.log(moreDatums);
})
.catch(function (err) {
  console.error('Augh, there was an error!', err.statusText);
});
```

We can improve this still further, adding both POST/PUT params and custom headers. Let's use an options object instead of multiple arguments, with the signature:

```js
{
  method: String,
  url: String,
  params: String | Object,
  headers: Object
}
```

`makeRequest` now looks something like this:

```js
function makeRequest (opts) {
  return new Promise(function (resolve, reject) {
    var xhr = new XMLHttpRequest();
    xhr.open(opts.method, opts.url);
    xhr.onload = function () {
      if (this.status >= 200 && this.status < 300) {
        resolve(xhr.response);
      } else {
        reject({
          status: this.status,
          statusText: xhr.statusText
        });
      }
    };
    xhr.onerror = function () {
      reject({
        status: this.status,
        statusText: xhr.statusText
      });
    };
    if (opts.headers) {
      Object.keys(opts.headers).forEach(function (key) {
        xhr.setRequestHeader(key, opts.headers[key]);
      });
    }
    var params = opts.params;
    // We'll need to stringify if we've been given an object
    // If we have a string, this is skipped.
    if (params && typeof params === 'object') {
      params = Object.keys(params).map(function (key) {
        return encodeURIComponent(key) + '=' + encodeURIComponent(params[key]);
      }).join('&');
    }
    xhr.send(params);
  });
}

// Headers and params are optional
makeRequest({
  method: 'GET',
  url: 'http://example.com'
})
.then(function (datums) {
  return makeRequest({
    method: 'POST',
    url: datums.url,
    params: {
      score: 9001
    },
    headers: {
      'X-Subliminal-Message': 'Upvote-this-answer'
    }
  });
})
.catch(function (err) {
  console.error('Augh, there was an error!', err.statusText);
});
```