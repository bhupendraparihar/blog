---
title: Implementing Throttle Function
date: 2020-05-23 16:15:32
tags:
---

What is a throttle function. "throttle" function returns a function which will run only once with in the time specified. This is very useful when we wish to perform some operation only once even when the function is called multiple times.
For more details, <a href="http://underscorejs.org/#throttle">please follow the link</a>.

In this article we are discussing how can we implement our own throttle method. The definition of our function should be
<pre>
function throttle(fn, timeInMilliseconds){
    return function(){
      ...
    }
}
</pre>

So. let's create a boolean variable which will in closure here, and change it only when the function is called or after certain time limit.

<pre>
function throttle(fn, timeInMiliseconds){
  var t = true;

  return function(){
    if(t){
      fn();
      t = false;

      setTimeout(function(){
        t = true;
      },timeInMiliseconds);
    }
  }
}
</pre>
Testing our throttle function
<pre>
function hello(){
  console.log('hello');
}

//This returns a function which will only run once in 5 seconds.
var throttled = throttle(hello, 5000);

throttled(); //print hello
throttled(); //5 second isn't over yet

setTimeout(function(){
  throttled();
}, 2000); // 5 second isn't over yet

setTimeout(function(){
  throttled();
}, 6000); //print hello
</pre>
