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
- refer to this article on when to use each one https://codyloyd.com/2021/css-units/
- refer to this article on all available units https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units

##### percentages
- when a percentage is used it  will be relative to some other property, like the parent value. *ex using 30% as width will take 30% of the parent container and font size will be 30% of the parent font.* 

##### Viewports
- vh or vw represent a relative percentage value to the availble viewport space. 
- more information on the various relative properties with respect to sizing things found here https://css-tricks.com/fun-viewport-units/ this also talks about respecting aspect-ratio. should come back to this
##### Choosing the right Units
- here is a video on knowing what units to be using for different contexts https://www.youtube.com/watch?v=N5wpD9Ov_To&ab_channel=KevinPowell


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
- for Text overflow, visit this page, likely will need to each time https://css-tricks.com/snippets/css/truncate-string-with-ellipsis/

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

##### Psuedo Selectors
There are times when you want to select elements that are either the first child or last child and sometimes when the elements are being hovered over or clicked. 
- `:last-child` , `:first-child` pared with a selector `p:first-child` will always select the first child that is a p. Benefit being that if you rearrange the content later it will always select the first child so not as many drastic changes have to be made
- There are also user-action psuedo classes such as `:hover` , and `:focus` that are when a specific state is ocurring. 

##### Psuedo elements
There may be instances where things need to be selected that perhaps are not their own element, but with psuedo elements, it behaves like it were a distinct element. **notice how a psuedo element marked with a double :: colon.
 - *need to select the first line of a paragraph* `p::first-line` 
	 - this gives you the flexibility to resize a page or element and wont have to worry about the font scaling affecting the first line being selected. This takes care of it all and behaves as if there were magically an html element wrapping the first line. 
##### Combining Psuedo-classes and psuedo-elements
```css
article p:first-child::first-line {
  font-size: 120%;
  font-weight: bold;
}

```
##### Before and after psuedo elements
the `::before` & `::after` selectors  can be used to add content into for example a `<p>` element by combining with the css property `content: "";` which will add the string written between the quotes. *note: most often used to add symbols, arrows emojis instead of actual text bc it's not always accessible by screen readers. *