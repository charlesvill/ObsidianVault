### Animations
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
###### will change
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

### Keyframes
- what is the difference between css animations and transitions?
	- a transition was designed to be used from one state to another triggered by a user interaction or a specific event
	- animations were designed to be looped, and do not rely user interactions like a hover or focus. they can run as soon as the page loads the css file
	- article on keyframes: https://www.joshwcomeau.com/animation/keyframe-animations/
- syntax: 
```css
#ball {
  width: 100px;
  height: 100px;
  background-color: red;
  border: 1px solid black;
  border-radius: 50%;
  animation-duration: 2s;
  animation-name: change-color;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

@keyframes change-color {
  from {
    background-color: red;
  }
  to {
    background-color: green;
  }
}
```
- animation name is a developer defined that will be accessed by the @keyframes property
- animation iteration count could be a finite number of cycles but here defined as forever loop
- animation direction defines how it returns to the beginning state, whether abruptly or smoothly as alternate doeshere. 
- with the `from/to` is actually an alias for 0%/100%
	- here is only two keyframes defined, at beginnign and end. the greater flexibility of animation is in being able to define more keyframes. for example: 
##### more keyframes
```css
@keyframes change-color {
	from {
	background-color: red;
	}
	50% {
	transform: scale(2);
	background-color: blue;
	}
	to {
	background-colr: green;
	}
}
```
additional keyframes are always defined in percentages*. 


## responsive sites
- using <picture /> element with webP or avif to dynamically source an image resolution based on some determined factors such as the device that you are using. 
	- ask chatgpt about this and how to implement. apparently next js does this and so does cloudinary. some of them do it on the fly with no additional steps
#### security
##### links
- with links that will take the user outside of your site, you should do the following: 
```jsx
<a href="https://twitter.com/yourhandle" target="_blank" rel="noopener noreferrer">
  Twitter
</a>
```
- the target blank means that it will open a new tab and the rel bit is a security measure to prevent the destination from having information about the site it came from.
#### Keyframes
- what is the difference between animations and transisitions?
	- transitions were meant to animate an object or event from one state to another. never meant for loops
	- animations were meant with the intention of a loop to be a part of the process
	- animations have alot more flexibility in how they are instantiated compared to transitions
	- transitions rely on a trigger
- You will use the `@keyframes {from{}to{}}` to describe what changes will take place during this animation
- go back to top lesson as reference and complete the lessons for 
### Accessibility
- Intro: topic of accessibility is referred to as a11y because there 11 letters between the first and last letters. 
- you should always use a label when using an input element
##### contrast ratios 
you should aim to have 4.5:1 contrast ratio atleast and you can use this checker tool to measure:https://webaim.org/resources/contrastchecker/

ADA compliance on websites means making digital content accessible to people with disabilities. This involves adhering to the Americans with Disabilities Act (ADA) standards, specifically the Web Content Accessibility Guidelines (WCAG). Websites need to be perceivable, operable, understandable, and robust for users with various disabilities. 
Key aspects of ADA compliance for websites: 
WCAG 2.1 Level AA:
Generally, websites should conform to WCAG 2.1 Level AA for ADA compliance. 
#### four principles of WCAG:
1. perceivable: 
	1. contrast should enable visibility in all conditions
2. Operable
	1. must alllow users to operate site through many means not just the mouse, needs to be keyboard accessible
3. Understandable
	1. use clear errors with feedback making it apparent how to fix
	2. consistent use of headings and sections logically organized to make content more easily digestable
4. Robust
	1. must be accessible by assistive technologies and user agents and must remain accesible for them throughout time


#### parking lot: 
- what are prohibited aria roles? why is this an example of prohibited use?
```js
y-axis label

<g aria-label="y-axis label" transform="translate(-36.5,0.5)">
```
##### Notes from the accessibility assignment: 

Strategy: 

started by installing npm package es-lint-a11y that helps to anaylze components in the code base 

using lighthouse in the chrome dev tools 

###### what is wrong with the bonds over time component: 
- incorrect use of aria labels in the d3 graph 

#### Sematic Html
![[Pasted image 20250917160219.png]]
- looking at this image here notice the aside for sidebar items and notice how a logical component of information is encapsulated into a section. 

#### focus elements with keyboard
- for elements that are not focusable with tab automatically like div elements, you can use tabindex=0 to allow that element to be focusable. a usecase would be the rock paper scissors project :
```html
<!-- The `tabindex` attribute makes the `<div>` elements focusable. -->
<div class='button-container'>
  <div class='rock button' tabindex='0'>Rock</div>
  <div class='paper button' tabindex='0'>Paper</div>
  <div class='scissors button' tabindex='0'>Scissors</div>
</div>
```
 - the higher the tab index the higher priority to tabbing. tab index greater than 0 is an antipattern and you dont want to do that because it will bounce the foucs around the screen and you want your user to progress in a linear fashion. you should order things in the dom the order that you want your users to progress through focus elements. 
##### hidden items
- with hidden menus such as those for smaller screens for nav bars need to use display : none to hide it from screen readers and prevent keyboard users to be able to tab into the content.
##### links
- a elements should be descriptive of where the link is going
	- ex: click me! doesnt say where vs: `Visit <a>The Odin Project</a>` 
	- it reads the `<a>` text and says link so click link says nothing about where you're going
- open in a new tab *should* notify in the a text that its a new tab (but will I?)

#### WAI ARIA
- aria is to fill the gaps in semantics or meaning for the content does not style anything
- Aria has 4 limitations: 
	- cannot change appearance
	- cannot change content
	- cannot change focus
	- cannot change keyboard event handling
- Aria has 5 rules:
	- use semantic html always unless there is nothing else 
	- never override semantic html labels
	- make sure its keyboard accessible
	- never use aria-hidden on focusable elemements
	- all interactive elements must have an accessible name
##### accessible tree
- based on the dom but contains only accessibility information
	- for our purposes focus on accessible name or name and description
	- name is what screen reader announces as the name
	- description is what screen readers will announce in addition to the name
##### aria-label
- overrides the native label to change the accessible name
##### aria-labeledby
- overrides both the native label and the aria-label to change the accessible name to the content of the id'd element that is passed to the aria-labeledby
##### aria-describedby
- takes one or more ids of an element and changes the description to the content of the elements passed to it
##### aria-hidden
- hidden to screen readers but will be visible on the screen
- useful for icons or non-content elements that would confuse screen readers if it was read aloud


#### Responsive Design
- iphone zooming - smaller screens will attempt to display a desktoip version of the website with zoom applied which messes with the scaling
`<meta name="viewport" content="width=device-width, initial-scale=1">`
- you need to include this in the meta tag

##### Avoiding fixed width and height
- width: 600px wil never be able to shrink under than that and will never fit on a phone screen
##### common responsive design pitfalls
- using percentages to define width and sizes
	- should not be the same proportions on all screens. some proportions should change depending if you're on a phone screen or a computer screen
		- examples of this include text, icons, ui elements, etc. 
	- instead: you should use static margins and use media queries if you want the margin to change on smaller screens
	- The times that using percentages works is if you want something that doesnt normally take 100% of the parent space to take all of it. 
##### Responsive Images
- for positioning, and sizing images you have properties such as `background-size` for determining the size of the image that serves as the background and `background-position` to justify the position of the image as it scales
	- these are for backgrounds set in css with `background-image: url();`
- for img elements, use `object-fit` to have some control over how it sizes itself relative to the parent container
**Problems introduced with images and differing screen sizes**
###### art direction problem
```
<picture>
  <source media="(width < 800px)" srcset="elva-480w-close-portrait.jpg" />
  <source media="(width >= 800px)" srcset="elva-800w.jpg" />
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva" />
</picture>
```
- if you have a background that needs to be formatted to look appropriate on smaller screens, you might use this to select image sources
- notice that the img element is wrapped in a picture element with source elements present
###### resolution switching problem
```
<img
  srcset="elva-fairy-480w.jpg 480w, elva-fairy-800w.jpg 800w"
  sizes="(width <= 600px) 480px,
         800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy" />
```
- will choose src file depending on screen size. 

*guide on making responsive images:* https://css-tricks.com/a-guide-to-the-responsive-images-syntax-in-html/

#### Media queries
check this code pen of a good example of how side navbars are repositioned on a flex column direction: https://codepen.io/TheOdinProjectExamples/pen/XWempGr

##### Tips
- best to limit queries as much as I can and rely onthe natural flexibility of layouts
- Print styles: 
```
@media print {
  /* print styles go here! */
}
```
consider making media styles if you're tailoring material for printing

##### complex media queries: 
- see this site for looking at mre edge cases of media query applications