- where questions come up and gradually get answers

- [ ] Why use `span` to nest elements inside of it in contexts other than putting emphasis or bold. ex in context
	`<label><span><input type="checkbox"/></span>True</label>`
	lesson in context [[Intermediate CSS#Advanced Form styling]]
- [x] What is the purpose of using ::before and ::after psuedo classes to insert content like emojis? why couldnt it just be put as part of the content in the html tag?
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

