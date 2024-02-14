##### reference links
- Find link here for reference https://docs.emmet.io/abbreviations/syntax/
	- cheat sheet: https://docs.emmet.io/cheat-sheet/
- link to good video: https://www.youtube.com/watch?v=V8vizNQKtx0

### Syntax

1. highlight area or elements
2. ctrl-shift-p to open command pallette and type "wrap Abbreviation"
3. typing "div>div>ul>li.list" will give you the following. 
```html
<div>
	<div>
		<ul>
			<li class="list"></li>
		</ul>
	</div>
</div>
```
- ref to code snippet markdown [[The 8 Most important Hotkeys]]
#### wrapping multiple lines in tags
- you can wrap plain text in individual list items 
- Highlight the lines
- use "div.exClassname>ul.prioritylist>li*"
- the "*" abbreviation will add a li item for each line. *.

####  Controlling the output  location of lines 
- using `$#` as a psuedo placeholder for example: `ul>li[title=$#]*>{$#}+img[alt=$#]`
-this gives you: 
```html
	<ul>
    	<li title="About">About<img src="" alt="About"></li>
    	<li title="News">News<img src="" alt="News"></li>
    	<li title="Products">Products<img src="" alt="Products"></li>
    	<li title="Contacts">Contacts<img src="" alt="Contacts"></li>
    </ul>
```

#### populating multiple elements with abbreviations

- in VS code, you can write out the abbreviations in the vscode document without actually using the wrap shortcut (which is ctrl-opt-w)