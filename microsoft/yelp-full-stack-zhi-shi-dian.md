\#1 What happened after click google.com

DNS get IP \(Browser, OS, Router, ISP DNS Server\)

Browser initialize TCP connection between client and server

Browser sends HTTP request /GET to server

Server sends back a HTTP response

Render the HTML

\#2 Closure

[https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)

A **closure **is the combination of a function bundled together \(enclosed\) with references to its surrounding state.

In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

To use a closure, simply define a function inside another function and expose it. To expose a function, return it or pass it to another function.

The inner function will have access to the variables in the outer function scope, even after the outer function has returned.

[http://www.ruanyifeng.com/blog/2009/08/learning\_javascript\_closures.html](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)

```cpp
　　function f1(){

　　　　var n=999;

　　　　function f2(){
　　　　　　alert(n); 
　　　　}

　　　　return f2;

　　}

　　var result=f1();

　　result(); // 999
```

[https://coderbyte.com/algorithm/3-common-javascript-closure-questions](https://www.gitbook.com/book/hebiao064/crack2018/edit#)

```cpp
// 1. What will the following code output?
for (var i = 0; i < 3; i++) {
  setTimeout(function() { alert(i); }, 1000 + i);
}

// 2. Write a function that would allow you to do this.
var addSix = createBase(6);
addSix(10); // returns 16
addSix(21); // returns 27

function createBase(base) {
    var counter = base || 0;
    function f2 (toAdd) {
        counter += toAdd;
        console.log(counter);
    }
    return f2;
}

// 3. How would you use a closure to create a private counter?
function counter() {
  var _counter = 0;
  // return an object with several functions that allow you
  // to modify the private _counter variable
  return {
    add: function(increment) { _counter += increment; },
    retrieve: function() { return 'The counter is currently at: ' + _counter; }
  }
}

// error if we try to access the private variable like below
// _counter;

// usage of our counter function
var c = counter();
c.add(5); 
c.add(9); 

// now we can access the private variable in the following way
c.retrieve(); // => The counter is currently at: 14#3
```

\#3. Endpoint

If no response: settimeout call

If slow?  Server too far, db query to slow \(too much join\), too much traffic,  distributed api service might be called



\#4. Promises 将嵌套的 callback，改造成一系列的`.then`

的连缀调用，去除了层层缩进的糟糕代码风格。Promises 不是一种解决具体问题的算法，而已一种更好的代码组织模式。接受新的组织模式同时，也逐渐以全新的视角来理解异步调用。

