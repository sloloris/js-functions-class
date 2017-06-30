_Everything covered here applies to ES5; ES6 introduces extend to cover prototypal inheritance._

[See here for the instructor's repo.](https://github.com/parkerlewis9/Prototypal-Inheritance)

### Prototype Chain
All objects in JS have a hidden ```__proto__``` property, or the object's prototype, which points to another object containing other methods applicable to the first object. The protoype chain refers to the way each object can call on the methods of its prototype object.

Note: the object at the top of the prototype chain's ```__proto__``` points to null.

### 'new' keyword
2 common ways to create objects:
1.
```javascript

var isabelle = { 'name': 'Isabelle' }

```
2. call a constructor function (used to create objects & initialize them with keys and values):
```javascript

var isabelle = new Object()
// initiated object is empty

```
This sets up the prototype chain for us by setting up the ```__proto__``` to point to wherever Object.prototype is pointing to. So here: isabelle.prototype === Object.prototype (same location in memory!)
Note: All objects have a .prototype method (differentiated from ```__proto__``` prototype)

### Object.create
To extend an object's properties to another object, set ```__proto__``` on the latter's constructor function to the former using Object.create.

Object.create allows us to create an empty object and set its ```__proto__``` property. 

```javascript

// ES5
ChildObject.prototype = Object.create(ParentObject.prototype)
// make sure to also overwrite the constructor so that it doesn't inherit directly from object
ChildObject.prototype.constructor = ChildObject 

```
example:
```javascript

function Animal (name, age) {
    this.name = name;
    this.age = age;
}

function Dog (name, age, breed) {
    Animal.call(this, name, age) // extends this.name and this.age from Animal
    this.breed = breed
}

Dog.prototype = Object.create(Animal.prototype)
Dog.prototype.constructor = Dog

var scout = new Dog('scout', 6, 'golden retriever')

// scout.__proto__ === Dog.prototype // because the new keyword was used

````

Classes in ES6 are a syntax layer on top of traditional ES5 prototype objects. 
In prototypal inheritance, methods on each instantiated prototype point to the SAME method in memory; in classical inheritance (like in Python), the classes each create their own instances of the methods. This makes JS prototypes more memory-efficient.