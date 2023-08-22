- good websites to work on practice problems: https://exercism.org/tracks/javascript/exercises/lasagna (already made a github account)
	- Code wars(looks like it lets you skip the trivial ones): https://www.codewars.com/
	- W3schools (has a directory of specific js disciplines and exercises for it): https://www.w3schools.com/js/exercise_js.asp?filename=exercise_js_variables1
### Parking lot for review in foundational JS
#### How to store html elements and add event logic
- use store as a variable with `document.querySelector(".className");`
	- mind that this is for one element and use `querySelectorAll(#idname);` for multiple elements
- for logic you can use `varName.addEventListener("click", (e)=>{...});` 
	- notice that event listener method appended to the variable name, and notice the thing listening for in quotes and the arrow function capability, *and the presence of e* which passes through event information accessible through dot notation or bracket notation.
#### DOM manipulation methods
- changing the inner contents of the element
- how to find the children of a target element
#### Javascript Array methods
- Appending to an Array: 
	- `arr.push(objectToPush);` no need to put brackets to the array name.
- removing an element or replacing to array: 
	- `arr.splice(indextoremove,howmanyindextoremove)` 
- find in an array a specific element
	- `arr.some((item) => item.title === newBook.title);` 
		- this will return a true/false if it finds in the array matching 

#### Creating Data-attributes with JS
- you can create a specific index number for an element that was dynamically created using javascript with data-atrributes with the following: `elementVar.dataset.index` 
	- *note the .index is actually what you can name the data attribute and it appears as data-index* 
#### dialog boxes as form popups
 see [[Intermediate CSS#Styling Forms]] to see it's implemenation with html. 
	 once the html is populated, you'll need to store the button to pop up the form, the form itself, and a cancel button for the form.
```javascript

const updateButton = document.getElementById("updateDetails");
const cancelButton = document.getElementById("cancel");
const dialog = document.getElementById("favDialog");
dialog.returnValue = "favAnimal";

function openCheck(dialog) {
  if (dialog.open) {
    console.log("Dialog open");
  } else {
    console.log("Dialog closed");
  }
}

// Update button opens a modal dialog
updateButton.addEventListener("click", () => {
  dialog.showModal();
  openCheck(dialog);
});

// Form cancel button closes the dialog box
cancelButton.addEventListener("click", () => {
  dialog.close("animalNotChosen");
  openCheck(dialog);
});
```
 - notice the `dialog.showModal()` method and the `dialog.close()`to open and close. *not too sure what the "animalNotChosen"* part is for though. #NeedMoreHelp 
#### using Form data without POST / GET
if you just want to use the form values within js, you can: 
	1. store reference to form by class or element
	2. add event listener `submit` and an arrow or defined function passing through `event` parameter
	3. add `formVar.preventDefault()` to stop the form from trying to send to a server
	4. access form data using variables and getelements by id or class: 
ex: 

```javascript
addForm.addEventListener("submit", (event)=>{

event.preventDefault();
dialog.close();
createBookObj();
})

  
function createBookObj(){

let author = document.getElementById("title").value;
let title = document.getElementById("author").value;
let pages = document.getElementById("pageNum").value;

//boolean that checks the value of read and returns t/f

let readStatus = document.querySelector("input[name=readStatus]:checked").value === "read" ? true : false;
let bookToAdd = new Book (title, author, pages, readStatus);
console.table(bookToAdd);
appendLibArr(bookToAdd);
}
```
- note the variables being initialized and storing the different form inputs. 
- note the unique radio value being accessed by using the name and specifically accessing the one that is checked. dont really understand why you need the `:checked` #NeedMoreHelp 
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
example of applying this syntax to print out a books information: 
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

#### factory functions and the module pattern
- turns out constructors aren't that favored , they can lead to some bugs that don't really give you error messages. many people prefer factory functions.
	- for one, you need to use the `new` keyword and if you forget it, it will behave strangely but again, no error messages.
	- What are factory functions?
		- creating objects by returning them insteading of using arguments in a function to assign key:value pairs.

```javascript
javascript
const FactoryFunction = (string) => {
  const capitalizeString = () => string.toUpperCase();
  const printString = () => console.log(`----${capitalizeString()}----`);
  return { printString };
};

const taco = FactoryFunction('taco');

printString(); // ERROR!!
capitalizeString(); // ERROR!!
taco.capitalizeString(); // ERROR!!
taco.printString(); // this prints "----TACO----"
```
- couple things here, not passing through string for the factory. note the return of `printString` as an object. which will give you access to that method when creating instances of the functions as variables. 
	- note also the other methods you dont' have access to because they're not returned but you can still access them throuh the method that was returned. this pattern of closing off certain methods or emulating their privacy is called closure. 
- inheritance with factories
	- just like constructors with prototypes, you can copy over functions and values from other factory functions to use in another using the `const {sayName} = Person(name);` where the {sayName} is created and set equal to Person(name) which is itself another factory function that has a function by the same name, sayName which is invoked when name is passed to Person. still kinda hazy #NeedMoreHelp 
- more on differnet patterns for inheritance in JS: https://medium.com/javascript-scene/3-different-kinds-of-prototypal-inheritance-es6-edition-32d777fa16c9
	- also talks about compositional inheritance being better than classes but didnt really look into why #NeedMoreHelp 

- What is namespace?
		- its sometimes used interchangably with the word scope, but it's specifically the highest level of scope, the global scope
	- what is lexical scope? 
		- variables or statements inside anotehr function, is under lexical or static scope or closure. static meaning accessible only within the scope of the function
	- What is the difference between expressions and statements?
		- expressions are bits of code that produce something 2+2 has the expression of 2, 2 and 2+2. each of those can be separate expressions 
		- statements are sequence of instructions for the computer to do something. statements have slots for expressions to come in 
			- ex: let `hi =` <- statement and the expression is the 5 assigned to the `let hi =` 
			- staements are the rigid structure of our programs and the expressions populate or fill in the details. strings, floats, longs, etc. as long as it can be value produced.
			- one handy way to tell is if you try to console.log it,if it works, its an expression and if it doesnt, it's a statement unless its not actually js of course.
	- what is .call() and .apply()? 
		- allow you to call a function and change its scope to change the contextual invokation of `this` looks like this, `funcName().call(links[i]);` the links "i" is something in the lexical scopeinside of the function but that can be brought out with the call and putting as argument what you''re trying to have come to a further scope up. Don't fully understand this though, will need to come back to this. #NeedMoreHelp 
	- what is .bind()?
		- a method that prevents methods that passthrough another functions with arguments from invoking immediately. 
ex: 
```javascript
nav.addEventListener('click', toggleNav, false); // will invoke the function immediately 
nav.addEventListener('click', toggleNav(arg1, arg2), false);
```
- normally you would fix this by putting another function inside of the event listener but you can also sollve this by calling the fucntion togglenav with bind with the arguments passed through without having to needlessly create another scope just to be able to pass the arguments. 
#### Private/Public scope and the Module pattern
- while JS does not do private and public scope like something like c# does, it can emulate it by making closures like seen with the module pattern. emulates it by keeping it out of the global scope. 
	- because its nested in a function you wont actually be able to call it because its not defined in the global scope. 
	- in order to call it , you use the module object pattern to create an object and call the object method. 
ex: 
```javascript
// define module 
var Module = (function () { 
	return { myMethod: function () {
	}, someOtherMethod: function () {
	 }
	  }; 
	  })(); 
	  // call module + methods 
	  Module.myMethod(); 
	  Module.someOtherMethod();
```
- so here we have methods that are nested privately but you can stil use them outside and not polluting the global namespace
- notice at the end it's returning the functions being delcared. 
- *essential for a module to be wrapped in the IIFE parentheis. see below for more*
- this is known as good code security, the less global these functions are the less likely they can access the data inside them. 
	- one naming convention is to start private methods with an underscore
- more on this and other patterns for organizing without cluttering: https://ultimatecourses.com/blog/everything-you-wanted-to-know-about-javascript-scope
**What is that (); at the end of the module?**
	- this is known as wraping a function (factory function) in whats called an IIFE or immediately invoked function expression
	- difference between function declaration and function expression: 
		- functions declared in a block are nomrmal function declaration. 
		- if you assign function as a variable, you are initializing function expression
			- key is that function expressions return values. either data type or another function even
			- to turn a regular function declaration to anexpression it's a simple as wrapping it in the parenthesis and add another set at the end. 
	- the reason why you do it is for privacy without unnecessarily taking a name in the global namespace. 
- Modules in general present good ways to create a factory function that doesnt need to be replicated tons of times, like if you only need one and need access to the methods in them. 
- another useful purpose of encapsulating some of our functions is to avoid *namespace collisions*. this is when you have say `add` function in three different places throughout your code, and they're all describing what the function does but it would conflict with other declarations of that function name so it would be nice of those other instances could be nested or encapsulated where they were needed but didnt need to be scoped in the global. 

another example showcasing private vs public methods in Module objects: 
```javascript
var Module = (function () { 
 var _privateMethod = function () { 
 }; 
 var publicMethod = function () {
  };
   return { publicMethod: publicMethod, ew
   anotherPublicMethod: anotherPublicMethod
    } 
    })();
```
again we see here returning the methods kinda like the factory functions pattern described above.
- what is the difference between function scoped and block scope?
	- function scope a variable is confined to a function specifically and block can be anywhere there are curly braces. 
- great video series on using modules in JS: https://www.youtube.com/playlist?list=PLoYCgNOIyGABs-wDaaxChu82q_xQgUb4f
#### Classes
getting started with classes: 
- class keyword is a syntax for making objects using functions. it has special attributes such as setting all methods in it to be non enumberable, meaning in a loop, it wont loop over the methods(which we usually dont' want, we want the properties like key:value pairs);
	- other ways that it's different from object constructors: 
		- function created by class lableed with special internal property `isClassConstructor`
		- classes always use `strict` and everything inside of it is automatically in strict mode. 
			- strict makes it easier to write safe code that throws errors with "bad syntax"
```javascript
class User {

name = "John";
age = 45;
sayHi() {
	alert(`Hello, ${this.name}!`);

	}

}

new User().sayHi(); // Hello, John!
```
 - notice the use of the `new` keyword that is necessary for instantiating new classes.
more on class basics: https://javascript.info/class
- what is temporal dead zone? 
	- class declarations have this along with let and const variables that will throw reference error if called befor they've been initialized. in contrast to function declarations and something like the var variable which will return 'undefined' if called before initialized. 
- option to have `static` fields: see more[[Full Stack Parking lot]]
##### field declarations
- class fields are syntax to create classes where fields are similar to object properties as opposed to variables, so no var, const or let keywords. 
```javascript
class Rectangle {
  height = 0;
  width;
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

```
- there public and private class fields: 
	- public: enumerable and configurable, writable the participate in prototype inheritance. 
	- private: only accessible from within the class body cannot be accessed from the outside
ex of public class fields: 
```javascript
class Rectangle {
  height = 0;
  width;
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```
- notice the constructor method here which is only allowed once in classes to instantiate new copies of it. 
ex of private class fields: 
```javascript
class Rectangle {
  #height = 0;
  #width;
  constructor(height, width) {
    this.#height = height;
    this.#width = width;
  }
}
```
- this time notice the hashtag which indicates private fields
##### inheritance
- use the keyword `class Lion extends ParentClass {...} 
	- notice the extends and the class you want to inherit from comes afte the present class name. 
	- extends sets the prototype for both the childclas and the childclass prototype
	- if the extends class is going to employ a constructor, it needs to use the `super();` method before using `this` 
		- `super` used in two ways:
			- Property look up: to access properties of an object or class prototype. if you are accessing properties then you need to put that property inside super as an argument
			- function call :  if you're acessing methods from the super class then you need `super().methodName` 
**Binding and unbinding**
- binding is a method `bind()` that when called in a function instance, will bind the `this` where called to the value being passed through. 
```javascript
const module = {
  x: 42,
  getX: function () {
    return this.x;
  },
};
const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// Expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// Expected output: 42

```
  - you see here that unboundGetx is not able to call the method in module until it was bound with the original object declaration. 
	  - if playing with this and get unexpected results, see this article in context: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind
##### mix-ins
- seems to be a syntax to allow the chaining of superclasses to chain inheritance, see more in context https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends#mix-ins
- here is a video where fireship talks about mixins, skip to about 8:30:https://www.youtube.com/watch?v=fsVL_xrYO0w&ab_channel=Fireship

##### getters and setters
what are getters and setters?
	- getters are ways of accessing return values of object functions within say an object literal syntax
	- setters are ways of updating or changing data inside of those fuctions or objects 
```javascript
get name(value) {
		 ...return this._name;
}
set name(value) {
	...this._name = value;
}
```
- you can see the get/set keywords in action here

##### composition vs inheritance
- inheritance involves making a sublcass of a parent class and the two are strongly coupled and there are some issues with subclassing such as potential security risks
	- inheritance is when you define your objects around what type they are
	- it forces the developers to build a strong taxonomy of their objects early on in the development process and people cannot predict the future and if you are deep in it's hard to get out
- composition is when you have a property that stores reference to another object of another class and use the features within it. it usually results in more code duplication but does not easily break if the other class its borrowing from changes. 
	- inheritance is when you define your objects around what they do. 
```js
class ReadOnlyMap {
  #data;
  constructor(values) {
    this.#data = new Map(values);
  }
  get(key) {
    return this.#data.get(key);
  }
  has(key) {
    return this.#data.has(key);
  }
  get size() {
    return this.#data.size;
  }
  *keys() {
    yield* this.#data.keys();
  }
  *values() {
    yield* this.#data.values();
  }
  *entries() {
    yield* this.#data.entries();
  }
  *[Symbol.iterator]() {
    yield* this.#data[Symbol.iterator]();
  }
}
```
- to note here is how private field `#data` is set equal to a new instance of other class Map
	- don't really know what the star is though #NeedMoreHelp looks like a fucking pointer
- good video illustrating how to use composition to allow greater flexibility in functionality of objects. 