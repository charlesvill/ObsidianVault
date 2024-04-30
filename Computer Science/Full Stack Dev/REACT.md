 what is the difference between a framework and a library?
	 - library is a collection of code that we import to save us time on development
	 - library is like pulling  a book off the shelf and yuou decide when and how that informatoin is used. 
	 - A framework is similiar i nthat ti is code made by someone else but the difference is that with a framework you have whats called  the inversion of control where you dont have as much control over the structure of your code. You use templates and the templates will tell you where to punch in your code. The framework is in control of the flow of your application. 
	 - what does it mean to have an opinonated or non opinonated framework? 
		 -opinionated is a subjective measure of how much freedom the user has in developing
#### The REACT App
- react apps are made out of components
- a component is a piece of the UI that has its own logic and appearance 
	- it can be as small as a button or as large as an entire page
- components are javascript functions that return mark up 
- There are multiple options for deployment of a react app: 
	- with a `<script>` tag on a CDN - content delivery network
	- or with a webframe work: 
		- vite: sort of like a deployment framework to get your react app up and running quickly with all the npm packages you need to get started quicker and has a built in web server
##### The React component
- while all components are essentially functions, some can be syntatic sugar for class and others pure functions:
	- class components - use the class syntax `extends react.component` can manage internal states and complex logic that would be useful in creating dymanic UI that reacts to user interactions for more on class sytax see [[Intermediate Javascript#Classes]]
	- functional components - more of the factory functions route (see[[Intermediate Javascript#factory functions and the module pattern]]) that typically are stateless which means it doesnt modify internal data or values
		- while functional is typically stateless (i.e does not modify) they introduced Hooks with methods to do just this.
- States vs Props
	- for some reason React likes to make up their own shitty names for things
		- States - variables and data local to the function that are typically modifiable
		- Props - variables and data that are passed as arguments to the function that are not modifiable
##### Vite
- comes packaged with eslint so you should install the prettier eslint-prettier-config see [[Intermediate Javascript#Linting]] for reference
- 