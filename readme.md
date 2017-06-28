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

_hoisting - when you define a var before you define it, ex. at the top of a file when it is defined later in the code_
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
var result = (function() {
    return {
        name: "Isabelle",
        printAge: function() {
            console.log(26);
        }
    };
})(); // these final parentheses immediately call function
```


