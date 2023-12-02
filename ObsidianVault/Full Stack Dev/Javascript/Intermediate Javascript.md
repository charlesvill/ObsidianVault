- good websites to work on practice problems: https://exercism.org/tracks/javascript/exercises/lasagna (already made a github account)
	- Code wars(looks like it lets you skip the trivial ones): https://www.codewars.com/
	- W3schools (has a directory of specific js disciplines and exercises for it): https://www.w3schools.com/js/exercise_js.asp?filename=exercise_js_variables1
	- good website for best practices on application design principles: https://12factor.net/dependencies
	- JS design standards: AirBnb style guide: https://github.com/airbnb/javascript
### Parking lot for review in foundational JS
- I fucking suck at recursion. need to come back to this assignment: https://www.codingame.com/playgrounds/5422/js-interview-prep-recursion
	- refer to the think like programmer book section on recursion 
	- the gap seems to be limited perspective on options I have to traverse through objects recursively devell
-[ ] what does it mean to be hoisted? 
	- understanding roughly is that it's really easy to attempt the call of a function prematurely
- what are generator functions used for ?
- [ ] what are the functions declarations that will execute immediately and which are the ones that need be called or invoked before they're actually executed? is there a specific pattern in the ones that execute immediately that one should be aware of? for example in the call back function of an eventhandler, you cannot but the function call itself because it will get called before the actual event is triggered. perhaps its because it requires a call back function that it will invoke on compilation instead of trigger event. a call backfunction initializes itself as a statement but does not invoke its contents while just putting the function name could be triggering it to actually load the contents instead of just initializing itself. 
- on performance, see chapter 5 and 6 of you dont know javascript for how to make javascript performant: https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch3.md

#### Review on javascript fundamentals: 

##### string methods: 
- splitting a string into array of sub strings at a character(s): `string.split(' ')` 

##### array methods: 
- length of an array: `arr.length`
- remove the first element of array: `arr.shift()` if you set a variable equal to it, it will return the removed element.
- removing, replacing, adding elements to array: `arr.splice()` takes a few arguments but the what it does: 
	- `splice(start, deleteCount, item1, item2, /* …, */ itemN)` anything after second parameter are just things to add
- Appending to an Array: 
	- `arr.push(objectToPush);` no need to put brackets to the array name.
- find in an array a specific element
	- `arr.some((item) => item.title === newBook.title);` 
		- this will return a true/false if it finds in the array matching 
- joing elements of an array to a string: 
	- arr = ["hello", "world"] `arr.join(", ");` this will result in Hello, world
		- if there is only one element in the array then it will simply output the one element without the delimiter
- create a shallow copy of an array with elements that pass the test 
- object/array destructuring - why its useful and how to use it and using the spread operator
	- destructuring takes a longer collection of data say a object or an array and parses it into smaller chunks
	- `const arr = [1, 2, 3, 4, 5, 6]; const [a,,c, ...rest] = arr`
		- what this is doing is declaring three different variables a, c, rest that destruct parts of that array. the spread operator there is pulling the rest of the elements and creates an array which prints out the remaining elements from arr.
	- combining the spread operator with objects proves to very useful as objects dont have the same array methods. 
		- returning more than one value from functions
		- ` function sum&mult(a,b) {return [a+b,a*b]}`
			- `const [sum, multiply] = sum&mult(2,3)`
			- this allows you to declare two seperate variables using deconstructor and you can call each of those variables independent of each other
		- combine objects and overwrite present properties and also pull from objects what we need:
```javascript
const personOne = {
	name: 'Kyle', 
	age: 24,
	address: {
		city: 'somewhere',
		state: 'One of them'
		}
}

function printUser({name, age, favoriteFood = 'watermelon'}){
	console.log(`name is: ${age}. Food is ${favoriteFood}`)
}

printUser(personOne)
```
- as can be seen here, print user is taking object personOne and destructing just the parameters listed there and can even call ones that are not present there and give them a default value. 
	- *in context: see composition to see how this can be applied to make object constructors that dont fall to strong taxonomical restraints* [[#composition vs inheritance]]
- What is the rest parameter syntax? 
	- this is when you want to allow a function to take more arguments `function (a, b, ...restParams)` 
		- common convention to call it 'restParams' but saves as an array and you access the parameters by index
#### How to store html elements and add event logic 
- use store as a variable with `document.querySelector(".className");`
	- mind that this is for one element and use `querySelectorAll(#idname);` for multiple elements
		- you'll need a forEach loop to add event listeners for more than one: `nodeList.forEach(element => element.addEventListener("click", (e)=>{...});` where *e* is event information of the specific element that triggered the event handler
- for logic you can use `varName.addEventListener("click", (e)=>{...});` 
	- notice that event listener method appended to the variable name, and notice the thing listening for in quotes and the arrow function capability, *and the presence of e* which passes through event information accessible through dot notation or bracket notation.
#### Handling User Input
- for key input: 
	- 
- for click input: 
	- see above to add event listeners to DOM elements like divs, or buttons

#### DOM manipulation methods
- changing the inner contents of the element
- how to find the children of a target element
#### Javascript Array methods

#### Creating Data-attributes with JS
- you can create a specific index number for an element that was dynamically created using javascript with data-atrributes with the following: `elementVar.dataset.index` 
	- *note the .index is actually what you can name the data attribute and it appears as data-index* 
#### Modifying classList names
- for the purposes of toggling something on and off for styling purposes: 
	- use the `classList.toggle("className");` and just add the event listener that triggers a function with this code in it. the language keeps track of the conditional logic for you so you dont have to make nested conditionals to handle the adding and removing of class names
- *useful classList methods* : 
	- classlist.contains("") T/F if the element contains said class (which would have saved so much time had I known about it earlier)
	- changing classes: in order to dynamically add or change a class for the purposes of say adding transitions with css: 
		- you need to get reference to the classlists (if you have more than one, you'll need to remove the one related to the class transitions)
```javascript
function classChange(className){
	sliderCont.classList.remove(sliderCont.classList[1]);
	sliderCont.classList.add(className);
}
```
 - now this is not the most elegant of solutions but allows you to replace the second one dynamically without having to know what class is currently taking up that second slot. and this is on the fly to be hooked up to an event handler and get those lit transitions see [[Intermediate CSS#Transitions]]
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
##### Useful methods for foundations 
- `console.dir()` - a useful way of listing out the properties of some variable or object in js
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
##### "This" keyword
the mystery of `this` and its meanings across contexts article: https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/
- in many places the use of `this` is purely contextual to the scope that its used in. in javascript however, it is used based on the context in which the function was invoked
- another explanation is that `this` is the reference to the current running function 
- difference between a function and a method: 
	- a method uses accessors and create a method invocation looks like: `[1, 5].join();` the way that this uses the dot notation to access javascript methods is a tell tale sign. functions on the other hand are just executed not accessing any objects
		- so a function is just the list of instructions in the function body and a method is the same thing but accessed through an object. perhaps technically speaking C does not have methods because it does not have objects
- the `this` keyword will refer to different things depending on the scope that its being called in. for example, if its being called in the global scope, like `alert(this)` the this being referred to is the window, browser, the highest level. 
- in other instances, for example if a function is declared inside of an object, and that function is called outside of it, this will still refer to the object that is being accessed. `user.fullName()` the this inside of this function will point to user object. 
	- *an arrow function inside of an object will not operate the same way. it will inherit the closest normal function which could be window or global scope.*
		- useful to use arrow functions when operating within a class, because a regular function inside the class could encapsulate and deny access to the thing you're trying to access, so the arrow function will name this as the class scope instead of the function. 
			- ex: you're trying to access an array that is declared in the class but youir calling a method to splice that array from a method inside the class but not in the same scope persay as the array. 
	- see the top lesson on object constructor and prototyping for more resources. 

#### factory functions and the module pattern
- turns out constructors aren't that favored , they can lead to some bugs that don't really give you error messages. many people prefer factory functions.
	- for one, you need to use the `new` keyword and if you forget it, it will behave strangely but again, no error messages.
	- What are factory functions?
		- creating objects by returning them insteading of using arguments in a function to assign key:value pairs.

```javascript
function createUser (name) {
  const discordName = "@" + name;

  let reputation = 0;
  const getReputation = () => reputation;
  const giveReputation = () => reputation++;

  return { name, discordName, getReputation, giveReputation };
}

const josh = createUser("josh");
josh.giveReputation();
josh.giveReputation();

console.log({
  name: josh.discordName,
  reputation: josh.getReputation
});
// logs { name: "josh", reputation: 2 }

//then extending the functionality of createUser with desctructors
function createPlayer (name, level) {
  const { discordName, getReputation } = createUser(name);

  const increaseLevel = () => level++;
  return { name, discordName, getReputation, increaseLevel };
}

```
- notice here that things being returned are those things that you might anticipate having to access. anything that just works in the side lines are private scoped and are not returned
- inheritance with factories
	- this is how you would extend the functionality of your objects again notce that createPlayer is importing the functionallity of createUser by using the destructor. also note that we still must return the functions from createUser to use them as well.
	- this method of destructoring can be seen in [[#Parking lot for review in foundational JS]]
- more on differnet patterns for inheritance in JS: https://medium.com/javascript-scene/3-different-kinds-of-prototypal-inheritance-es6-edition-32d777fa16c9
	- also talks about compositional inheritance being better than classes because classes force you to use inheritance which can cause issues when you want to implement features into say a penguin object that doesnt exactly conform in the right way with the parent class bird, because penguins fly. 

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
useful video on classes: https://www.youtube.com/playlist?list=PLtwj5TTsiP7uTKfTQbcmb59mWXosLP_7S

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
	- don't really know what the star is though #NeedMoreHelp looks like a fucking pointer , honestly this was a poor example, here is a better one: 
```javascript
function flyer({ name }) {
	return {
	fly: () => console.log(`${name} flew`)
	}
}

function attacker({ name }) {
	return {
	attack: () => console.log(`${name} attacked`)
	}
}

function flyingMonsterCreator(name) {
	const monster = { name: name }

	return {
		...monster,
		...attacker(monster)
		...flyer(monster)
		}
}
```
- good video illustrating how to use composition to allow greater flexibility in functionality of objects. 

#### ES6 Modules
- different than the modules pattern
##### first a history lesson on javascript and its evolution 
why do we have npm?
	because it was easier to manage packages and libraries when they updated or patched. the package manager did it for you and the json would automatically list the dependencies. 
why do we have nodejs?
	js did not originally have any sort of way of bundling files or code to import to different projects or code bases bc it was not meant to be working anywhere else except the browser. so Node Js was created to allow you to work with js offline without the use of global variables of code scripts you perhaps did not need. export code across files. 
##### what are modules exactly?
when you build projects, it will be useful to import libraries or resuse code that you have built in other projects. well it can get really complicated managing these files and also bloats your packages when you have all the depenencies available in your html files even if some of the js scripts dont use the libraries. 
	solution is to use modules to bundle these dependencies. 

**what is webpack?**
- webpack is a module bundler installed with npm 
	- getting started: see webpack docs: https://webpack.js.org/guides/getting-started/
	- how its working:  webpack once installed reads all your import statements and bundles them in an output location usually called /dist folder that will be the code actually running on the browser for production. 
		- it does something called transpiling code for development side libraries like typescript or SASS (development side meaning that it's not a dependency that will be for client side but more to aid devleopment) 
			- transpiling is when it converts the similar language like typescript or SASS to its respective language. 
**import**
- used to import read-only live bindings. 
	- called live bindings bc it can be updated by the exporting module but not altered by the imported module. 
	- by definition, *binding* is association of an identifier and a value. like variable and its value, parameters passed like *e* 
- syntax: 
	- `import defaultExport from "./module-name.js"` defaultExport must be a real js identifier 
	- import only belongs at the top, not in functions or anywhere else. 
	- there are four kinds of import declarations
		- namespace import - give it a name and like objects, refer to the name and call methods from it. 
		- non default import - you can import them but will need curly braces and call them exactly as they were exported as and seperated by comma. you can name it whatever you want is you use an 'as' next to the import statement once you've mentioned the actual name you exported it as. 
		- default import - you can give identifier any name
		- sideeffect import- will not import any values but will run the code and import the side effects of the code running. used often for polyfills, whatever that is. 
		- Hoisting - something about the import delarations being put at the top and run before something else. not too sure. 
		- see more on all four and syntax here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
**Export**
- there are two forms of exporting, named export and default export
	- default export - allows for any expression , can rename the use name on import because its a default export. you can only have one default export per file exported.
	- Named export - export out listed functions, variables declared elsewhere. useful when needding to export several values. , when imported, they need to be refferd by the exact same names as they were exported. (can rename to whatever with `as`) 
- see more on exporting here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
#### Webpack and loaders and plugins
Working with webpack generally involves three things to bundle your assets well: 
	1. adding files to directory
	2. import files to js file
	3. update input/output files in wepackconfig & loaders as needed
- to see more of handling .toml, .yaml, .json5 with webpack modules: https://webpack.js.org/guides/asset-management/
- 
Output management - what does the HTMLWebpackPlugin do?
	- as projects ge more complicated, the names of the entry points tothe webpackconfig file could change or even add new ones, the index.html file will still reference the old ones even after you change the config file. the bundles output will reflect the change but the html file will not. 
		- so this allows you to automatically link to the entry point names and creates new index.html files and will overwrite the one that you have even if its already there. and it will automatically bundle all your assets. 
- cleaning the /dist folder: 
	- after a while the dist folder will get cluttered, `clean: true,` under the output in the webpackconfig will know what outputs you're actually using and clean up the files that you are not using. 
Source maps, what are they and what are they good for?
- when youstart bundling different scripts, bugs will throw erros for the entire bundle as opposed to the spefic script that is giving issues. source maps fix that. 
	- in the webpack.config file: `devtool: 'inline-source-map', ` this goes under module.exports and right above the plugins (though not too sure if the order really matters. ) *note: it has been said that this is not recommended for production environemnts and only for the development environment.* 
- What is watch mode?
	- it becomes tedious to run `npm run build` everytime that yo make a change so this watches for changes and compiles for you
		- `"watch": "webpack --watch",` this goes in the package.json under scripts. under test.
- What is webpack-dev-server?
	- a rudimentary webserver that gives us the ability to use live reloading
		- because there important considerations to be made when there are more than one entry point refer to the actual link for how to on this for necessary optimizations: https://webpack.js.org/guides/development/
##### how to get up and running with npm and webpack?
- you will need to make sure the following are installed first: 
	- npm : https://www.theodinproject.com/lessons/foundations-installing-node-js
	- make the directory where the project will be
	- use `npm init -y` to initialize the npm packages
	 - make sure to add a `.gitignore` file and add this: `/node_modules` lest you want to look like a fool uploading your packages to your repo
		 - if you do accidentally, make the file and then run this in your cli : `git rm -r --cached node_modules`
		 - then `git add ./ && git commit ".gitignore"` and finally `git push origin main`
 	- use `npm install webpack webpack-cli --save-dev` to install necessary standard webpack modules
- create a webpack.config.js file to handle custom configs
	- copy this to make sure your webpack.config looks like this:
```javascript
const path = require('path');

module.exports = {
	mode: 'development',
	entry: './src/index.js',
	devtool: 'inline-source-map',
	devServer: {
		static: './dist',
	},
	output: {
		filename: 'main.js',
		path: path.resolve(__dirname, 'dist'),
	},
}
```
 -  open up the package.json and make sure it looks like this: 
```json
{
  "name": "weather-app",
  "version": "1.0.0",
  "description": "Demonstration of async and await api fetching with front end concepts applied",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "watch": "webpack --watch",
    "start": "webpack serve --open",
    "build": "webpack"
  },
  "author": "Charles Villalpando",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^4.15.1"
  }
}
```
 - set up live server:
	 - run `npm install --save-dev webpack-dev-server` 
- betweeen the configs in the package.json and the webpack.config.js and running the install for the web server, you'll be set to running in a node js environment. 
- the next essential packages involve getting eslint set up in your project and prettier: 
	- es lint: 
		- run: `npm install --save-dev eslint eslint-config-airbnb`
		- then `npx eslint --init`, check through necessary prompts select airbnb
		- eslint on vs code should already be installed
	- prettier: 
		- run: `npm install --save-dev --save-exact prettier`
		- then: `node --eval "fs.writeFileSync('.prettierrc','{}\n')"`
		- create a .prettierignore and include files that it should ignore
		- run this to make it compatible with eslint: `npm install --save-dev eslint-config-prettier`
		- then in the eslintrc.json: make sure it has this line below the "extends: [ "airbnb"]" `"prettier"` with no comma after if its the last extends you have.

##### extra webpack features: 

 - bundling more than one JS script together: 
 - bundling your css: 
		- place your style.css in your /src folder
		- use `npm install --save-dev style-loader css-loader`
		- add the module to the webpack.config.js:see below code snippet
		- make sure to import the style.css file into the index.js file or wherever all the modules are being loaded to
```javascript
module: {
+    rules: [
+      {
+        test: /\.css$/i,
+        use: ['style-loader', 'css-loader'],
+      },
+    ],
+  },
 };
```

- bundling your images: 
	- after placing your image in directory, import to the index.js file. you can attach it to the dom using js.
	- add the module loader in the webpack.config.js: 
```javascript

{
+        test: /\.(png|svg|jpg|jpeg|gif)$/i,
+        type: 'asset/resource',
+      },
```
- 
- 
- how to view page on live server through npm 
	- when compiling, if a webpack.config.js is present, the `webpack` command will pick it by default
 - Publishing your webpack page to github: 
	 - see the link for reference: 
		 - first publish the page the same way you normally would and then run this command: 
			- `git subtree push --prefix dist origin gh-pages`
			- then in your repo, change the branch to gh-pages
			- make sure you ran npm run build before you publish!
#### how to create your own NPM package to import to your project later
1. start with creating the github repository and cloning it locally to your project folder
2.  run `npm init --scope=@charlesvill` to scope your packages (so you can avoid naming collisions)
3.  make sure you're logged in to your npm account and run `npm publish --access public` 
4. good to go, you can install your package with `npm install @charlesvill/package-name`
### Principles of Object Oriented Programming
#### Single responsibility Principle
- states that a class, module, object should only fulfill a single responsibility. doesnt mean that it can only do one thing. but al lthe things it does must be for that single responsibility
	- for example: 
		- in a text based game, you should separate the part that manipulates the dom with the application logic that listens to when the game is over. so you should creat a module to handle all of the DOM magic
		- it is fine if it calls other functionality, but it should not be written in there. 
- Another way to think about it: if changing one aspect of a method/class/component affects another, you might have too many responsibilities on that component
- the single responsibilty principle is the first of 5 principles of OOP called the SOLID principles
- this is good article summarizing the problem: https://duncan-mcardle.medium.com/solid-principle-1-single-responsibility-javascript-5d9ce2c6f4a5
	- the TLDR: with example of error logging on a car class object, when you implement the error logs specific to that object, when refactoring, you have to go to every class object and refactor the way that individual object handles it. 
		- the good way is to have error logs handed by an outside object that your object calls the method on. this way, if you need to refactor how you handle error logs, you only have to refactor the error log class. 

#### SOLID principles
1. single responsibility
2. open-close
	- open to expansion but closed to modification
		- what this means is that the original constructors or classes should not be modified but should be open to expanding them to allow for other functionality by only expanding the current functionality without changing the original code and over complicating it
		- in practice this could be something like a huge switch statement being broken up into smaller classes and where the switch statement was issued just handles passing through the questions from the question class type. see this video for more on this: https://youtu.be/-ptMtJAdj40?si=I2Xvt24AH3zyeHdx
1. liskov substitution
	- so if we have a class cat that inherits from class animal, then what is true for animal should be true for cat meaning there isnt a strong deviation from the ineriting classes. if there is, like with the rectangle inheriting from square example, maybe you need to change who it is inheriting from or use composition to get features that you need 
2. interface segregation
	- you should not inherit from parents that have methods that will not apply in the child instance. for example penguin class inheriting from the bird class that has a method for flying. you can instead use composition to give objects the methods they need and avoid giving to those that do not need it. 
3. dependency inversion
	- should abstract away lower level functtionality when looking at a higher level method. for example higher level method of processing payment, if successful do this, else, do that. this should not include the writing of how the payment is actually processed, this should be abstracted away in a seperate class so if you need to change who does payments, you can focus on the class instead of the higher leven functions that depend on the lower level stuff. it may look like more code, but it means better written code that will save you time refactoring down theline. 
#### what are tightly coupled objects?
- they are components that are not necessarily related directly but when changing one thing, you have to refactor the other. good example is with a game where you want to change all the UI but doing so affects the game logic in some way. This should not be the case. should be able to touch UI without it affecting the game logic
#### few notes on performance 
- the various DOM selector methods: queryselector and getElementbyID
	- getElementbyID has access to cached DOM elements while the other does not. this suggests that searching for deeply nested elements could take longer on query selector
	- depending on the use case, could be better to use get element by ID though that is really in cases where deeply nested and it is searching many many times. over all, it's not a huge performance hit. 
#### working with dates in javascript
working with dates in javascript can be a bitch, particularly when working with the new Date() class methods. 
- when passing through a date to new Date() you have to pass it as a string! make sure even if you're passing it a variable that is a string already, you are still using the backticks so that they are actually being passed as a string. 
- further, the format is expected to come in the form of : 'YYYY-MM-DD' though I've tested with less issues when the traditional 'DD-MM-YYYY'. 
	- *note: though the latter of formats works better, input forms with calendar inputs pass back the value in the former format, which sometimes comes with its issues depending on which timezone you're in*
	- I've found that including `const inputDate = new Date(`${date}T00:00`);` the T00:00 actually helps in actually capturing the correct date when passing the date as a string. see the tasks project for more context
- You can use the library date-fns to import lots of useful functions like `format` and `differenceInCalendarDays` 
	- *note: the hours are taken into consideration when looking at difference in days unless you purposely omit the days like so: * 
```javascript
const inputDate = new Date(`${date}T00:00`);

const inputDateNoTime = new Date(

inputDate.getFullYear(),

inputDate.getMonth(),

inputDate.getDate()

)
```
- notice here the date constructor is making the date object from the initial string with the local timezone adjustment and then making a new date object that omits the hours by getting the only the year , month and day of the former object. then you would pass this noTime object wherever you need things having to do with differences in days that don't have a regard or necessity to consider hour precision. 
	- *note: after some testing, I found that as long as the local timezone adjustment was made above, I did not have to use the no time changes here. however, I'll leave it here incase I have issues in the future with something related.*

#### Storing data in JS: Local Storage vs Session Storage vs Cookies

With data that is meant to persist after exiting the window, there are a few similarities between all of them. 
	- they all store on the browser 
	- for local and cookies it is meant only for a single user and no other user of that website has access to that data. 
- clicking on the application tab on chrome dev tools allows you to see the local storage, session storage and the cookies that are being used
- local and session storage are using the Web Storage API
##### cookies: 
 - much smaller than local and session storage
	 - only 4kb
	 - older compatibility on html5
	 - the cookies available on all tabs on the browser
	 - you have to set when they expire
	 - not just stored on your browser, they get also get sent to the server with http requests, 
		 - make sure to make the cookies as small as possible
	- almost always want to use local or session storage, cookies is only really if you really need to send the information to the server. 
##### session storage
- exists only on that one session and tab, not avaible in another tab
- expires on the end of the browsing session, closing the tab
##### Local Storage
- exists until you manually delete it. 
- to acess local storage, you use the variable `localStorage.`
	- storing: `localStorage.setItem('keyString', 'valueString');`
	- removing: `localStorage.removeItem('keyString');`
	- retrieving: `console.log(sessionStorage.getItem('keyString'));`
- storing Objects: 
	- because the set method needs to be a string, trying to pass an object as a value will not give the desired results if it's not converted into a string. 

### Linting
style is very important to keeping code maintainable and easy to read
- very useful style guide for airbnb & Javascript: https://github.com/airbnb/javascript
	- refer to this throughout to answer questions on styling
		##### styling for objects  see 3.1 in air bnb doc
		- when using dynamic names, make sure to use computed property names that are not defined elsewhere outside of the object
		- use property value shorthand: `obj = { skywalker, }` when skywalker is a variable already declared. don't give it a property name and then the value as the variable. just the value variable
		- whats the better way to shallow copy objects?
			- use the spread operator to make a copy `const copy = { ...original, c: 3};` 
				- this makes a copy of the original and adds the key c with prop 3
		##### Styling for Arrays
		- use the literal syntax for array creation because the array constructor only allows one argument and because Array global could be affected. *whatever that means lmao*
		- look at 5.1 on destructuring objects for best practices
		##### best practices for Functions see 7.1
		- should never mutate the function arguments that are passed through see 7.12
		- always put default parameters last and avoid mutations to default parameters that are invoked on the function call
		- proper spacing for function declarations: `const x = function () {};` or 
			- `const y = function a() {};` 
		##### variables
		- should not use 'var' only const and let
		- group your let and const variables 
##### Linting & Formatting program
- use eslint, the most popular of them, follow these directions: https://eslint.org/docs/latest/use/getting-started#quick-start 
	- you can run `npx eslinter filename.js`
	- install the vscode plugin on vscode and change the plugins found here to allow changes to happen when you save
	- change settings in the eslint.rc to the rule set so that it allows console.logs
- use Prettier for formatting to apply intelligent indentations and making your code more consistent to look at. 
	- use this instructions to get started: https://prettier.io/docs/en/install
	- will also need to install plugin for vscode to auto format code on a save or key press
- Make sure to install the patch to allow prettier and es-lint to work in tandem: https://github.com/prettier/eslint-config-prettier#installation
- why to use linting and prettier
	- linting catches simple mistakes such as inconsistencies in variable declarations (let/const vs var), semi colons and other things that are not obvious but might break with some minification software.
##### Dynamic User interfaces
- on making Drop-down menus: 
	- see the guide on making a drop down menu or install npm package or look in the ghub repo
	- *notice that it does not use display: none to rid of the dropdown because it's not animatable*
		- instead you can use the opacity and opaque as does github on their own page
- making your own packages to publish on npm and pull them later for use!
	- inside a folder that has a self contained tool or piece that can be reused, like a stylesheet and script for generating drop-down-menus, npm init (not y)
	- specify the name with local scoping `@charlesvill/packageName`
	- adding the repo is optional
 - after initializing npm go in the package.json and add "type": "module" like this:
	 - `"main": "index.js",`
	 - `"type": "module",`
	 - this is to make sure you can import your package as a module *this needs to be set on the repo youre importing to as well*
		 - if you happen to forget this step and need to update for any reason your package: 
			 - make the changes, git add and commit and push
			 - run npm link again
			 - then run this: `npm version patch` and it will update the package locally and then: 
			 - `npm publish` to update your package online
	- after the self contained script is done (using module exports as applicable) run `npm link` to add the package to a local repo to be cloned locally for testing. 
		-*note: if you're going to export as module either note in the package.json that it's {type: "module"} or type="module" in the script tag*
		then create another folder named test and make a script that imports your package
		- run `npm link package-name` to download the package in the local folder
		- after testing, head to the package directory and make sure you're logged into npm 
		- then you can run npm publish --access=public 
		- then you should be good to go!
### Client side form validation
- before sending off data from forms to the backedn databases, it's important to validate the information as correct using client side validation. while it has been covered in html in [[Intermediate CSS#Form Validation]] (this should really belong in a html notes not css but here we are)
- review of some of the psuedo states that are true of elements 
	- valid `:valid` css selector for styling or presentig certain feedback
	- invalid `:invalid` same as above
	- out of range `:out-of-range` specific for certain form elements as appropriate
##### error messages that can be displayed: 
[`badInput`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/badInput "badInput"), [`patternMismatch`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/patternMismatch "patternMismatch"), [`rangeOverflow`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/rangeOverflow "rangeOverflow") or [`rangeUnderflow`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/rangeUnderflow "rangeUnderflow"), [`stepMismatch`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/stepMismatch "stepMismatch"), [`tooLong`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/tooLong "tooLong") or [`tooShort`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/tooShort "tooShort"), [`typeMismatch`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/typeMismatch "typeMismatch"), [`valueMissing`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/valueMissing "valueMissing"), or a `customError`.

- regular expressions are used for patterns and they're their own skill. see this article: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions see[[#regular expressions]]
	- invaluable site to test out regexpr : https://regexr.com/
#### The Constraint Validation API
contains many useful properties and methods to use such as: 
	- `element.validity.typeMismatch` will return a true if say an element is not conforming to the format expected
	- `element.setCustomValidity("I am expecting an email address!"` self explanatory
	- on the forms you can also stop the automatic html validation if you want full control using javascript (does not disable any CValidation API or css psuedo selectors as a result)
		 `<form novalidate></form>`
- you can also nest a span with the tag `aria-live="polite"` to control where the error gets seen if wanted in DOM
- see the constraint validation api documentation for examples and regExp implementation  example, file size limiter example : https://developer.mozilla.org/en-US/docs/Web/HTML/Constraint_validation
- here is another more concise version from w3 schools: https://www.w3schools.com/js/js_validation_api.asp
Example of implementation: 
```javascript
const email = document.getElementById("mail");

email.addEventListener("input", ()=> {
	if(email.validity.valueMissing){
		showErrorMessage();
	}
})
```
- for the next few examples, they will all involve turning off the validation build into html to allow the script to have full control of the validation. 
##### email validation
- right off the bat reg exp is not needed if using the contraint validation api. 
- make sure the the input is of type email and that the min len is 8 and it's required
- for the script you will need: 
	- refernce to the input field, form & the custom error field if applicable
	- event handler for input:
		- `if(email.validity.valid)` -> else `showError()`\
	- event handler for submit: 
		- deny submission if not valid:: `(!email.validity.valid)` -> `showError()` `event.preventDefault()`
	- function to display error message: 
		- checks for three things: value missing, type mismatch, too short
			- `(email.validityvalueMissing)`
			- `(email.validity.typeMismatch)`
			- `(email.validity.tooShort)` 
##### zip validation
##### country validation (text)
##### pwd validation

#### regular expressions
see this video on quick start and overview: https://www.youtube.com/watch?v=rhzKDrUiJVk&ab_channel=WebDevSimplified 
here are the reference documentation for them: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions
some of the bigger reg expression patterns: 
	
#### What is ES6? 
- alot of features being used like const, let, modules, for of loops were introduced in the ES6 which is short for ECMA script which was standardized in 2016
- a potential problem with javascript updating is that browsers take a while to update to support these new features. 
	- *solution?* Babel transpiles code into code that older browsers can use. it can easily be added to the webpack configuration to integrate it with workflow
		- follow the guide here to integrate it to your current webpack workflow: https://github.com/babel/babel-loader
		- nice article on basics of how babel works and the importance of plugins: https://blog.jakoblind.no/babel-preset-env/
	- on its own babel does nothing until you install the packages that handle the specific ES6 features that need to be transpiled. 
		- while you could sit there and manually install each feature you used, its easier to use a preset: a collection of plugins that work all at once. ex: `@babel/preset-env` they even have ones for airbnb
#### JSON
- article on it: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON 
- short for Javascript Object Notation its universal for transmitting data across the web
	- when you convert a json  string to a native javascript object is called deserialization and the opposite is called serialization. 
		- also use the term 'parsing' when referring to the deserialization
	- often seen with MIME type which is metadata, eseentially a string with information about the media file
- json can exist in its own file `.json` that is essentially just a text file with the json strings in it
	- Json needs to have double quotes for the properties single quotes only allowed surrounding the entire json string
	- json can have only properties, no methods
- Json can be validated to ensure good working and that a stray comma or other error wont throw off the whole string with JSONLint: https://jsonlint.com/
- this website allows you to paste in json and checks for errors: https://jsonformatter.curiousconcept.com/
- Only quoted strings can be used for the properties

#### Asynchronous Code 
- asynchronous code is the ability of javascript to hand off the execution of something that does not happen instantaneously like server requests. you send off and execute the rest of your synchronous code and then once the async function is done you can have things trigger after its complete
- aysnc boils down to three different kinds in js: callbacks, promises, and async/await
- What is a callback?
	- callback is a function that has another function as one of its parameters. the effect is that the function is asynchronous. meaning that the call for the asynchronous function will begin but the other functions will continue get called as the async function continues to run 
	- this is typically done for node that uses mostly async functions and for server requests and other things that have to do with file system. this is because those operations especialy server requests and retrieving things from the file system takes alot longer than the cpu could process other tasks stored in memory (RAM)
	- what does a callback function look like?
```javascript
var fs = require('fs')
var myNumber = undefined

function addOne(callback) {
  fs.readFile('number.txt', function doneReading(err, fileContents) {
    myNumber = parseInt(fileContents)
    myNumber++
    callback()
  })
}

function logMyNumber() {
  console.log(myNumber)
}

addOne(logMyNumber)
```
	- notice here that the function to log the mynumber is passed through the function call for addOne which has the asynchronous function of reading the file. now the console.log function will get called at the end of addOne as the callback function
- if you try to call synchronous calls right after an asynchronous call back() you'll see the output of that synced function befor the asynchronous calls 
- What is a promise?
	- promise is a newer way to tackle asynchronous functions you promise to do something and has one of two possibilities: 
	- *if ever need help on promises read this* : https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch3.md
			- specifically chapter 2 and 3 or even more cruise the headings for what you need help with
		- it will either get resolved, or rejected
		- you use functions then and catch to handle either the resolved or rejection of the promise
		- `asyncfunc.then()` where you can run a callback after the promise has been resolved aka if its finished getting what it needs to
		- `asyncfunc.catch()` this is run if the promise is rejected because of a time out or because a status code for a server is no bueno
		- `asynfunc.finally()` gets triggered regardlesss of whether the promise is fulfiled or reected
		- Promise.all method takes an array of promises and fires one callback once they have all been resolved
		- Promise.race() will fire as soon as any promise in the array has been resolved
```javascript
const promise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const condition = true; // Replace with your condition

    if (condition) {
      resolve('Success!');
    } else {
      reject('Failure!');
    }
  }, 2000);
});

promise
  .then((value) => {
    console.log(value); // Will print "Success!" if condition is true
  })
  .catch((error) => {
    console.error(error); // Will print "Failure!" if condition is false
  });

```
 - look here at the anatomy of the promise constructor: 
	 - the arguments 'resolve' and 'reject' are passed to the constructor and handle passing the values of either the success of the promise or the failure
		 - resolve("success") - passing through string 'success' for the resolving which gets passed to the .then() as the value variable passed through the .then(value) that is why you see console.log(value) === 'success'
		 - same with the 'reject' it will take the argument you passthrough it and pass it as argument for the catch in this case initialized as 'error' and can print out the contents of the error message that you printed out. 
```javascript
(new Promise((resolve, reject) => { reject("Nope"); }))
    .then(() => { console.log("success") })
    .catch(() => { console.log("fail") })
    .finally(res => { console.log("finally") });
```
	-note here the sequence of promise methods and notice the new Promise syntax 
- conceptually what is a promise?
- additional notes on promises: 
	- if you pass a non-promise to a Promise.resolve() you get a promise back that resolves to the value that was passed through. I think what this means is that it will simply complete the then function with the first accepted parameter and pass the value as that parameters parameter. lol confusing stuff. 
	- if you pass a promise to a Promise.resolve() you'll just get that promise back. literally will be the equality === property to them
	- resolve is often used to mean success most of the time but the name suggests resolve could be resolution as either failing or passing. this name is accurate because a then statement while of the resolve, can find a reject pattern in its own scope and thus could return with a reject, so it really can be either a pass or a fail, but mostly its used for a pass. 
```javascript
function fulfilled(msg) {
	console.log( msg );
}

function rejected(err) {
	console.error( err );
}

p.then(
	fulfilled,
	rejected
);
```
- note here that its named fullfilled and rejected unambigously because the first parameter for then will be always the pass unlike the resolve of the original promise parameter. 
- what is a thenable and what relation does it have to promises?
	- in essence, thenable is a function that behaves like a promise but perhaps is not a promise type perse maybe because it doesnt actually support promises such as older code bases or browsers that do not support es6
	- allegedly you can defer the error message of a rejected with the method .defer()
- how does chain flow in promises?
	- you can chain .then() statements on a promise and each time it is done, it will return a new promise and with each new promise, you can then chain another .then() statement and so on and so forth if you pass a promise.resolve() with a non promise value, this value will get passed down to the last instance of a thenfor example: 
```javascript
var p = Promise.resolve( 21 );

var p2 = p.then( function(v){
	console.log( v );	// 21

	// fulfill `p2` with value `42`
	return v * 2;
} );

// chain off `p2`
p2.then( function(v){
	console.log( v );	// 42
} );
```
	- notice here the the Promise.resolve(21) and how at the end 21 gets passed along and mutated but still passed to p2.then()'s callback function
	- you also do not have to name them something different like p2 or p3 you can just call .then() as many times as you want and its essentially the same thing 
	- also to note, the second step there return statements automatically resolve the promise. 
- What is the event loop? and what does it have to do with asynchronous functions / methods?
	- event loop is what takes an asynchronous function that has been put off, and puts it back onto the call  stack once the async func has completed and has been put in the task queue and waiting to be added to the call stack
- what does it mean when you say that javascript is single threaded and that it can only do one task at a time when it can load stuff and files in the background?
	- in reality, js is trully single threaded so it can only do one task at a time. what happens is that the runtime for javascript either the v8 chrome engine or the magic node js c++ shit that's happening will give js only one thread. 
	- when there is a task that needs to be async, it will be pushed off the runtime into other apis in the browser or other node magic stuff like c++ that has access to those extra threads so it can handle the loading of stuff while js can run the rest of the cod and hen when that background stuff is done, it gets slapped back into the runtime by the event loop and the single thread is back to business. 
- what is a `setTimeout()` function and what is it used for ? 
	- it is an asynchronous function that will delay the execution of that code for the time set in the argument 
	- what does this function have to do with the event loop and async functions? 
		- well sometimes people say to put some the time out time to 0 which would not make sense except that because of the event loop, even with time of 0, it effectively just waits until the stack is clear and then it will trigger that callback in the setTimeout()
- What is callback hell? 
	- when you have functions passed as parameters as a part of async functions it is difficult to trace the execution order of functions when they are laid out sequentially but do not fire sequentially. Many think whats difficult abot it is how they often are deeply nested, but what is the problem is how when following execution order, you often have to glance and bounce around all over the code base to follow it. 
- reference for callback hell and workarounds: https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch2.md *dont really understand some of the things he's saying like how he makes the asyncify function or the timeoutify function* come back to this... 
- In what cases would promises better than a call back?
	- sometimes your callbacks might do the following that a promise would fix: 
		- call back too early, late, or never
		- too few or too many times
		- fail to pass necessary parameters, or swallow any errors that may happen
- what does the `.then()` function do?



#### Working with APIs
- what is an api?
- how does access to an api work?
- how do you fetch and extract data from an api?
```javascript
const response = fetch(`https://pokeapi.co/api/v2/pokemon/${queryString}/`, {mode: 'cors'})
	.then((rsp) => {
	if (!rsp.ok) {

throw new Error(`Search was not found, please try again. Status: ${rsp.status}`);

}

return rsp.json();

})

.then((data) => console.dir(data))
.catch((error) => console.error(`Search was not found, please try again, ${error}`))
```
notice here the the fetch request that is checked for the status inside the first '.then()' and then if it is not okay, you throw a new error and it will be pushed to the catch. 
- explain how an api request could be blocked by the browser and how to fix this?

#### Async and Await 
basically a way of handling async events that are expressed more linearly and easier to read compared to promises and then() and catch() blocks : good article to brush up on async/ await: https://javascript.info/async-await
- what is an async ?
	- it is syntactical sugar for promises. when you declare a async function, it returns a promise
- how do you declare an async functoin
	- write async infront of it
- what does the async keyword do exactly
	- wraps your function in a promise that will return a promise that looks to be resolved 
- what does the await keyword do
	- defers the execution of the next line in the async block until the await expression is done
- what does the async *function* return?
	- a promise
- what happnes when an error is thrown inside an async fuction
	- you can either nest a try .. catch blocks inside the async to catch it or you can also chain a .catch() to the await expression.
- how cna you handle errors inside an async function?
```javascript
	async function f() {
		try {
			let response = await fetch(url);
			let user = await response.json();
		} catch(err) {
			alert(err);
		}
	}
f();
```
	- note here how the await fetching wrapped in a try.. catch block that will on failure, send the alert to the catch block for either the user or the response awaits. 
- good video on await and aysnc for demonstrations and eror handling : https://www.youtube.com/watch?v=9YkUCxvaLEk&ab_channel=dotconferences also talks about error with using express ******* 

### A bit of Computer Science
valuable course on algorithms: https://www.coursera.org/specializations/algorithms from stanford!!
#### Recursion
- when is recursion best used for?
	- to iterate over an object with departments that need to sum all the salaries. 
	- using for loops would be tedious and possibly error prone, try this: 
![[Pasted image 20231031154410.png]]
	- here we can see the object company has some complicated nested arrays and the sort and the recursive function here will apply a check for if array or if its just key value pairs
	- notice that the recursive call is focues on traversing deeping into the recursion depth to find the base case
	- source: https://javascript.info/recursion
- Another take after a couple days working with recursion: 
	- one of the main themes of recursion is 'divide and conquer' wherein you have a problem either a data set or some complexity built into the function that needs to be simplified. ex: splitting array to a single element
	- by dividing and conquering via recurison you are essentially creating branches with each call added to the stack that descends furhter until you've reached the single indivisible element to work with. then
	- as you reach the base case, it 'unravels' itself  up the stack chain. typically the recursive call will be assigned to a variable or a return value where the evaluation of that expression will be used for something as it continues to unravel itself
	- ex: 
```javascript
function mergeSort(arr) {
  const len = arr.length;
  if (len < 2) {
    return arr;
  }
  const mIndex = Math.floor(arr.length / 2);
  const lArr = mergeSort(arr.slice(0, mIndex));
  const rArr = mergeSort(arr.slice(mIndex));
  let mArr = [];

  while (lArr.length > 0 && rArr.length > 0) {
    if (lArr[0] < rArr[0]) {
      mArr.push(lArr[0]);
      lArr.shift();
    } else {
      mArr.push(rArr[0]);
      rArr.shift();
    }
  }
  return lArr.length > 0 ? [...mArr, ...lArr] : [...mArr, ...rArr];

}

console.log(mergeSort([7,2, 1, 5, 3, 0]));
```
- notice here the important compenent in merge sort is sorting one half and merging. we find what each half is by setting the half variable equal to the recursive call that will descend and divide the array completely till its only one. and the many branches it creates will all unwind and return pieces of array that will continue to the steps of merging which then returns the merged piece of array to the higher level. very much looks like branches
- more on merge sort see [[C#Recursion]]
#### Time Complexity
also seen in cs50[[C#Algorithms]]
review: 
- theta time is the average between the upper bound and the lower bound 
- big O notation - the upper bound or the worst case scenario
- omega notation - the best case scenario
- in big O notation, the order from fastest to slowest:
	- - O(1) - Constant Complexity
	- O(log N) - Logarithmic Complexity
	- O(N) - Linear Complexity
	- O(N log N) - N x log N Complexity
	- O(n²) - Quadratic Complexity
	- O(n³) - Cubic Complexity
	- O(2ⁿ) - Exponential Complexity
	- O(N!) - Factorial Complexity
- most important thing for determining the big O time is considering how the speed of the algorithm changes as the data set will change. so if the steps are the same for a data set of 5 as the set of 5000 thats constant time of O(1) which means its fixed 
- O(log N) means that for each doubling of the data set, it will gain one other step
	- exmaples include binary search, with data set of 1, 1 step. 2, 2 steps. 4, 3 steps. 8, 4steps, 16, 5 steps etc. 
- O(n) linear time- means that the steps will grow proportionally with the number of elements in the data set
	- example is iterating through the whole array
- O(n log n) - behaves like log n but an added algorithim of O(n)
	- example of this is merge sort bc its log n for dividing array recursively but then it needs to merge by touching each element in the array at some point. 
- O(n2) quadratic time - for each item you need n times steps
	- when you put a loop inside of a loop essentially for each item you need to do the n steps n x n
- O(n3) - you get it at this point
- O(2n) really slow, i think you gotta try really hard to be this slow
##### space and time complexity with build in js methods
-time complexity - the runtime of the algorithm as the data set grows 
- `arr.push()` and `arr.pop()` both constant time bc just adding element at the end and a single index. does not take longer given a larger data set
- `arr.unshift()` however is linear time bc it needs to iterate through each element and reindex it
##### logarithmic 
simple example of logs: 
	Log(16) = x 
		`logarithm is the x, which is the power the base, 2, needs to be raised to get to the number (16)`
		- in this case, 4 bc 2x2x2x2. 
- O(log n)
	- when looking at algorithms the O(log n) you have to double the input size in order to get the steps to increase by 1. very fast
	- examples of O(log n ) time are balanced binary trees and binary search of sorted lists
- linearithmic - O (n log n)
	- behaves linearly but nested in it has a logarithmic iteration that only adds a step per doubling datasets
- Factorial time O(n!)
	- example is the traveling salesman problem that checks all possible cities and routes and returns the distance shortes, bruteforce method
big cheat sheet on time complexity: https://www.bigocheatsheet.com/

##### finding big O of your functions
![[Pasted image 20231107101642.png]]
more on how to determine the time complexity of the function: https://www.sahinarslan.tech/posts/step-by-step-big-o-complexity-analysis-guide-using-javascript
#### space complexity
- similar to how time complexity is determined but have to consider to what extent variables are being reproduced for your code. for example, are you reproducing something for each input? as many are, most are space complexity of about O(n)
- What is memoization?
	- is an optimization technique where you would cache the results of an expensive function calls to a pure function #NeedMoreHelp and then returns the cached result when it is needed again.
	- sometimes this code though saving memory could be difficult to read and its benefits have to be measured against the drawbacks of readability
- How is space comlexity defined?
	- space complexity is total space taken with respect to the input size. 
	- includes the auxiliary space and the space used by input
- what is Auxiliary space?
	- extra or temporary space used by the algorithm
		- ignores the input size but accounts for program calls inside of the functio

#### Common Data structures and algorithms
- the choice of what data structure to use depends on the speed of loading data and accessing it and what is the most important for your project
- questions to consider: 
	- what is breadth first search and depth first search and when should you use one over the other?
	- what are the best ways to implement stacks and queues in Js?
- making a binary search tree from an unordered list:
	- in the order of the elements in the array you add nodes as either being greater than or less than the root element and you'll have to descend greater depths and continue this process of repeatedly finding where the next element in the array wouuld fit as it traverses through the current tree formation
- depth first vs breadth first with binary search trees
	- breadth first: 
		- refers to traversal through the nodes in the tree, you would first visit each node associated with a depth level before you descendd another level
		- something would need to keep memory of the previous levels other branch so that it could go up and descend to the level analyzing but on the righ side to continue seeing all of them
	- depth first: 
		- video showing this in practice: https://www.youtube.co/m/watch?v=gm8DUJJhmY4&ab_channel=mycodeschool
		- there is three kinds: preorder, inorder, post order
		- preorder refers to descending recursively the left most branches all the way down and each level down reading the value before descending another level
		- inorder descends a branch and reads the nodes value once it finishes left branch
		- post order descends a branch and reads both the descending left and right branches and then reads the data right before it asends back up
- Level Order / breadth first traversal: 
	- excellent video explaining: for c++: https://www.youtube.com/watch?v=86g8jAQug04&ab_channel=mycodeschool 
	- using the queue method:
		- on the root node adds the current node on the stack to be read
		- reads the first node in the stack which is the current node
		- it registers the children addresses
		- adds them to the queue`
		- moves to the child node that is first added to the stack
		- repeats
	  - queue method means that in effect the sequence of repeated steps here will read the node values in each level before reading the next one
##### Making a balanced binary search tree
- starts with having a sorted array. use either your own merge sort algorithm or use the build in array.sort() which allegedly uses a hybrid of merge sort so O(n log n). 
- Takes the middle of the sorted array and then it makes it the root of the tree and places each half of the already divided array as children of the root and proceeds doing that until there are no elements left to place. 
	- will do this recursively.
##### vocabulary for graphs
- edge - the line connecting two vertices or nodes
- vertex - a node or piece of data
- undirected graph - where the edge necesities a biconditional relationship with both the nodes connected to it. 
- incident - is the relationship of two nodes connected by an undirected edge, also known as adjacent or neighbors
- degree of a vertex - is the number of edges that are incident on a vertex
- edge weight - is a number put on the edge between two vertices that could forexample show the distance between those two vertices or how close each of the two vertices are as friends
- weighted graph- graph whose edges have weight. like google maps and other navigation. cities are nodes and the roads are the edges and the weights are the distances between the vertices and the navigatoin finds the minimal sum of edge weights over all paths to get to the destination. shortest path.
- notes on graph theory from p guide to cs: 
	- what is asymptotic notation? - its just big O notation
	- what is an edge list? for a graph, you list out all pairs of nodes that have edges
	- what is an adjacency list? for a graph, you list out all the nodes that are essentially children of a given node https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/e/quiz--representing-graphs











### Testing Javascript 
#### Testing Basics
- what are the supposed benefits of Test driven development?
  	- keeps you out of the debugger
  	- improves design of code
  	- speeds up development by eliminating waste
  	- reduces bugs in new features and in existing features
 
  - the process is that you develop a test right before having code that is testable. you design the test before you actually code the project. perhaps a way of fleshing out the ideas of what your program is supposed to accomplish. like a way of thinking backwards about your program or expaining it to some one else how its supposed to work 










