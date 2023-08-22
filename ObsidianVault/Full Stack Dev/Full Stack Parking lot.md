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
- [ ] 

