### Function Declarations (Named Functions) vs. Function Expressions

A function declaration has a name & exists in the code base before code runs - meaning it can be run before it is defined in the code
```javascript

function sayHello(name) {
    return "Hello, " + name;
}

```
Function expression - function only comes into existence when the assignment happens - it doesn't exist prior because it doesn't have a name:
```javascript

var sayHello = function(name) {
    return "Hello, " + name;
};

```

#### hoisting - when you define a var before you define it, ex. at the top of a file when it is defined later in the code
```javascript

var name = "Tim";

function sayName() {
    console.log(name);

    var name = "Whiskey";
}

sayName(); // returns undefined

```
*but if you do it like this:*

```javascript

var name = "Tim";

function sayName() {
    console.log(name);

    name = "Whiskey";
}

sayName(); // returns "Tim" - variable is only scoped inside function if the var name is used

```

### IIFE - "Immediately Invoked Function Expression"

```javascript

// function is wrapped in parentheses to invoke an expression
var myFunc = (function(fname, age) {
    return {
        name: fname,
        printAge: function() {
            console.log(age);
        } // this is a closure
    };
})(); // these final parentheses immediately call function

```
_JS (unlike Python) doesn't need to pass parameters to call a function_
```javascript

// myFunc is an object
var myFunc = (function(fname, age) {
    return {
        name: fname,
        printAge: function() {
            console.log(age);
        } // this is a closure
    };
});

var result = myFunc("Isabelle", 26); // here, result is a function
result.printAge();
result.name;

```



Exercise: create an IIFE that takes a first name, last name, and age, and prints them all out.

```javascript

var printNameAge = (function(fname, lname, age) {
    return {info: function() {
        return fname + " " + lname + ", Age " + age ;
        }
    }; 
})("Isabelle", "M", 26);

printNameAge.info(); // returns string 

```

When do you want to use IIFEs?
  - When you want to create a "singleton" - an object in your code that only exists once, ever. The advantage of this over a function that can be called over and over is that the IIFE keeps its own state, so that if one of the parameters is changed it is maintained throughout the object (using this.[parameter]). The object serves as a bundle that can be passed around with its own state. Used if you want to create only one of something but not more.

### Higher Order Functions & Callbacks
-common in array iterators (map function) & with setTimeout

Callback functions are functions given to other functions to be invoked later:

```javascript

var yell = function() {
    console.log("YELLING");
};
setTimeout(yell, 3000); // invokes function in 3000 milliseconds
// setTimeout is the higher order function
// yell is the callback function - should not be yell() to prevent it from being prematurely called

```

```javascript

var yell = function() {
    console.log("YELLING");
};

console.log("before");
setTimeout(yell, 0); 
console.log("after");
// will print "before", "after", "YELLING" - setTimeout puts it on the queue to be run at the end of loaded code

```
_single-threaded applications only allow one thing to happen at a time - things do not happen concurrently_
_JS does asynchronous input & output but code runs top to bottom_
_setTimeout is not asynchronous but simply adds things to the browser queue_

#### Array Iterators

Iterating over an array with a for-loop:
```javascript

var arr = [4, 5, 6, 7, 8];
var newArr = [];
for (var i=0; i < arr.length; i++) {
    newArr.push(arr[i] + 1);
}
console.log(newArr);

```

Iterating over an array with map function:
```javascript

var arr = [4, 5, 6, 7, 8];
var newArr = [];
arr.map(function(el){
    newArr.push( el + 1 );
});

console.log(newArr);

```







