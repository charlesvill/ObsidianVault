
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
- for the transition property you have the option to use "all" meaning any css property that can be changed will be changed but that is not recommended as down the line with adjustments to the component or the styling might lead to some unexpected results
- on transition-timing-functions: this adjusts the speed of progression of the transition over time. it can be linear/proportional or it can be gradual either beginning or end
	- ease-out: fast then slow end- useful for objects entering
	- ease-in: slow then fast - useful for objects leaving the screen
	- ease-in-out: fast slow fast  - useful for looping animations
	- ease: fast slow fast but not symmetrical fast, more decceleration at the end - prob loop
- `transition-delay` can be really helpful when youre in one of those menus where you have to hover over the parent in order to select one of its children and god forbid you move the mouse diagonally to select an option and get out of the box of the parent and then the child subbox immediately closes. very frustrating. solution to this is to add a transition delay for like 300 ms
```css
.dropdown {

  opacity: 0;

  transition: opacity 400ms;

  transition-delay: 300ms;

}

.dropdown-wrapper:hover .dropdown {

  opacity: 1;

  transition: opacity 100ms;

  transition-delay: 0ms;

}
```
- notice here that he could have used the shorthand for the transition delay but this person recomends making it explict because the numbers can be a little ambiguous
##### stacking contexts: 
- similar to layers in photoshop affects the higher z index for rendering on top of other elements. 
	- when a stacking context is created, it affects how grouped elements are competing for being on top with respect to elements siblings with any parent element. 
- there are times when you might want to create a stacking context to allow children componets a higer rendering index for certain pieces of art or animations where elements grouped are meant to render over everything else
- other times, its worth considering for performance reasons to avoid stacking contexts as painting over all other elements are less performant and can be avoided especially if that's not necessary to your ends
- see here for more on contexts: https://www.joshwcomeau.com/css/stacking-contexts/
##### Performance
- on the general try to avoid transitions that affect layout such as chaning : top, right, etc when the positioning is absolute or relative. 
	- instead you should use transform properties such as translate() and rotate()
- Here is a article that shows best practices as well as some tips on how to diagnose performance: https://web.dev/articles/animations-guide
###### willchange
- hardware acceleration (handing off pixel work to gpu) can occur with certain animations which can lead to some slight imperfections in the animation depending on the os and browser
- you can avoid this by using the `will-change: transform;` property
	- this hints to the browser to let the gpu handle the thing entirely thus leading to greater consistency in the animation
- This property works on transform properties such as translate and rotate etc. will not work on layout transitions such as margin-top etc because transform properties use gpu anti-aliasing trickery while the layout options cannot, they need to round to nearest pixel because it works within the document flow and leads to jank
##### Respecting Motion Preference
- as an access measure, you should include the option to remove any transitions if users prefer no motion for motion sickness purposes. 
	- to do this:
```css
@media (prefers-reduced-motion: reduce) {
  .btn {
    transition: none;
  }
}
```
- this means that animations will resolve immediately to their finished state
- 