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