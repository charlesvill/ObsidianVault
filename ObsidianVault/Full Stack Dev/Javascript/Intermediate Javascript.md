- good websites to work on practice problems: https://exercism.org/tracks/javascript/exercises/lasagna (already made a github account)
	- Code wars(looks like it lets you skip the trivial ones): https://www.codewars.com/
	- W3schools (has a directory of specific js disciplines and exercises for it): https://www.w3schools.com/js/exercise_js.asp?filename=exercise_js_variables1
### Organizing Code
- the language is extremely forgiving which is in part enabling for poor design choices that lead to poor maintainability.
	- the discussion on organizing code is going to come down to 4 categories:
		- Plain JS Objects and Object Constructors
		- Factory Functions and Module Pattern
		- Classes
		- ES6 modules
#### Objects and Object Constructors
 review on objects: 
 good source of review on objects:https://javascript.info/object
 - there is the object constructor or the object literal syntax for declaring an object but it's largely seen as better to use the literal syntax: 
```javascript
const myObject = {
  property: 'Value!',
  otherProperty: 77,
  "obnoxious property": function() {
    // do stuff!
 }
}
```
- as seen above, you have *key:value* pairs at play here storing different kinds of data even functions with strings. 
	- Accessing this data: 
		- There is dot notation and bracket notation. dot notation is usually the best one but there will be circumstances when it will be necessary to use bracket notation like in the case of the string property "obnoxious property" seen there. 
		- ex: `console.log(myObject.property);` will print //Value! 
		- bracket: `myObject["obnoxious property"]` // produces the function. 
	- Other nuances with bracket vs dot notation:
		- you also cannot use dot notation if you're trying to retrieve something using a variable. 
			- ex `const variable = 'property'`  `myObject.variable` 
				- this will return null becuase it will be looking for a property called variable which does not exist. this works though to pass 'property' through to the object to find a property called 'property' ex: `myObject[variable]`. //returns 'Value!'
	- Adding data: 
		- you can declare: `myObject.myBool = false;` or `myObject["Charles Villalpando"] = true;` 
	- Deleting data: 
		- use command `delete myObject.myBool;`
	- What are *Computed Properties*?:
		- it is when you use brackets in the object literal to define the name as a variable that exists outside of the object
ex:
```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {

[fruit]: 5, // the name of the property is taken from the variable fruit

};

alert( bag.apple ); // 5 if fruit="apple"
```
- so here we have the property `[fruit]` that will be named by the input of the prompt if it matches 'apple'
	- *note: dont be confused by the second argument in the prompt method, it simply gives a conditional that will match and return the second argument if the prompter's input matches*
- how do we test if a property exists in an object?
	- "in" operator: `alert( "property" in myObject)` returns a true/false in this case a true; 
		- uses ' ' string to check for property but you can also use a variable that exists outside the object that is equal to the string that would match a property in the object like so = `alert (key in myObject);` when you previously declared key = "property". 
- For in loops
	- in order to iterate through the properties in the object, you can use a for in loop like so:
		- `for (key in object){ // loop body }` key is the variable being declared to store the property you're iterating over

##### objects as a design pattern
one way to organize code is to grouping things like repeated variables into objects for example if your storing the names and scores of a number of players you could store them in objects for each of the players instead of cluttering your code with variable declarations 

##### Object constructors
when needing to duplicate the making of objects in code as a function, like when needing to create an inventory of items to sell, it is not feasible to manually type out those objects yourself.
- syntax: 
```js
function Player(name, marker) {
this.name = name
this.marker = marker
}
```
- then you could call the function to create the new object with the keyword `new` 
```javascript
const player = new Player('steve', 'X')
console.log(player.name) // 'steve'
```
- you can also add functions to the object: 
	- first declare the function like above but add a function after and have the function called sayName() print the `name` . 
	- and you can access that function `alert(Player.sayName())` // prints out value for key `name`
example of applyig this syntax to print out a books information: 
```javascript
function Book (title, author, pages, read){
    this.title = title;
    this.author = pages;
    this.pages= pages;
    this.read = read;
    this.info = function(){
        let readResponse; 
        if (read === true)
        {readResponse === "have read";}
        else{readResponse === "not read yet";}
    return (`${title}, by ${author}, ${pages} pages, ${readResponse}`);
  }

}

const lotr = new Book("The Hobbit","J.RR Tolkien", 456, false);

lotr.info();

```
//`'The Hobbit, by J.RR Tolkien, 456 pages, undefined'`

##### The Prototype
- all objects in js have a prototype. 
	- what does that mean?
		- any object constructor or literal you create will have another copy of itself as an object that serves as a pool for methods and data that will be shared amongst the many instantiations of the object constructor that you may have. 
		- ex: looking at the book example, if you have a thousand books, you will have 1000 instantiations of the info function. so much memory could be saved if we were to just pool that function and other repeatedly accessed data in a prototype that the instantiation of the specific `Book` object can inherit methods from
		- this above is called prototypal inheritance
	- Characteristics: 
		- its mutable meaning that you can add, change the functions present in the Book.prototype. 
		- comes with certain built in methods and properties
		- allows for two or more objects to be linked and access each others methods even if they're not explicitly decared in their own respective object declarations (inheritance)
		- when you try to access a property or method, JS will first check the declared object and then the property if it was not found on the original object (the one declared)
		- at the end of the chain is Object.prototype and it's methods and properties. any efforts to look past that will return in null. the chain could look like this:
			- Book{}, Book.prototype{}, Object.Prototype{}. <- end of the chain
- Syntax: 
	- to find the prototype use `getPrototypeOf()` method and a object literal or constructor goes inside there.

```javascript
function Hero(name, power){
this.name = name;
this.power = power;
}

Hero.prototype.greet = function () {
	return `${this.name} says hello.`;
}

//fig.1 here we see instantiation of Hero with the name gorgon
let gorgon = new Hero("Dungarth", 9000);

//and here we see gorgon object accessing the newly created method in the prototype object despite not being in the constructor.
console.log(gorgon.greet);
```
This here is declaring a function within the prototype of Hero{} that can now be used by any instantiation  of Hero there after as seen in fig. 1
- Copying over properties from one constructor to another: 
	1. use the `call()` method in the declaration of a object as seen:
```javascript
function Warrior(name, level, weapon){
	//chain constructor with call
	Hero.call(this, name, level);
	this.weapon = weapon;
}
const paul = new Warrior("paul", 3 , "axe");
paul.();
```
what the call method is doing here is it's copying over the methods and properties that the Hero object has
	*when you try to access properties from futher down the chain, specifically from prototypes call will not work* for example if Hero has the greet() on its prototype and not on its declaration, it will not work. for that, you'll need `Object.setPrototypeOf()` to share the prototype properties and methods as well
		- as seen in fig 2, the inheriting object goes first

```javascript
// Initialize constructor functions
function Hero(name, level) {
  this.name = name;
  this.level = level;
}

function Warrior(name, level, weapon) {
  Hero.call(this, name, level);

  this.weapon = weapon;
}

function Healer(name, level, spell) {
  Hero.call(this, name, level);

  this.spell = spell;
}

// Link prototypes and add prototype methods
//fig. 2syntax is (reciever, giver)
Object.setPrototypeOf(Warrior.prototype, Hero.prototype);
Object.setPrototypeOf(Healer.prototype, Hero.prototype);

Hero.prototype.greet = function () {
  return `${this.name} says hello.`;
}

Warrior.prototype.attack = function () {
  return `${this.name} attacks with the ${this.weapon}.`;
}

Healer.prototype.heal = function () {
  return `${this.name} casts ${this.spell}.`;
}

// Initialize individual character instancaes
const hero1 = new Warrior('Bjorn', 1, 'axe');
const hero2 = new Healer('Kanin', 1, 'cure');
```

**correct order of accessing prototypes**
- to avoid issues and inefficiency, the .setPrototypeOf part needs to be done before any other methods are declared and before any instantiations of the objects
- How to find the next stop in the chain of protoypes?
	- use the command `Object.getPrototypeOf(Hero.protype)` 
##### This keyword
the mystery of `this` and its meanings across contexts article: https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/
- in many places the use of `this` is purely contextual to the scope that its used in. in javascript however, it is used based on the context in which the function was invoked
- another explanation is that `this` is the reference to the current running function 
- difference between a function and a method: 
	- a method uses accessors and create a method invocation looks like: `[1, 5].join();` the way that this uses the dot notation to access javascript methods is a tell tale sign. functions on the other hand are just executed not accessing any objects
		- so a function is just the list of instructions in the function body and a method is the same thing but accessed through an object. perhaps technically speaking C does not have methods because it does not have objects
- the `this` keyword will refer to different things depending on the scope that its being called in. for example, if its being called in the global scope, like `alert(this)` the this being referred to is the window, browser, the highest level. 
- in other instances, for example if a function is declared inside of an object, and that function is called outside of it, this will still refer to the object that is being accessed. `user.fullName()` the this inside of this function will point to user object. 
	- *an arrow function inside of an object will not operate the same way. it will inherit the closest normal function which could be window or global scope.*
	- see the top lesson on object constructor and prototyping for more resources. 