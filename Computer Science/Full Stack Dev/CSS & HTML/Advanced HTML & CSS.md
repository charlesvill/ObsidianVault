
## Animation

### Transforms
- almost all elements can have the `transform` property applied to it except for `<col>` and `<colgroup>` and those elements that are non-replaced inline elements
	- examples include `<span>` `<b>` `<em>` whose main content is contained within the html
	- extremely useful article on the application of transforms in projects: https://www.joshwcomeau.com/css/transforms/
	- if you want to make some cool diagonal transformations using trig look here: https://9elements.com/blog/create-diagonal-layouts-like-it-s-2020/
	- 
#### 2D transforms
transform functions include: 
- rotate - rotate element on a 2D plane
	- `transform: rotate(45deg);`
		- values: `45deg` `-1rad` `0.3turn`
- scale - grow or shrink 
	- `transform: scaleX()` or `scaleY()` or `scale()`
		- values: `scale(.25)` or `scale(.25, 1.5)` x then y respectively
- skew - skews on a 2d plane
	- `transform: skew()` or also skew with either x or y
		- values: `45deg` `-0.5rad` 
		- skew() takes two values and only one acts same as skewX()
- translate - slides in a direction
	- `transform: translate()` also same with X and Y translate() takes two values for x and y axis
		- values: px and `-33%` percent of the elements width
##### Chanining transforms
```css 
.blue-box {
	transform: translate(20%) rotate(45deg)
}
```
- you can chain the transformations with separating space
- *note* the order of transformations applied matter because translating a shape and then applying a rotation will rotate from the origin point before the translation was applied, thus making like a "swing" effect. keep this in mind when trying achieve certain effects with transformations. 
#### 3D transforms
- `rotate`, `scale`, and `translate` functions are used in 3d transformations as well
	- however, in order to achieve a 3d effect, you need to use perspective property
```css
.element {
	transform: perspective();
}
```
- it tells to render as if it were viewed from a specific distance on the z-axis
- more on perspective with examples how to use it: https://css-tricks.com/how-css-perspective-works/
```css
.element {
  transform: rotateX();
  transform: rotateY();
  transform: rotateZ();
  transform: rotate3d();
}

```
- additional functions for 3d, these do not require the perspective()
- scale 3d - `transform: scaleZ(); and scale3d()` 
- translate 3d - `transform: translateZ and translate3d()`
- matrix - uncommon, dont really use it but it exists to combine all transform functions but poorly readable
#### Benefits of transform
- its cheaper to use than other css properties. see here to learn more about that here: https://developers.google.com/web/fundamentals/performance/rendering/#the_pixel_pipeline

### Transitions
- Allows to define properties that will change, how long it will take and the way it changes
```css
button {
	color: white;
	transition: background-color 1s ease-out 0.25s;
}
button:hover {
	background-color: black;
	cursor: pointer;
}
```
syntax: `transition-property, transition-duration, transition-timing-function, transition-delay`
