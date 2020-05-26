---
title: public and private
date: 2020-05-22 12:01:43
tags:
---

Here is the code for creating a object definition(class) which maintains the public and private scope of variable.
<pre>
function Person(new_name){
	//_age is a private variable
	var _age = "";

	var obj = {};
	
	obj.name = new_name;
	obj.getAge = function() {
		return _age;
	}
	obj.setAge = function (new_age) {
		_age = new_age;
	}
	obj.displayInfo = function () {
		return "My age is " + _age;
	}
	return obj;
}

var person = new Person('BP');
person.setAge(26);
console.log(person.getAge()); //26
console.log(person._age); //undefined
</pre>

You can observe, it is closure what keeps the varible private