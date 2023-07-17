## Default Styles
- Different browsers add basic CSS to elements parsed on the web. Often devlopers will reset these CSS values to have consistent results regardless of the browser. 


## CSS Units

##### Absolute units vs relative units
- the only absolute unit in web projects you should be using is px
- the family of relative units all can change based on their context\
- articles suggest using rem for the font and using px for margins, padding etc. the main difference being that using relative for padding and margins will allow the more accurate scaling as things zoom or are on different size screens, however it may lead to unnecessarily large unused space. 
- long answer is it depends on the priority pendulum leaning towards either functionality or aesthetics wherein the scaling proportions would need to be more tight. 

##### em and rem 
- both are referring to a font size, could be other things, ***prefer rem over em. 
- em is the font size of the element or the element's parent it's multiplied to the font size so 4px font with 4 em equals (4px * 4em == 16px )
- rem is the same except that it uses the root elemtent so it doesn't get changed if parents change or contexts change. better consistency. 
- refer to this article on when to use each one https://codyloyd.com/2021/css-units/ [[CSS reference Notes]]
- refer to this article on all available units https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units [[CSS reference Notes]]

##### percentages
- when a percentage is used it  will be relative to some other property, like the parent value. *ex using 30% as width will take 30% of the parent container and font size will be 30% of the parent font.* 

##### Viewports
- vh or vw represent a relative percentage value to the availble viewport space. 
- more information on the various relative properties with respect to sizing things found here https://css-tricks.com/fun-viewport-units/ this also talks about respecting aspect-ratio. should come back to this [[CSS reference Notes]]
##### Choosing the right Units
- here is a video on knowing what units to be using for different contexts https://www.youtube.com/watch?v=N5wpD9Ov_To&ab_channel=KevinPowell [[CSS reference Notes]]



## More Text Styles

##### Nice System Font Stack
- The purpose of this string of code is to access the installed fonts on the system and will generally produce nuetral font style:
	```css
body {
  font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}
```


##### How to include different Fonts
1. **Online font libraries**
	1. font libraries like google fonts, Font Library or adobe fonts
		1. select font
		2. copy snippet from website 
		3. link in html ex 
		4. or you could also use an `@import` tag that can be dropped at the top of a css sheet
```html 
		<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
```

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
```

2. **Downloaded fonts**
	- You can also download them and import them into your project and link the file with the `@font-face` tag on css ex: 
	```css
@font-face {
  font-family: my-cool-font;
  src: url(../fonts/the-font-file.woff);
}

h1 {
  font-family: my-cool-font, sans-serif;
}
```


##### Letter-spacing & Line Height
- you can use `letter-spacing: .5em;` to bring together or space out fonts that might aesthetically benefit from tweaking. 
- the `line-height: 1.5` does similar for adjusting relative to normal spacing\

##### Text-transform and text Overflow
- allows you to capitalize element's text value. you can do all uppercase, capitalize or all lowercase with the attribute `text-transform: lowercase;` 
- for Text overflow, visit this page, likely will need to each time https://css-tricks.com/snippets/css/truncate-string-with-ellipsis/ [[CSS reference Notes]]


## Plethora of CSS Properties
- there are hundreds of properties though 90% of the time only a much smaller pool of them are used. Here are some of the properties that have not be talked with as much detail: a
	1. *Background* (dont freak on the syntax) https://developer.mozilla.org/en-US/docs/Web/CSS/background
		1. check out this other CSS tricks resource https://css-tricks.com/almanac/properties/b/background/
	2. *Box Shadow* best used sparingly and lighter, more subtle https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow
	3. *Overflow* when your content doesnt fit on a line or space, you can use scroll bars or the like to style user access to extra lines https://developer.mozilla.org/en-US/docs/Web/CSS/overflow



## Advanced CSS Selectors

Previously we've seen css selectors like chaining `.parent #child` combinators. we can be more specific with child and sibling combinators
	*ex html:*
```html

<main class="parent">
  <div class="child group1">
    <div class="grand-child group1"></div>
  </div>
  <div class="child group2">
    <div class="grand-child group2"></div>
  </div>
  <div class="child group3">
    <div class="grand-child group3"></div>
  </div>
</main>

```

1. `>` - the child selector
	```css
/* This rule will only select divs with a class of child */
main > div {
  /* Our cool CSS */
}
/* This rule will only select divs with a class of child */
main > div {
  /* Our cool CSS */
}

```

2. `+` - the adjacent sibling
	- it seems the way this works is the + bumps to the adjacent below it or around it hence why these examples will select the group1 plus how many div are added
	- the last +div will be the one that is being selected
```css
/* This rule will only select the div with the class child group2 */
.group1 + div {
  /* Our cool CSS */
}

/* This rule will only select the div with the class child group3 */
.group1 + div + div {
  /* More cool CSS */
}
```

4. `~`  - the general sibling combinator
	 - This one will select siblins in the same indentation level
```css
/* This rule will select all of .group1's siblings - in this case the 2nd and 3rd .child divs */
.group1 ~ div {
  /* Our cool CSS */
}
```

##### Psuedo  class selectors
There are times when you want to select elements that are either the first child or last child and sometimes when the elements are being hovered over or clicked. 

**Structural class selectors**
select elements based on their position within the DOM
- `:root` very top level of the document, no parents. generally equivalent to html element
	- typically where the document wide css rules will go
- `:last-child` , `:first-child` pared with a selector `p:first-child` will always select the first child that is a p. Benefit being that if you rearrange the content later it will always select the first child so not as many drastic changes have to be made
	- *note: you can also count back or forward from last or first ex `div:last-child(3)`* 
- `:empty` match elements with no children at all
- There are also user-action psuedo classes such as `:hover` , and `:focus` that are when a specific state is ocurring. 
- *should be noted that psuedo class have the same specificity as regular classes*
**Dynamic psuedo class selectors
- use `:nth-child` followed by (n) that you want to select to be really specific if there are alot of children or have specific way to select
	- ex: 
	```css
 .myList:nth-child(5) {/* Selects the 5th element with class myList */}

  .myList:nth-child(3n) { /* Selects every 3rd element with class myList */}

  .myList:nth-child(3n + 3) { /* Selects every 3rd element with class myList, beginning with the 3rd */}

  .myList:nth-child(even) {/* Selects every even element with class myList */}
```



##### Psuedo elements
There may be instances where things need to be selected that perhaps are not their own element, but with psuedo elements, it behaves like it were a distinct element. **notice how a psuedo element marked with a double :: colon.
 - *need to select the first line of a paragraph* `p::first-line` 
	 - this gives you the flexibility to resize a page or element and wont have to worry about the font scaling affecting the first line being selected. This takes care of it all and behaves as if there were magically an html element wrapping the first line. 
	 - `::selection` allows you to change the highlighting when user clicks on the page
	 - `::marker` allows you customize the syling of the `<li>` elements bullets or numbers
	 
##### Combining Psuedo-classes and psuedo-elements
```css
article p:first-child::first-line {
  font-size: 120%;
  font-weight: bold;
}

```
##### Before and after psuedo elements
the `::before` & `::after` selectors  can be used to add content into for example a `<p>` element by combining with the css property `content: "";` which will add the string written between the quotes. *note: most often used to add symbols, arrows emojis instead of actual text bc it's not always accessible by screen readers. 
- this has been used to insert empty string and add block dimensions and color to add shapes and images along with text
**more on psuedo element properties** https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements


**more on psuedo selectors and elements** https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements


##### Attribute Selectors
`src='picture.jpg'` or `href="www..."` all examples of attributes that need more flexible system of targeting them 
	- same specificity as classes and psuedo classes
- There are three ways to target a specific attribute: 
	1. `[attribute]` - ex `[src]{...}` this will target any element that has the src attribute
	2. `selector[attribute]` - ex `img[src]{...}` this will target img elements with src attribute
	3. `[attribute="value"]` - to get really specific match with a specific attribute
- We can also use general selectors that match part of attribute values with aspecific syntax that is similar to regular expressions though not too familar with them [[Regular expressions]]
	- `[attribute^="value"]` `^=` - matchs strings from the start
	- `$=` matches strings from the end
	- `*=` is a wildcard selector that will match any where in the string
- more on attribute selectors https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors [[CSS reference Notes]]
- ex
	```css
[class^='aus'] {
  /* Classes are attributes too!
    This will target any class that begins with 'aus':
    class='austria'
    class='australia'
  */
}

[src$='.jpg'] {
  /* This will target any src attribute that ends in '.jpg':
  src='puppy.jpg'
  src='kitten.jpg'
  */
}

[for*='ill'] {
  /* This will target any for attribute that has 'ill' anywhere inside it:
  for="bill"
  for="jill"
  for="silly"
  for="ill"
  */
}
```

## Positioning 

#### Static vs Relative Positioning
 - *static* is the default positioning behavior all elements will have entering the page
 - *Static* means just following the standard document flow and populating the elements in the order they're placed in the DOM
 - *Relative* behaves the same as Static on the page but allows you to use properties like left, bottom, etc. to shift over it's positioning relative to how it would be if it were standard static. 
	 - ex: 
	```css
	.child-one{
	position: relative;
	left: 10px;
	}
```
- **Note on relative Pos** - not normally used with directional property but more so placed on the parent of an element that you wish to place absolutely. This is because of that relative positioning that will place it relative to where it would be in the static flow and the absolute inside of it will correspond to the relative positioning. otherwise the absolute would not respect any containers or other elements.

#### Absolute Positioning
- removes itself from document flow and allows you to position at exact point on the screen without moving any other elements
- useful with using the directional properties 
#### Fixed Positioning
- similar to absolute in that it remves itself from the document flow but it positions itself relative to the viewport, not any parents or root documents 
- Big take away is that it will fix it's position regardless of where you scroll to on the page. 
- takes in directional properties like the others
#### Sticky position
- a combination of relative positioning and fixed positioning into one, While it's in view its relative positioning that is bound to it's parent positioning if it's relative or absolute, however when you scroll past it, it wil behave as a fixed position and stay in the position determined by the direction propery given
	- ex: `top: 10px` means it'll stay 10 pixels from the top of the view port as you continue to scroll down.
	- *important to note it's normal until it reaches the offset that was set* 
- Resource page on positioning https://developer.mozilla.org/en-US/docs/Web/CSS/position

## CSS Functions
#### calc()

- Used for handling alot of nesting of different units when specific quanties needed that need to be changed dynamically. 
- *do not need it inside of min(), max(), or clamp()*

#### min() & max()
- min() is a css function that helps to define a boundary for the maximum size/value. 
- in it essence, it calculates the arugments passed and determines which of the (up to three) arguments is the smallest and picks that one as the size
- min() takes two parameters `min(150px, 100%)` where the first value is the size maximum it will take if there is enough space. the second argument says if there is not enough space, it will take up 100% of the parent width or the property that this is being used on. 
- max() does the same but the opposite, determines which of the passed values is the biggest one and picks that one as the value. 
- Because of the way it interacts as the parent container can dynamically change, it could appear as if the max was really setting a minimum size among values passed through. 
#### clamp()
- clamp uses three parameters that are a minimum , an ideal, and a maximum. 
- what of the three is used depends on how the parent container is being sized as screen available spaced is changed. 
	- If bigger than the ideal, switch to maximum.
	- smaller than maximum, it'll stay in ideal until parent container gets too small to fit  the ideal and switches to the minimum. 
- clamp() can also be used to create dynamic and fluid sized fonts. bitchin'
**NOTE: for these three functions you do not need to include calc() inside. already baked into it**

More on these three CSS functions found here: https://web.dev/min-max-clamp/ [[CSS reference Notes]]
Practical applications of each of these: https://moderncss.dev/practical-uses-of-css-math-functions-calc-clamp-min-max/ [[CSS reference Notes]]

## CSS Variables and Custom Properties
allows us to define a color value for example and use it throughout larger projects and not have to be as verbose for each instance of the color and can change the value of that color from the single variable as opposed to changing each instance of the color.

- Declaring a variable would be similar to any other language except for: 
	- `--variable-name: red;` needs to be initalized by two dashes
	- Uses Kebab case
	- Case sensitive
- when accessing variable throughout your project, you need to use the `var()` function with the variable name inside of it.
	- *var function accepts two parameters, the second being a fallback property incase the first one is not valid or hasn't been initialized yet. you can also refer to another custom property that itself has another fallback property and so on and so forth*
		- ex:
		- as seen here, the fallback is a var with it's own fallback of yellow
		```css
color: var(--undeclared-again, var(--color-text, yellow));
```
#### Scope of Custom Properties
- scope of where you can access custom properties work similar to block scope in JS. 
	- if you want a custom property to be accessible throughout the whole document, you'll need to use the `:root` selector instead of `html` selector as the former has higher specificity.

##### Inheritance of custom properties
- if a parent container has a selector that gives them a custom property, it's children will inherit the same value unless the children have their own custom property assigned to them via a selector.

##### Making themes with Scope and :root
- because of the rules of scope you could create two separate selectors for class light and dark that use the same property names but different values for light and dark themes respectively. Then, using something  like a media query could change the class on the root element and the respective properties will feel the values to the instances of the property found throughout the document that color the background, the text, divisions, etc.
- see custom properties TOP lesson for more information and syntax: https://www.theodinproject.com/lessons/node-path-intermediate-html-and-css-custom-properties

## Frameworks and Preprocessors

- Frameworks are sets of premade css stylesheets that utlize quick ways of populating much of the common parts of a typical page such as footers, navbars, split views, etc. 
	- popular frameworks include Bootstrap and tailwinds css
- Essential to know the foundations however for debugging and tweaking the framework baseline as at times they can be very generic and patterns will arise in websites that point towards a specific framework and hurts creativity. 
- something very useful about frameworks is it can standardize the conventions for class naming and IDs which could help with working on teams and avoid subjectivity and "personal flair" from individual develepors allowing for a more uniform consistent styling.
- **Preprocessors** are utilties that can be installed that involve a language used to speed the flow of writing CSS. Often times it will take a specialized style sheet that utilizes the custom language and then it will process it into a regular css sheet and/or merge with an existing style sheet for compatibility. Helps with expediting syntax, repetitive things, features that css does not all have on its own such as a nesting structure similar to how html nests. 
	- popular preprocessors include SASS and LESS
	- SASS has the largest user base of developers
- Typically the sentiment in the community is that preprocessors help projects scale as they get more complicated with more style sheets and they are easier to maintain once it's been deployed.
- another sentiment is that stying deeply nested html elemeents are easier to read with preprocessor syntax
- Overall, it is important to consider who will be working on your project and what the development cycle is going to look like (who will maintain, if you might need to undo the preprocessor/framework) and debugging could be over all more difficult with preprocessors.