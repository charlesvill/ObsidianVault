###### parking lot: 
- Why do components that accept parameters or "props" need to have curly braces around the parameters? like the ones seen here: 
```jsx
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {isPacked ? (
        <del>
          {name + ' ✔'}
        </del>
      ) : (
        name
      )}
    </li>
  );
}
```
- when the main entry point or app component that calls other components use the syntax `<List animals={animals}/>` what is it doing? is it initializing a parameter to pass through to the List component? and why does it have to look like that and not a more traditional parameter for vanilla js function?
### Intro to React
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

#### JSX
- it looks like html in javascript which it is but its also syntatic sugar for creating a react element function. without jsx you could call this function and insert the props, states, children one by one. 
- used because it allows the rendering logic and the content to live in the same place for a more visual approach to your UI (as a component)
##### rules/syntax: 
- Must return a single root element - if you need to return mulitple like many divs you need to nest it in a react fragment : `<></>` which is literally empty tags because you dont want the elements to have a container. 
- Tags that normally self close need to be explicitly closed like: `<input> -> <input />` or `<li></li>`
- camelCase for most things - bc it turns into javascript, html elements and their attributes turn into objects and keys of those objects. so reserved words like class cannot be used. thus, you use camelCase `class="hello" -> className="hello"` 
- *exception:* `aria-*`, and `data-*`, are kept with the dash as in html because of historical reasons
- passing strings and dynamic values through jsx: 
	- because its just javascript, you can embed strings in the mark up like you would any variable that holds a string such as {name} or use "Charles" make sure not to use it for element tags because that will not work
	- `src={avatar}` would be the correct way to dynamically create the src and not using double quotes.
- Passing objects: `person={{name: "Hedy Lamarr", inventions: 5}}` notice double braces
	- the first curlies are the access to JSX allowing javascript. 
	- second curlies are for the javascript object with key value pairs
- passing inline css styles: 
```jsx
export default function TodoList() {
  return (
    <ul style={{
      backgroundColor: 'black',
      color: 'pink'
    }}>
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```
- notice here the presence of the double quotes in the style attribute for the ul element
- *note that style properties are written in camelCase such as:* `style="background-color : black" -> backgroundColor: black`
- multiple expressions in objects: 
```jsx
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}

```
- notice here the super unique way of building your person object with a theme that matches the person and how you can just pull the theme and name in the mark up using dot notation. it's pretty cool
- **Convertting html into jsx** : use transform website tool: https://transform.tools/html-to-jsx
###### conditionals in React
- ternery operators are big in react like `{cond ? <A /> : <B />}`
- the and operator && is used as well in ways I hadnt before: 
	- `{cond && <A />}` this means if cond true, render A or else nothing. 
###### rendering lists
- rather than using something like a for in loop, react users employ arr.map() or arr.filter()
	- see [[Intermediate Javascript#array methods]] for more on iterative array methods
- *careful with arrow functions* in those array methods because arrow without curly braces imply return but curly braces will not explicitly return without you writing return line. this is because its used for writing a block of code as opposed to one line. 
- Each array item needs a key that can be either a string or anumber that uniquely identifies it amongs the other members in the list `<li key={person.id}>...</li>`
- whenever you use map() each call will need to assign a key in order to avoid errors
- *rendering multiple DOM nodes for each list item* you can only pass one key per `<>...</>` so need to do something else. see: https://react.dev/learn/rendering-lists LOOK FOR THE DEEP DIVE
```jsx
import { recipes } from './data.js';

function Recipe({id, name, ingredients}){
  return (
    <div key={id}>
          <h2>{name}</h2>
          <ul>
            {ingredients.map(ingredient =>
              <li key={ingredient}>
                {ingredient}
              </li>
            )}
          </ul>
        </div>
  )
  
}

export default function RecipeList() {
  return (
    <div>
      <h1>Recipes</h1>
      {recipes.map(recipe =>
        <Recipe key={recipe.id} name={recipe.name} ingredients={recipe.ingredients}/>
      )}
    </div>
  );
}

```
- here is some syntax of: 
	- a) calling other components
	- b) passing "props" as arguments
	- c) demonstrating reacts ability to populate an array of list markup automatically (the return of map is an array of list elements)
- *notice the parameters defined have curly braces* in Recipe. And yes, it is necessary to have the curly braces or else it will come up undefined
	- the curlies are an example of destructuring
#### Setting up your first react project
- reference this lesson for using vite to get a devleopment up and running quickly 
- 

#### Markdown stuff
- `<hr/>` - this is a thematic break between paragraphs like a change of scenary or something paints a line at the point can have attributes like size and whether it has shade or not
- `<article/>` - is a logical section of text that is a whole as a blurb. can exist independent of other text on the site and should be able to be separated and not detract from its purpose or meaning as a result
#### CSS attributes in JSX
- if you for example return an element in a component and want to add style attributes to it, you can: 
	- in the attributes: `style={{display: 'none'}}` double braces with the value as a string

#### Keys
- keys are needed by the internal workings of react to keep track of what is what incase the elements are rearranged or removed and need to be rendered in an altered way. the keys associate the particular element from its siblings
#### Props
- properties that are passed down from the parent to the children. 
- it is only one direction, from parent to child 
- Props are immutable and only way for them to change is to get different props from the parent component. the component itself cannot modify its own props
- They look like html attributes but you can pass any javascript object through arrays, objects, and functions
- Prop destructuring allows you a concise way of passing multiple props to a component to then render elements. see in this example how text, color, font params are mapped to the values in the app():
```jsx
function Button({ text, color, fontSize }) {
  const buttonStyle = {
    color: color,
    fontSize: fontSize + "px"
  };

  return <button style={buttonStyle}>{text}</button>;
}

export default function App() {
  return (
    <div>
      <Button text="Click Me!" color="blue" fontSize={12} />
      <Button text="Don't Click Me!" color="red" fontSize={12} />
      <Button text="Click Me!" color="blue" fontSize={20} />
    </div>
  );
}

```

- default props: if there is some data or props that are going to be the same in multiple elements you can save yourself from repetition by making default props so you dont have to enter them each time. see: 
```jsx

function Button({ text, color, fontSize }) {
  const buttonStyle = {
    color: color,
    fontSize: fontSize + "px"
  };

  return <button style={buttonStyle}>{text}</button>;
}

Button.defaultProps = {
  text: "Click Me!",
  color: "blue",
  fontSize: 12
};

export default function App() {
  return (
    <div>
      <Button />
      <Button text="Don't Click Me!" color="red" />
      <Button fontSize={20} />
    </div>
  );
}

```
- notice here the syntax of .defaultProps

- you can also pass a function through as a prop for example if your child is a button the button will take the prop function and call it 
- There is something called currying that looks like a callback function is called and then does some shit idk looks like you can call hella shit at the same time from a return statement or something here is more on it: https://javascript.info/currying-partials I just cant rn
- you can also use the spread operator to avoid having to list out all the props that you are passing to your components: 
```jsx
export default function example(props){
	return (
		<Hello {...props} />
	);
}
```
- absolute legend I think there

- look here for more on passing jsx in a children prop: https://react.dev/learn/passing-props-to-a-component
#### State in React
- simple definition is that sta te is the data and the result of the data being manipulated
- In one moment you might have a state in your machine or program that will be different if you have processes that dynamically change the state of the data
	- examples of this could be incrementing value on an integer during runtime.
	- or could be user interactions with your components that dynamically cause changes in the elements being rendered
- In order for components to behave dynamically, it needs to remember things about itsself
- State is local to each instance of the componenet on the screen so if you have three copies of the same component, changin the sate of one will not affect the state of the others
##### using state in functional components
- functional components (components made out of strict functions) have to use imported useState method from react in order to have a modifiable state
- This useState method is known as the useState Hook
```jsx
const [stateValue, setStateValue] = useState(initialValue);

// adapted for our use case:
const [backgroundColor, setBackgroundColor] = useState(initialColor);

```
 - seen is the destructuring syntax to initialize backgroundcolor and a function. the useState hook returns an array with an initial value that will set the initial state value. 
 - second thing you initialize there is a function that will be used to update the state
###### how does it work under the hood?
- whenever a state or prop changes, the whole component must rerender which involves destroying itself including the variables and functions and react nodes. 
	- the useState value will return the latest state value
- react reconcilliation algorithm - rerendering generates a virtual dom and compares with the actual dom to see what is the minimal amount of processing that it needs to do in order to update it. 
##### Hooks
- special functions that allow us to use react features
- they are only available while react is rendering
- recognizable by the `use` prefix as in `useState` 
	- They can only be called from the top level of a functional component
	- Hooks cannot be called from inside loops or conditions
- Why do you need the hook?
	- because a regular local variable will not persist or be paid attention to by react between renders
	- it also will not trigger the rerender
	- so the useState hook both retains the information and will trigger the rerender
- **when you should not use hooks**:
	- if you need to store data in a single function call then just use regular variables and not hooks
	- hooks are only meant to remember data *between renders* if your logic needs a variable only in the context of a single function scope, then a regular variable will work just fine
##### Rendering components in React
- What happens when react is rendering your components?
	- on an initial render you would have to use react render utils to create a root element and render the target dom node
	- subsequent renders are triggered by updates to the state by the set function hooks. 
	- initial renders call the root component and subsequent ones call the function component whose state triggered a rerender
##### Structuring state and managing it: 
- you should never modify the state value directly: 
	- primitive types(passed by value: int, bools) are already immutable
	- reference types(arrays, objects) should never directly be mutated
		- use setState: `const newPerson = {...person, age: person.age + 1};` then `setPerson(newPerson)` 
		- as opposed to `person.age = person.age + 1; setPerson(person) `
- Principles of structuring state: 
	1. **group related state**
	2. **avoid contradictions in state** - two states that communicate different states of the same thing i.e message sent, can lead to a state is sending to true and a isSent to true, aka impossible states. better to have one state that holds the "sending" , "sent" , "typing"
	3. **avoid redudant state** - if you calculate data from props and store in state, thats redundant and unnecessary i.e fname, lname, and fullname state 
		- same goes for mirroring a prop. state var initialized to prop. if prop changes the state will not get updated
	4. **avoid duplication** if you same data replicated in multiple state variables, hard to sync
	5. **avoid deeply nested state** - not efficient and hard to update
##### States and the rendering cycle
1. Initial state values are put on a "shelf"  by react
2. user button (set)  triggers react to update a state on the shelf
3.  React then re-render the component pulling the updated shelf value
*important to note that everytime you have a set func it will rerender*
##### sharing state between two components
when you want a state between two components to always change together if for example they will both use a state that each of them needs to have an updated version you would actually drop the state from both components and then add it as a state to the closest parent of both of them and then pass to each of them as propl its known as *lifting state up*
- what is an example of sharing state or syncing it?
	- if you have a parent component that calls two instances of panels for food recipes, and you can click the show button to reveal the recipe
	- not sharing state would be each recipe's canShow state exist independent of each other and neither the other panel nor the parent component could control the canShow state in any of the panels
	- sharing state would entail removing the state from each of the components and instead managing the state in the parent in a way where it could control which child component has what and is passed the values needed as props
		- it needs: 
			- state as props
			- management variable or state in parent
			- function as prop to update state
- what is an uncontrolled state vs controlled state?
	- controlled state is when you have parent managing the state for each of the children components
	- uncontrolled state is when each component manages its own state and cannot be controlled by parent
- what does it mean to have a single source of truth?
	- not that all states should live in one place, but that all states live in a specific component and not shared amongst components. if multiple components need it, it should be uplift by the parent and passes as props instead

### Dealing with Side Effects
- A side effect is when your react component needs to reach out beyond the component and states and access or sync with something outside like an API server call or changing where the component is located in the DOM.
- in order to interact with the outside world you might use another hook `useEffect()` which will help to run code outside your component. 
- for example in a timer function that counts up every second and update the state count, you would have beserk behavior because of the fact that everytime state is updated the component re-renders and creates a new instance of this counter intervals and will not keep track. `useEffect()` along with some arguments helps to stop the code inside the hook from creating new instances. 
###### Component life cycle vs Effect life cycle: 
- component: 
1. mounting - when the component is added to the screen, it is mounted
2. updating - when either a state or a prop changes, usually in response to user interaction
3. umountaing - when it's removed from the screen
- Effect :
1. synchronizing - your effect function will define what it looks like to synchronize
2. stop synchronizing - the clean up function returned by the effect function will define when to stop synchronizing

questions:
- what triggers the clean up function to stop synchronization?
	- if passing a new prop and thus rendering doesnt affect the effect function what will trigger the effect to call the clean up function? 
#### using UseEffect hook 
##### syntax
##### use dependencies 
###### what needs to be included in dependencies
- all variables that are inside the component body, that are rendered by props or state are *reactive*. and if they're reactive and used by the useEffect, they will need to be in the dependencies array
