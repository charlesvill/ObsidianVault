##### Resource Links: 
- Google https://fonts.google.com/icons
- Feather Icons: https://feathericons.com/
- Noun project: https://thenounproject.com/browse/icons/term/free/
- Ionicons: https://ionic.io/ionicons

#### About

- SVG are scalable image that retain their quality as they scale without increasing the file size
	- they are often used for: 
		1. Icons
		2. graphs/charts
		3. large, simple images
		4. patterned backgrounds
		5. Applying effects to toher elements via filters
- they are defined using #XML - Exensible Markup Language [[XML & RSS]]. 
#### Linking VS Inline SVG
- generally, linking is cleaner and simpler however at the cost of not being able to dynamically tweak settings in the SVG attributes. 
- Inline can result in delays in cacheing and loading html elements but can be avioded by using web-tool like webpack or a front end library like React. 
	- *one thing to note: with inline, you will have much greater control of the fill color. if you link via a img element you will not be able to manipulate the fill color.* 
#### How to 
 - you can link an svg just like a regular picture by using an img tag and linking it to the location of the svg in your files. 
 - for linking inline the source code of the svg can be pasted inline with the html elements and be styled with css. looking down, class and ID can be added as properities of the html tag to be selected in css. can also use the `svg` type selector like you would for img 
 - *note: the sizing of an svg behaves wierdly when put next to other elements such as imgs and p. this seems to be fixed by nesting the svg in a span element. #NeedMoreHelp not sure why.*
#### Anatomy of an SVG
- *XMLNS* - XML NameSpace what dialect of xml beig used to avoid the conflicts of different elements sharing same tag name such as `<title>`. it usually likes like a URI #NeedMoreHelp on this concept. 
- *Viewbox* -  the bounds of the SVG, aspect ratio and origin of svg
- *Class, ID* - same as html
- *Elements* - like `<circle>, <rect>` and other shapes are defined by the namespace. basic building blocks
- *SVG Attributes* - can be changed using CSS 

#### Clout SVG designs
- The best animated effects on webpages are done with SVG animations find TOP on SVG to get more info on it 

