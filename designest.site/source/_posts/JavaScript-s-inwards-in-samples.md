title: "JavaScript's inwards in samples"
date: 2014-10-19 14:04:42
tags: JavaScripts
---


Let's take a look at an example:
```
function A() {
}

A.prototype.x = 1;

var a = new A();

A.prototype = {
    x : 2
}

console.log("a.x = " + a.x); 

function B() {
}
B.prototype.x = 1;

var b = new B();

B.prototype.x = 2;

console.log("b.x = " + b.x); 

```

Please check yourself. See answer:

```
a.x = 1;
b.x = 2;

```

Let's go:

As you can find JavaScript program source text is free-format, using the
semicolon as a statemant terminator and curly braces of grouping blocks of 
statements. But...

var C = function () {};




