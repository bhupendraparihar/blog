---
title: looping problem
date: 2020-05-22 12:13:48
tags:
---
I was looking into a problem of closure inside loop in stackoverflow. It is as follows..

<pre>
var funcs = {};
for (var i = 0; i & lt; 3; i++) { // let's create 3 functions
    funcs[i] = function () { // and store them in funcs
        console.log("My value: " + i); // each should log its value.
    };
}
for (var j = 0; j & lt; 3; j++) {
    funcs[j](); // and now let's run each one to see
}
</pre>

the output I was expecting is 

<pre>
My value: 0
My value: 1
My value: 2
</pre>

But the output is much different.
<pre>
My value: 3
My value: 3
My value: 3
</pre>

Now the reason for such an awkward behaviour is within each of our anonymous functions, is bound to the same variable outside of the function.

This problem can be solved by closure.

<pre>
var funcs = {};
for (var i = 0; i < 3; i++) {          // let's create 3 functions
  funcs[i] = (function(i){
    //console.log(i)
    
    return function() {            // and store them in funcs
       console.log("My value: " + i); // each should log its value.
    };
  })(i);
}
for (var j = 0; j < 3; j++) {
    funcs[j]();                        // and now let's run each one to see1
}
</pre>

or just by using let instead of var, as let has block level scope.
<pre>
var funcs = {};
for (let i = 0; i & lt; 3; i++) { // let's create 3 functions
    funcs[i] = function () { // and store them in funcs
        console.log("My value: " + i); // each should log its value.
    };
}
for (var j = 0; j & lt; 3; j++) {
    funcs[j](); // and now let's run each one to see
}
</pre>