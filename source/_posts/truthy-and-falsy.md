---
title: truthy and falsy
date: 2020-05-22 12:07:41
tags:
---
In JavaScript, apart from Boolean values like true and false, all other values also have some boolean value corresponds to it.
<pre>
    false
    ""(empty string)
    0(zero)
    undefined
    null
    NaN(not a number)
</pre>
are considered falsy values.

So all the other values except these are, truthy values.

Ex "false" (String false) under conditional statement returns true.

This is very important concept in JavaScript.