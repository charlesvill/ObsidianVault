- where questions come up and gradually get answers

- [x] Why use `span` to nest elements inside of it in contexts other than putting emphasis or bold. ex in context
	`<label><span><input type="checkbox"/></span>True</label>`
	lesson in context [[Intermediate CSS#Advanced Form styling]]
- [x]What is the purpose of using ::before and ::after psuedo classes to insert content like emojis? why couldnt it just be put as part of the content in the html tag?
	ex: 	
		Response: at times you could just want to avoid certain text or emojis to muddle the html content which would make it confusing for accessibility devices. Further, you can insert things that you might not be able to with html, such as gifs, icons, and other media. see notes in context [[Intermediate CSS#UI Psuedo-classes]]
	```css
.select-wrapper::after {
  content: "▼";
  font-size: 1rem;
  top: 3px;
  right: 10px;
  position: absolute;
}
```
- [ ] what is the difference between classes, factory functions, object literals, and modules and object constructors? why are there so many different kinds of templates to build objects? which one should I be using?
- [ ] what does a typical workflow look like when you would be taking advantage of the benefits of prototypal inheritance?
- [ ] what does it mean to be static? static initialization blocks: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
	  - it is setting a method or a field that is available by the class, but not by the individually instantiated objects from the class. 
	ex: 
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static displayName = "Point";
  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.displayName; // undefined
p1.distance; // undefined
p2.displayName; // undefined
p2.distance; // undefined

console.log(Point.displayName); // "Point"
console.log(Point.distance(p1, p2)); // 7.0710678118654755

```
  - notice the .displayName is not available on the p1 instatiated copies but it is on the Point.displayName actual reference to the class template. its useful for methods or info that doesnt need to be carried or accessed by the individual instantiations,. see this in context[[Intermediate Javascript#Classes]]
- [ ] what does it mean by public and private features? does it just mean creating enclosures within objects to emmulate private fields?[[Intermediate Javascript#field declarations]]
- [ ] conceptually what are bindings and what are important considerations of bindings that need to be taken when it comes to being a developer?
- [ ] why are there so many templates to create objects? object constructor, classes, factory functions, module pattern? why do we have so many and what are important considerations to take in deciding which ones to employ for your project? i
- [ ] is it good practice to avoid using global variables and declarations? things like const for event listeners and such. should they be wrapped up somewhere if at all possible? are there instances where you would want to avoid encapsulating constant variables and leave them isntead in the global scope?
- [ ] this shit found in chapter 3 of you dont know javascript under concurrent iterations dont make nonsense:
```javascript
**Note:** In this implementation of `map(..)`, you can't signal async rejection, but if a synchronous exception/error occurs inside of the mapping callback (`cb(..)`), the main `Promise.map(..)` returned promise would reject.

Let's illustrate using `map(..)` with a list of Promises (instead of simple values):
var p1 = Promise.resolve( 21 );
var p2 = Promise.resolve( 42 );
var p3 = Promise.reject( "Oops" );

// double values in list even if they're in
// Promises
Promise.map( [p1,p2,p3], function(pr,done){
	// make sure the item itself is a Promise
	Promise.resolve( pr )
	.then(
		// extract value as `v`
		function(v){
			// map fulfillment `v` to new value
			done( v * 2 );
		},
		// or, map to promise rejection message
		done
	);
} )
.then( function(vals){
	console.log( vals );	// [42,84,"Oops"]
} );

```
- [ ] next point here

