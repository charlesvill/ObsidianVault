## Default Styles
- Different browsers add basic CSS to elements parsed on the web. Often devlopers will reset these CSS values to have consistent results regardless of the browser. 
- how to reset the CSS in browser
	- refer to this Meyer's reset: https://meyerweb.com/eric/tools/css/reset/
	- just place at the top of your style sheet

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
  src: url(../fonts/the-font-file.woff)
  format('woff');
}

h1 {
  font-family: my-cool-font, sans-serif;
}
```

3. How to use online downloaded fonts
	- after downloading ttf file, go to https://www.fontsquirrel.com/tools/webfont-generator and upload the ttf file to convert to a webfontkit
	- extract the zip file and place extracted contents into font folder in project files *the two woff files are there for compatibility* 
	- the files will contain example css for formatting the `@font-face` importing piece for the style sheets
##### How to include icon from online: 
- you dont always have to download the icons from online and include them as images, you can also import themfrom a website that supports it and then link it as a style sheet. you then use class and id markers to identify the correct icons you're trying to use. see example: 
```html
<head>
   <link 
     href="https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css" 
     rel="stylesheet"
    />
 </head>
 <body>
	 <button>
		Press Me
		<i class="bx bx-chevron-down" id="arrow"></i>
	 </button>
 </body>
```
- you see this here is how the style sheet is linked from online and then using the classes and id combo to actually import it into the file right after the text 

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
		1. simple box shadow code: `box-shadow:0.3em 0.3em .3em rgba(0, 0, 0, 0.3);`
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
- example of selecting deeply nested with psuedo selectors: `.welcome-sign > div > p:first-child` this selected the first p that was a child of a div that was inside of the class `.welcome-sign`
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
- We can also use general selectors that match part of attribute values with aspecific syntax that is similar to regular expressions though not too familar with them [[Regular expressions]] also [[#Form Validation]] 
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
- careful with absolute and relative positioning because it sometimes is not the most responsive approach. remember that you can also use padding and margins to move around objects. 
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

## Form Basics
Questions: 
	1. what are forms?
		1. They are umbrella element that connects essential data from user (client side) to data banks. 
		2. The inputs  can come in the form of dropdowns, text input, buttons, checkboxes, etc.
		3. for now, operate two functions *Post* and *Get* , which represent retrieving from and posting changes to server. *i.e google search or posting tweet.*
	2. How do they interact with the back end?
	3. What is the syntax?
		1. ex: 
```html
<form action="example.com/path" method="post">

</form>
```
- The two attributes required and seen here are the `action` and `method` attribute. 
	- action designates the location data will be sent to and method designates whether it'll be posting or getting. 
#### Form controls
- are the types of input that are options to collect data.
- each of these have available attributes that are necessary to communicating to the server how to sort the data and make meaning of it

here are some of the most important ones:
#####  Input Elements
- Text input
	- Best paired with `label` element to describe the data to enter in field area with a `for` attribute that matches the *id* in the input attributes.
	- `<input type="text" id="name" name="user_name">` 
	- Necessary to have the type attribute to define a single line text input
	- the `name` attribute is specific to naming the variable that will store this data in server side.
	- in order to have default text in the field, use the `value` attribute with text wrapped in "" quotes.
	- can be resized with the size and maxlength attribute to limit the size of the box and the number of characters allowed
- email input
	- one line with basic validation to make sure valid email strucuture is being entred
	- if email form verification fails, the psuedo class `:invalid` will match and `validityState.typeMismatch` property will return true
- password input
	- 
- number input
	- will render a step higher or lower ui to adjust value input. step can be adjusted with the `step` attribute `step="2"`
	- by default only allows integer values unless `step` is set to `step="any"`.
	- with the `min` and `max` attributes, you can constrain the floor and ceiling values
	- one would think that credit cards are best served with number input, but because of the incrementer it has rendered, it's best to actually use input type text with the attribute `inputmode` to `numeric` also setting `autocomplete="cc-number"` suggests pre-configured credit card numbers
- slider controls
	- use the `input type = "range"` 
	- by default will only have the slider that does not display the slider output amount
		- for that you will need `<output for"same as id for input">` and then use javascript to get reference to that output element and place event listener to listen for input into the input control and have the text content of the output element be the output of the slider input control
- Meter & Progress bars
	- in forms can be very handy visual see https://developer.mozilla.org/en-US/docs/Learn/Forms/Other_form_controls heading "other form features"
- text area
	- technically not an input element but useful for inputting reviews or longer collections of text
	- different from text input in that it's not a void element, it needs an opening and closing tag in contrast to some of the other input elements.
		- also another difference is that you can do line breaks (press enter)
	- for the purposes of having default text in the field, you need to put it in between the opening and closing tags as html content. again, in contrast to text input
	- to constrain rendering box across lines of text, `textarea` accepts three attributes
		1. cols - limit how many columns (width) default is 20
		2. rows - how many rows (height) default is 2
		3. wrap - soft, hard and off which render only browser wrapping both submitted and renderd and none respectively
	 - You can also control how much the user can rezise the text area with: 
		 - both 
		 - horizontal- only 
		 - veritical - only
		 - none - neither
		 - block & inline - only in block/inline direction (experimental)
- File picker
	- allows you to select one or more files to send to server. you can control file types or constrains using the attribute `accept` and allow multiple files with `multiple` attribute
- Date and Time picker
	- uses the `input` element tag with type that ranges from time to datetime-local
	- examples `input type="..."` `date`  `datetime-local` , `month` , `time` `week`
	- you can also constrict date and time with min/max and step\
- Color Picker Control
	- `input type="color"` will bring up the default operating system color-picking functionality
- more on color picker and date and time picker https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types
##### Selection Elements
anything involving a list that goes together should be nestedinside of a fieldset with accompanying legend providing description of the list
*typically, the legend handles the description of the entire list and the labels are the description for individual list items* 
- Select Dropdown
	- use the `select` element tag as parent container and `option` for each list item
	- You can initiliaze a selection with the option "selected" like `<option selected>Cherry</option>` 
	- you can use `optgroup` to parent dropdown list items that are grouped together with a label attribute `<optgroup label="fruits">`
	- you can allow the choice for multiple choices by adding attribute of "multiple" 
	- In many input forms, like the text type, you can use a datalist element to give suggested dropdown menu and even autocomplete suggestions 
		- in the input `type="text"` add attribute `list=name` 
		- right below make `<datalist id="name">` make sure it matches the list name
		- data list is the container so populate nested options like a regular dropdown to show the suggestions
	- for more see: https://developer.mozilla.org/en-US/docs/Learn/Forms/Other_form_controls heading "Drop-down controls"
- Radio Buttons
	- should be nested inside of a fieldset element, has to do with accessability and screen readers
	- Should be using labels bc it allows the label to be clickable as means to selecting the box the label corresponds to
	- syntax:
	```
<fieldset>
  <legend>What is your favorite meal?</legend>
  <ul>
    <li>
      <label for="soup">Soup</label>
      <input type="radio" id="soup" name="meal" value="soup" checked />
    </li>
    <li>
      <label for="curry">Curry</label>
      <input type="radio" id="curry" name="meal" value="curry" />
    </li>
    <li>
      <label for="pizza">Pizza</label>
      <input type="radio" id="pizza" name="meal" value="pizza" />
    </li>
  </ul>
</fieldset>
*make sure for radios that they have the same name attribute so they can be grouped together, otherwise it will not work as intended.*
- checkboxes
	- should use labels for the same reason above
- *checkboxes and radios with checked attribute will match with psuedo class :default even if they are no longer checked by user. any that are currently checked will match with the :checked psuedo-class* 
##### Buttons
Buttons all use the `button` element tag but are defined by the type attribute that define it as one of the following three: 
- Submit buttons
- Reset Buttons
- Generic button
- You can also make a button by using the input element tag and then type use submit, reset, generic. however, those are void elements and do allow HTML in their content whereas `button` elements do.
- image button
	- behave like a submit button but render like an img
	- use `input` element with img as the `type` 
	- when you submit, you send not the value, but the coordinates of where you clicked on the image relative to its local coordinates
	- more on this here:https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls#image_button
	Ex: <input type="image" alt="Click me!" src="my-img.png" width="80" height="30" />
		
	
##### Organizing Form Elements
- when staging forms on webpages, often logical sectionining is needed to chunk longer forms such as surveys to prevent users from getting overwhelmed. 
	- For this, you willl use Fieldset element
		ex: paired with the `legend` tag that denotes a logical section. each section will need the fieldset container and `legend` tag right below it.
		```html
<fieldset>
	<legend>Contact Details</legend>
	  <label for="first_name">First Name</label>
	  <input type="text" id="first_name" name="first_name">

	  <label for="last_name">Last Name</label>
	  <input type="text" id="last_name" name="last_name">
	
</fieldset>
```
	- `label` tags are good to use with checkboxes and radios but are more importantly an important description for the form control but also important for screen readers to read properly
		- look into `aria-label` for more on better making accessibility for screen readers
		- see this article for more on layout for accessibility: https://developer.mozilla.org/en-US/docs/Learn/Forms/How_to_structure_a_web_form
		-   it's common practice to use common html elements to organize such as ul, li, div, p, h1-5 etc
	- the `section` element should also be used in conjunction with the fieldset element for separating logical chunks in forms
##### dialog element and forms
- with the `<dialog>` element, you can make a form appear with javascript method `.showModal()` to submit information and make it disappear when its no longer needed
- implementation: you declare the `<dialog><form method="dialog"></form></dialog>`
	- note that the form will be nested inside the dialog element tags and the form will have to have the `method` attribute set to dialog to have the form close the modal form with a submit button see [[Intermediate Javascript#Parking lot for review in foundational JS]] for more on its implementation with Javascript.

##### using data from forms
see the javascript lesson [[Intermediate Javascript#using Form data without POST / GET]] to see how to access form data within your js.

### Styling Forms 
#### Fonts and texts
- sometimes elements in fonts dont' always inherit font rules from parents and thus may need these rules applied: 
	```css
	button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
}

```
#### Box sizing
Sometimes there will be difficulty facing consistent sizes because of each widget having their own rules for border, padding and margin and also because of each different browers reliance on operating system default settings for things. Something that can help though is: 
```css
input,
textarea,
select,
button {
  width: 150px;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

```
more on box sizing and styling forms in general found at: https://developer.mozilla.org/en-US/docs/Learn/Forms/Styling_web_forms
**Legend Styling**
- by default the legend will place itself top left corner, in order to change this, you need to set the parent fieldset position as relative and the legend position to absolute. 
- for more on styling and example see: https://developer.mozilla.org/en-US/docs/Learn/Forms#form_styling_guides
- \
### Advanced Form styling
checkboxes and radio buttons along with input type search bars tend to be more difficult to style compared to others
	Some elements cannot be styled solely with CSS these include: 
		- `select` `option` , `optgroup` , `datalist`, `input type color`, 
		- Date related controls such as date, datetime-local
		- range, file, progress and meter
#### Appearance property
- the appearance property can be used to control OS-level styling that can be applied by default in forms. 
	- the best application of appearance is to set it to none to allow css styles to built from the ground up to allow again for greater consistency and experience across browsers and devices. 
		- useful for radio, checkboxes, search bars in removing inconsistencies
- Selects and Datalists
	- on a select again the dropdown arrow could look different depending on what browser you're on, again bringing the appearance property useful
	- making a new arrow using generated content required the use of a wrapper of div around the select element because of the way the browser renders form elements specifically
	- use the ::before/::after psuedo class to add the dropdown arrow to the wrapper div
		- more on this : https://developer.mozilla.org/en-US/docs/Learn/Forms/Advanced_form_styling
	- More issues styling encountered when looking at the box appearing with the options, styling such as spacing and colors of the options box would require custom libraries to be imported or building your own custom form control.
	- *worth nothing that you can use the multiple attribute to display all the optoins on the screen at  once sidestepping this issue though it may still not conform to the page's intended design aesthetic*
- Date input types
	- Literarlly SOL with styling the rendered date picker calendar, limited to the box that you can click on. 
	- not even `appearance="none"` works here
		- again, if you want something stylized, need library or build a custom one.
- file input types
	- the button itself is completely unstylable.
	- what you could do is hide the button itself by putting opacity to 0 and using an attached label and style that one normally and user can just click on the label like normal.
- Meters and Progress Bars
	- Even worse tbh outside of changing the fill color nought is possible. appearance as none makes things worse
		- go to progressbar.js : https://kimmobrunfeldt.github.io/progressbar.js/#examples
			- Third party solutions for progress bars
### UI Psuedo-classes
- `:required` / `optional` targets elements that can be required or optional according to html attribute of `required`.
- `:valid`/`:invalid`, `:in-range`/`:out-of-range`
- `:enabled`/`:disabled`, and `:read-only`/`:read-write` the latter for attribute `readonly`
- `:checked`/`:indeterminate`, and `:default` checkboxes and radio buttons that checks if neither option was selected or neither check nor unchecked and if it was the default option when the page was loaded.
- Using generated content with psuedo-classes
	- using the ::before/::after, you could style cool custom radio/checkbox dials that do not clutter the html page and thus screen readers and accessibility devices. Example here: https://developer.mozilla.org/en-US/docs/Learn/Forms/UI_pseudo-classes Heading: using generated content with psuedo-classes
- Valid/invalid triggers
	- some of the things that will trigger an invalid to be selected in css are: 
		- controls with `required` that are left empty
		- controls with built in validation like email and url that doesnt match with its requirements
		- current value is outside range limits specified in min/max attributes, but also matched with `:out-of-range`
		- more to see in [[Intermediate Javascript#Client side form validation]]
- for Enabled/disabled see above psuedo classes article link 
- Read-only and Read-write
	- use the attribute `readonly` right before the closing tag
	- use cases: if you have already typed in info on a previous page but wish to have it populated as read only so the user to reference inputs they made on a subsequent page
- :default and :indeterminate
	-  things that can be considered indeterminate include:
		- radio/checkbox/progress
- Come back to test your skills advanced styling if I'm having trouble with project
	- see internetishard article on styling and forms https://internetingishard.netlify.app/html-and-css/forms/index.html
- Good article on improving UX in forms https://www.silocreativo.com/en/css-rescue-improving-ux-forms/

## Form Validation 
Form validation gives a precheck before user submits data to the server to protect servers from recieving incorrect data.
	some examples of validation include:
		- required validation (add `required attribute to it`)
		- text length validation (min/max) `minlength`  or the `maxlength` attribute
		- Number range validations `min` `max` attributes to define the range for number based inputs
			- *note: if you don't put a step attribute, it will default to 1 which will be floats will not be seen as a valid entry*.
		- Pattern validations for things like credit card inputs or zipcodes, we want certain patterns to be met and you use `pattern attribute` 
			- can only be used on `input` elements
	- what are regular expressions? patterns used to match character combinations in strings. in javascript regular expressions are objects [[Intermediate Javascript]]
		- see this article for more on expressions https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions
				-quick start quide:
					`[Bb]`anana | `[Cc]`herry this says either capital or lowercase but the rest has to match with either of the two separated by the pipe
					*textarea does not support the use of the pattern attribute* 
	- what are some of the errors that will be presented prebenting a form from being submitted?
		- badInput
		- patternMismatch
		- rangeOverflow
		- rangeUnderflow
		- stepMismatch
		- tooLong
		- tooShort
		- typeMismatch
		- valueMissing
		- customError
## Grid 
- useful guide to review grid elements https://css-tricks.com/snippets/css/complete-guide-grid/#aa-grid-area
- see this for inspecting the grid elements https://developer.chrome.com/docs/devtools/css/grid/


- grid makes page layouts alot easier 
#### review on flexbox
- flexbox was useful for aligning containers along the main and the cross axis
- `flex-wrap` was useful for having items flow over to either the next row or the next column
- grid layouts can make evenly sizing items much easier compared to flex
- video resource on when to use flexbox vs grid https://www.youtube.com/watch?v=hs3piaN4b5I
#### getting started on grid:
in a div container with 4 items, you can place this css on the container to declare it a grid:
```css
	.containter{
	display: grid;
	grid-template: 50px 50px/50px 50px 50px
	}
```
- the `grid-template` part defines the rows and colums each 50px separarated by space denotes the number of rows and colums. rows go first so its two rows size 50px and three columns of 50px each
- Grid track can be defined as a direction of grid elements either in the rows or the column direction
	- basically either a row or column so when you define `grid-template` you are defining the number of tracks you will have for rows and columns
#### implicit vs explicit grid
- if you were to add an additional html element in the container without declaring it in the css grid-template, it would still be populated as an additional row as an implicit grid element. 
	- wtih the grid-template you are explicitly defining the track sizes but it will not cover the settings of implicit track izes. if you want settings to cover the implict track sizes you will need the property `grid-auto-rows: 50px;` for the columns it will follow the same structure as the one seen here for rows. 
- `grid-auto-flow:` this will define whether the implicit grid items will be added either inthe row or column direction. aka being populated vertically or horizontally
	- *note: if you decide to use grid-auto-column, you'll also need to set the grid-auto-flow to column*
#### Gap 
- use the property: `column-gap` and `row-gap` to set the alley between each respective item. also accepts the shorthand gap prpoerty to set both of them
	- **this is placed on the parent container div**.
	- shorthand: `gap: 1em 20px;`
		- `row-gap` , `column-gap` 
*to add a border, go on the individual grid element selector and put border: 1px solid blue;*
#### Parent container vs children properties
Parent properties include but are not limited to:
- display
- grid-template
- grid-gap
- gap
- justify-items
- align-items
- place-items
- grid-auto
child properties include but are not limited to: 
- grid-column/row-start/end
	- determine a grid items location by referring to specifc lines
		- shorthand: `grid-column: 4 / 6;` what this means is that the grid column start is at line 4 and the end is at 6, so it spans two lines separated by the forward slash. 
		- options include specifying a line or using the `span` option that span across the number of lines following the span option and also a name option that will span until you hit the line with the specified name listed after the span option
		- `auto` option indicates auto-placement an automatic span or a default span of one
	- see the above guide for more information on placing the grid elements using the different placing properites on the children

#### positioning grid elements
On lines: 
- everytime that tracks are created, lines are creatd implicitly, lines cannot be created explicitly
- the lines are numbered from the start of the track to the end of the track in both the vertical and the horizontal directions
	- so a 3x3 grid has lines 1 through 4 on both the vertical and the horizontal directions
	- used to position grid elements
On Cells: 
- you can place positioning elements on individual cells to make them span more than one cell using the `grid-column-start:1` and the `grid-column-end:6` propertys that will extend the cell that has these properties from lines 1 to 6. (on a 5x5 that would have 6 lines)
- shorthand for each `grid-column` and `grid-row` in the syntax `grid-column:1 / 4;` where the 1 is the start and the 4 is the end
- alternatively, you can also use the `span` property to have it span the number of lines that you specify
grid-area
- shorthand to position all four aspects (column/row&start/end) 
```css
#living-room {
  grid-area: 1 / 1 / 3 / 6;
}
```
- the order of the properities is as follows: 
	`grid-row-start`/ `grid-column-start` /`grid-row-end` /`grid-column-end` 
grid area also can refer to a few other things such as: 
- default spans: if no start/end grid values defined it wil default to the span of one track for both column and row.
- counting backward: specifying a negative value will count from the back `grid-column-start:-1;` this is very useful for making grid elements span across the templates
- `grid-template-areas` 
	- instead of defining the grid area with lines for each element, make a template out of words as seen here: 
```css
.container {
  display: inline-grid;
  grid-template: 40px 40px 40px 40px 40px / 40px 40px 40px 40px 40px;
  background-color: lightblue; 
  grid-template-areas:
    "living-room living-room living-room living-room living-room"
    "living-room living-room living-room living-room living-room"
    "bedroom bedroom bathroom kitchen kitchen"
    "bedroom bedroom bathroom kitchen kitchen"
    "closet closet . . ."    
}

.room {
  border: 1px solid;
  font-size: 50%;
  text-align: center;
}

#living-room {
   grid-area:  living-room;
}

#kitchen {
  grid-area: kitchen;
}

#bedroom {
  grid-area: bedroom;
}

#bathroom {
  grid-area: bathroom;
}

#closet {
  grid-area: closet;
}

```

- the periods here represent empty cells that can be changed later
##### extra grid properties
- justify-self: aligns the grid item along inline (row) axis within its individual cell
	- options: start- flush with the start edge of the cell 
	- end- flush with the end edge of the cell
	- center- aligns in the center of the cell
	- stretch- fills the whole width of the cell (default)
- align-self: aligns the grid item along the block (column) axis within the individual cell. with the same options as justify-self
- place self: sets both the align-self and the justify-self in one single declaration
	- options: auto - default alignment for layout mode
	- `<align-self> / <justify-self>` if one of these is omitted then the one provided is carried over to both
		- ex: `place-self: center stretch` AS is center and JS is stretch to fill along the row axis
- *centering content inside of grid elements using the grid layout* 
	- if I wanted to center some text for example that is the content of some grid elements, you will need to select all the grid elements and then set their displays all to grid and add the following properties as well:
		- `align-items: center;`, `justify-items: center;`
##### Special units and functions
- fr- fractional unit. they are a portion of the remaining space of the parent container. for example if the total width for a grid is 400px and the four columns have their defined size as 1fr, then each of the four columns will be 1 fraction of the 400, 100px. 
	- ex: `grid-template-columns: 1fr 3fr;` roughly translates to 25% and 75% except that they work alot nicer with additional things like padding an margin compared to say explicitly declaring a percentage.
- sizing keywords: 
		- min-content: the smallest the grid can be before it will stop shrinking the elements inside of it and trigger the overflow and using the scroll bar to see the rest
		- max-content: 
			- can only be used with the `grid-template-column/row` and `grid-auto-columns/rows` 
			- it will take two arguments: the minimum size the grid track can be and the maximum size it can be
			- it makes sense to use static values like pixels. 
		- auto-fit and auto-fill: 
			- part of the repeat funciton 
			- both will return the largest possible positive integer without the grid items overflowing
				- ex `width: 1000px; grid-template-columns: repeat(auto-fit, 200px);` this would effectively return 5 because with columns of 200 px, at 1000px of width the largest possible interger would be 5 to fill the whole width.
				- *the real beauty is when you combine this in the repeat function with the minmax() function to dynamically tell you how many columns/rows you can have given a min and max size*
				- ex: `repeat(auto-fit,minmax(150px, 1fr));` 
				-think of like a page with lots of items like a youtube results and with the screen size it will dynamically show the # of columns of thumbnails based on the size of your screen. 
			- auto fill will the most time work exactly the same except when ther are less items than can fit on a row, the auto-fit will keep the grid items at their max size and auto-fill will snap back to the min size and will add another grid item once there is space permitting. 
				- #NeedMoreHelp see TOP Lesson on advanced grid properties
				- for the most part auto-fit will be filling the entirety of the space provided looks like while auto-fill will stay smaller size
 - sizing functions: 
	- `fit-content()` uses the space abiabilebutneer less than the min-content and never more than the max-content. 
	- `minmax()` sets a minimum and maximum value for what the length is able to be. this is useful when paired with relative units *this is really useful for fixing awkwardly sized grid cells*
		- ex `grid-template-columns: minman(100px, 1fr) 3fr;`
		- see https://css-tricks.com/you-want-minmax10px-1fr-not-1fr/ for more on this
	- - clamp(): review from [[Intermediate CSS#clamp()]]
				- typically want to do a static size for the min and max arguments but a relative or dynamic value for the ideal
		
#### Practicing grid and web layouts
- to see an example of how you would do a layout of a webpage with a header, nav bar, sidebar , article section and a footer , see the TOP practice problem for the css-exercises "01-grid-layout-1".

#### Advanced Grid Properties
- when changing zoom levels you can use the property: `overflow: auto; ` to enable scrolling if the grid container is smaller than the grid could accommodate
- user size controls on grid: `resize: both` gives the user the control to resize the grid by clicking and dragging the bottom right corner of the grid container.
## Grid vs Flex
- when should you use one over the other?
	- Content vs Layout centered desicions 
		- if your website is centered around a particular content then flex is great to use the logical rules and proportions to center the layout around the content. 
		- if your website is more layout centered meaning that you have a clearer idea of how you want the structure of the website to look more than the content, then you go with grid and then the content will follow the contraints of the tracks laid out by grid
	- further, if you're trying to layout a 1 dimensional layout, flex could be more intuitive to control the items along the axis
	- on the contrary, complex 2 dimensional layouts: grid.
	- They are not however, mutually exclusive. How to use them together: 
		- one use case is to make the parent a grid container and then the children flexboxes to control their content layouts
	- some things to consider for pros and cons of each one: 
		- grid is not able to do row-reverse and column and row direction swaps on the fly like flexcan do as easily
		- video on more for when to use one or the other: https://www.youtube.com/watch?v=HYji_V2aYa0
		- article expanding on use cases for each: https://webdesign.tutsplus.com/flexbox-vs-css-grid-which-should-you-use--cms-30184a
#### Transitions
- when you want something to animate or move with css, like with an image carousel, you can use the transition property with the value of transformX()
	- they work relative to the base position on the top right. so if you want your image to slide right: 
		- `transition: transformX(-480px);` placed on a selector class that is dynamically placed using js see[[Intermediate Javascript#Modifying classList names]]
		- then, on the parent, if you want smooth transitions, you'll need to add the property: `transitions: ease .5s;` where you specify how long the transition should take. 
