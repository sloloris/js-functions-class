### Function Declarations vs. Function Expressions

- function declaration has a name & exists in the code base before code runs - meaning it can be run before it is defined in the code
```javascript

function sayHello(name) {
    return "Hello, " + name;
}

```
- function expression - function only comes into existence when the assignment happens - it doesn't exist prior because it doesn't have a name:
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





