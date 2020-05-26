---
title: Implement synchronous run for asynchronous tasks
date: 2020-05-24 03:24:34
tags:
---

This is a programming problem of running two asynchronous function in synchronous manner.  We have few async tasks t1, t2 and t3.

<pre>
var t1 = function(arg){
  console.log('Task 1 start');
  setTimeout(function(){
    console.log('Task 1 end');
    arg();
  }, 500);
}


var t2 = function(arg){
  console.log('Task 2 start');
  setTimeout(function(){
    console.log('Task 2 end');
    arg();
  }, 100);
}

var t3 = function(arg){
  console.log('Task 3 start');
  setTimeout(function(){
    console.log('Task 3 end');
    arg();
  }, 200);
}
</pre>

We want to implement a runSync method which takes array of these tasks, but run them synchronously. 

Lets create a task array, tasks = [t2, t3, t1], and t3 should run only when t2 is finished and then run t1.

<pre>
var runSync = function(tasks){
  var i = 0;
  
  function run(){
    if(i < tasks.length){
      tasks[i](run);
      i++;
    }
   
  }
  
  run();
}

runSync([t3,t1,t2]);

</pre>