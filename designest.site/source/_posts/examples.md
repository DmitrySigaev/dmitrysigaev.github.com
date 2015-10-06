title: my testing JS in  Node.js
date: 2013-10-05 14:43:21
tags: Node.js, JavaScript
---

{% codeblock %}
console.log('Standard ECMA-262 3rd Edition - December 1999:');
console.log('Variable object:');
/*
 * Always in programs we declare functions and variables which then successfully use building our systems.
 * But how and where the interpreter finds our data (functions, variable)?
 *  What occurs, when we reference to needed objects?
 *  Many ECMAScript programmers know that variables are closely related with the execution context:
 * */

var a = 10; // variable of the global context

(function () {
    var b = 20; // local variable of the function context
})();

console.log(a); // 10
// check: console.log(b); // "b" is not defined
/*
 * Also, many programmers know that the isolated scope in the current version of specification is created 
 * only by execution contexts with УfunctionФ code type. I.e., in contrast with C/C++, for example
 *  the block of for loop in ECMAScript does not create a local context:
 *  */

for (var k in { a: 1, b: 2 }) {
    console.log('k'+ k);
}

console.log('k' + k); // variable "k" still in scope even the loop is finished

/*
 * Variable object in global context
*/

var a = new String('test');
b = 10;

console.log(a); // напр€мую, будет найдено в VO(globalContext): "test"

//node.js fix console.log(window['a']); // косвенно через global === VO(globalContext): "test"
console.log(a === this.a); // true(browser) : false in node.js this.a is undefined

exports.a = a;
console.log(a === this.a); // true beacause this is exports;

// var aKey = 'a';
// console.log(window[aKey]); // косвенно, им€ свойства сформировано налету: "test"

/*
 * Variable object in function context
 * 
 * Regarding the execution context of functions Ч there VO is inaccessible directly,
 * and its role plays so - called an activation object(in abbreviated form Ч AO).
 * 
 * VO(functionContext) === AO;
 * 
 * An activation object is created on entering the context of a function and initialized 
 * by property arguments which value is the Arguments object:
 *  
 * AO ={
 *   arguments: <ArgO>
 *   };
 *   
 * 
 * Arguments object is a property of the activation object. It contains the following properties:
 * callee Ч the reference to the current function;
 * length Ч quantity of real passed arguments;
 * properties-indexes (integer, converted to string) which values are the values of functionТs arguments
 *  (from left to right in the list of arguments). 
 *  Quantity of these properties-indexes == arguments.length. 
 *  Values of properties-indexes of the arguments object and present (really passed) formal parameters are shared.
 */

function foo(x, y, z) {
    
    // quantity of defined function arguments (x, y, z)
    console.log('foo.length: '+ foo.length); // 3
    
    // quantity of really passed arguments (only x, y)
    console.log('arguments.length:' + arguments.length); // 2
    
    // reference of a function to itself
    console.log('arguments.callee === foo: ' + (arguments.callee === foo)); // true
    
    // parameters sharing
    
    console.log('x === arguments[0]: ' + (x === arguments[0])); // true
    console.log(x); // 10
    
    arguments[0] = 20;
    console.log(x); // 20
    
    x = 30;
    console.log('arguments[0]: '+arguments[0]); // 30
    
    // however, for not passed argument z,
    // related index-property of the arguments
    // object is not shared
    
    z = 40;
    console.log('arguments[2]:'+ arguments[2]); // undefined
    
    arguments[2] = 50;
    console.log(z); // 40
  
}

foo(10, 20);

/*
 * Feature of implementations: property __parent__ 
 */
/*
 * As it was already noted, by the standard, to get direct access to the activation object is impossible.
 * However, in some implementations, namely in SpiderMonkey and Rhino, functions have special property __parent__,
 *  which is the reference to the activation object (or the global variable object) 
 *  in which these functions have been created. Let's test.
 *  
// console.log(foo.__parent__); So in node.js  __parent__ property doesn't work;

{% endcodeblock %}