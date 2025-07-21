##### parking lot: 
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
- what is the error when you try to use array.map()? "array.map() is not a function"
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
###### rendering array of list items
- take a look at this elegancy: 
```jsx
export default function List() {
  const listItems = people.map(person =>
    <li key={person.id}>
      <img
        src={getImageUrl(person)}
        alt={person.name}
      />
      <p>
        <b>{person.name}:</b>
        {' ' + person.profession + ' '}
        known for {person.accomplishment}
      </p>
    </li>
  );
  return (
    <article>
      <h1>Scientists</h1>
      <ul>{listItems}</ul>
    </article>
  );
}
```
- notice that the return statement has `<ul>{array}</ul>` here the html is being automatically generated for the list items because in the `listItems` variable, the li was mapped to each array item. what this results in is a list of html li elements. react is smart enough to automatically populate the list items in the return line inside the `<ul>` element without the need to run a for-loop
	- notice that to make this possible, the mapping needs to include the html for react to recognize it. and the array variable needs to be wrapped in the curly braces. /css/

#### Setting up your first react project
- go into the folder where projects are and: 
- `npm create vite@laest Project-Name-React -- --template react` 
- then CD into the project folder and run `npm install` and that is literally it. super easy. 
- hit `npm run dev` to launch the local site by clicking on the link in the terminal
##### adding your react project to your github repo
if you follow the above instructions will create a local repo but will not actually be tracked by either a local or remote git repo. complete the following steps to get your new vite react project up and running with git and github: 
- in your project directory hit: `git init -b main`
- then `git add . && git commit -m "First commit"`
- then using github cli (additional appliction needed for remote) : `gh repo create`
	- *note* github cli requires authorization token generated by your gh account, google ("token authorization for gh cli")
- follow all interactive cli prompts and you should be good to go!

#### Markdown stuff
- `<hr/>` - this is a thematic break between paragraphs like a change of scenary or something paints a line at the point can have attributes like size and whether it has shade or not
- `<article/>` - is a logical section of text that is a whole as a blurb. can exist independent of other text on the site and should be able to be separated and not detract from its purpose or meaning as a result
#### CSS attributes in JSX
- if you for example return an element in a component and want to add style attributes to it, you can: 
	- in the attributes: `style={{display: 'none'}}` double braces with the value as a string

#### Keys
- keys are needed by the internal workings of react to keep track of what is what in a list incase the elements are rearranged or removed and need to be rendered in an altered way. the keys associate the particular element from its siblings
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
- There is something called currying that looks like a callback function is called and then does some shit idk looks like you can call hella shit at the same time from a return statement or something here is more on it: https://javascript.info/currying-partials I just cant rn - revisited but dont see the point of currying at this point. practical use cases might be limited for this. 
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
- simple definition is that state is the data and the result of the data being manipulated
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

##### Rapid state updates
- due to the nature of how states update, if you have an app that is frequently trying to access and update state in consequetive and rapid re-renders, you might encounter issues with state values being outdated or incorrect. you will have to use a callback function to ensure that you have the state value at the time it was enqueued: 
```jsx

const handleSubmit = (e) => {
    e.preventDefault();
    setTodos((todo) => [...todo, inputVal]);
    setInputVal("");
  };
```
- notice here instead of `[...todos, inputVal]` you have the call back function
- see here for more: https://react.dev/learn/queueing-a-series-of-state-updates
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
- *note* : for api calls you'll need to hide your api key from where the code base is hosted. you'll need to create an environment variable. under vite: 
	- create a file in your root directory called `.env`
	- name your environment starting with `VITE_` ie: `VITE_SOMEKEY = 123`
	- then in your react component you can access your variable like so: 
		- `const apiKey = import.meta.env.VITE_SOME_KEY`
	- you can now pass your key throughout your project and not worry about it leaking online. a
We've talked about this idea of having pure functions meaning that your functions a) always return the same output for the same input and b) do not modify or mutate data outiside your function. 
	- At times however, something in your project needs to change as is what makes programming interesting, bringing about interesting changes such as dynamic user interface from interactions on your webpage. 
	- Reacts paradigm assumes all functions are pure functions and especially during rendering, all functions must be pure functions to ensure that react applications are safe to run on servers and scale appropriately. 
	- when a function needs to mutate something such as the dom or synchronizing with outside state or api fetches, React will handle that process separately after rendering asynchronously.
	- UseEffect is one such example of asynchronous hooks that allow you to process or generate data outside the component. 



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
	- what is useSelectoptions and how might it be useful in reducing code repetition?
- not a question but you should review the lifecycle of effect: https://react.dev/learn/lifecycle-of-reactive-effects, https://react.dev/learn/you-might-not-need-an-effect, https://dmitripavlutin.com/react-useeffect-infinite-loop/ and make sure that you understand all of the nuances of the code in here
- understand thoroughly the instances when you do need a useEffect and when you do not: 
	- be able to accurately determine in different circumstances why you might need or not need the useEffect
- what is the limit for too many states? is it for things that could be calculated during the render?
#### using UseEffect hook 

##### syntax
##### use dependencies 
###### what needs to be included in dependencies
- all variables that are inside the component body, that are rendered by props or state are *reactive*. and if they're reactive and used by the useEffect, they will need to be in the dependencies array
- a linter will complain if you have variables in your useEffect that are declared inside your component and are not in your dependencies. this is because all variables declared inside the component are reactive. 
	- if you would not want to include them as dependencies, i.e you dont want it to synchronize on those variables, then you can put the variable declarations either outside the component or inside the useEffect function call since it wont be reactive to re-renders.
###### life cycle of a component and useEffect:
useEffect is a combination of the following methods from class components: 
- `componentDidMount` `componentDidUpdate` and `componentWillUnmount`
- its 1. mounting,  2. re-render, 3. right before it unmounts
n
  - having a depency araray, the useeffect will trigger on intiial render and if the variable changesin dependency array changes. 
- leaving a useEffect with an empty dependency array would be the same thing as 1. only triggering when it mounts the component
- useEffect with dependency array ommitted is the same thing as 1 & 2 because it will re-run every time that 
- And 3 is the clean up function that runs right before the component is being unmounted and removed from the screen
  - having a depency array, the useeffect will trigger on intiial render and if the variable in dependency array changes. 
- see here more a visual on the lifecycle of react components: https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram//
###### what is the commit phase?
- the "commit phase" is after react has checked for difference in the components and works with the DOM to make updates and when the side effects are run. 
- this is where the 'componentDidMount()', componentdidupdate and componentwillunmount will run. synonomous with useEffect() in functional components
#### avoiding using useEffect when not needed
- if you have data you need to transform before it is rendered, you do not need to use an effect to track the change of the data and then apply the transformaiton. what will happen is react renders the screen and then applies the effect actions that will cause a state to change and thus rerender the component which is inefficient
	- instead you should keep all your data transformation at the top of the component. that will be run quicker and before the rendering begins and it will regnerate the data transformations every time that your component renders again
- There might exist some conditions where you have expensive process that you need to process not on every render but when some of the variables involved in the process change. instead of using a useEffect which is code smell (because it is processed with props or states and not somethig external) and should instead cache the expensive result in a memoization (useMemo) which will only run when one of the dependent variables has changed instead of on each render. 
```jsx
import { useMemo, useState } from 'react';

function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState('');
  // ✅ Does not re-run getFilteredTodos() unless todos or filter change
  const visibleTodos = useMemo(() => getFilteredTodos(todos, filter), [todos, filter]);
  // ...
}
```
- important to note that useMemo should only ever be used with pure functions meaning that a function component that accesses a global variable and increments would result in a different answer for multiple jsx calls. creates unpredictable results. I think it also needs to be a pure function because the useMemo runs during rendering, and react does not allow impure functions during rendering your components. 
	- instead you should pass your component the variable as a prop so that the value is controlled outside of it so that every time that function is called it will result in the same predictable behavior according to the value passed as prop. 
	- You can however mutate locally declared variables, these are the components little secret and does not modify anything outside of it. 
###### how to know if your calculation is expensive
- unelss youre creating or iterating over thousands of objects, it's probably not expensive. 
- You can test by adding `console.time() console.timeEnd()` to measure the time it takes to perform a calculation
	- if It's adding up considerably after testing your inputs then probably memoize it
```jsx
console.time('filter array');  

const visibleTodos = getFilteredTodos(todos, filter);  

console.timeEnd('filter array');
```
##### changing all state values a prop change
- by default react will want to preserve state values when different props are passed this might not be wanted if the state pertains only to the prop that was previously passed
	- the solution to this is to pass a key to each component related to the prop so that react treats it as a different component and thus not fetch the same state values. 
```jsx
export default function ProfilePage({ userId }) {  

return (  
<Profile  
userId={userId}  
key={userId}  
/>  
	);  
}  

function Profile({ userId }) {  
// ✅ This and any other state below will reset on key change automatically  
const [comment, setComment] = useState('');  
}
```
- notice here how a key is passed to the child component that will make react treat each of instance of that as a seperate component that will not share any state betweeen them. this is a good way of preventing some state values to cross over when parent states change like userid to prevent you accidentally being able to post something under someone elses account. 
##### changing some state values when a prop changes
- sometimes you might not want to change all of the state values but some of them. 
- see the example from the react docs on avoiding useEffect:

- essentially what you can do is store the current state that you want to change and then on a prop change , you check during rendering if the state being pulled is different than the one passed by the prop and then if it is you run the setState hook to change the state to a null or whatever you need it to be. 
	- this is a more efficient way of changine only some states based on changning props but its actually not the best solution. the best solution involves not having to update the state at all and instead calculating and storing the state you needed to change on a prop in a regular local variable: 
```jsx
function List({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selectedId, setSelectedId] = useState(null);
  // ✅ Best: Calculate everything during rendering
  const selection = items.find(item => item.id === selectedId) ?? null;
  // ...
}
```
- here instead the selectedid is stored in state and the actual list item is calculated during rendering by seeing if the id is found in the new list prop and if its not then the current listem set to null and presumably other code in the component would have logic to set the updated id and list item
##### UseEffect and event handlers
- you should not use useEffect hooks for user interactions such as click or other events. those should be only event handlers
- useEffect should be used for when the purpose of the code running because the component has displayed or rendered. 
	- the difference event handlers run code because there was a click event, not because the page was loaded or component rendered
	- an example of appropriate use of effect would be sending an analytics report when the component mounts.
	- direct quote from react docs: `When you choose whether to put some logic into an event handler or an Effect, the main question you need to answer is _what kind of logic_ it is from the user’s perspective. If this logic is caused by a particular interaction, keep it in the event handler. If it’s caused by the user _seeing_ the component on the screen, keep it in the Effect.`
##### other considerations
- avoid useEffects that are triggered by other state changing
- on initializing the application if you need to use global variables for example if something only needs to render or run once you can accomplish this by setting a global variable and checking the variable in the component so you have more control over how many times that will get run.
	- for this make sure that you keep this pattern to a minimum and only in the entry point of your app or where the app.js root component is
- race conditions - when two different things are racing and arrive back at different times than you expected. This happens with data fetching 
- `useRef` this one is a reference hook that allows you to increment from the component without having to rerender the component for example on tracker a counter for each change in input form: 
```jsx
import { useState, useRef } from 'react';  

  

function CountInputChanges() {  

const [value, setValue] = useState('');  

const countRef = useRef(0);  

  

const onChange = ({ target }) => {  

setValue(target.value);  

countRef.current++;  

};  

  

return (  

<div>  

<input type="text" value={value} onChange={onChange} />  

<div>Number of changes: {countRef.current}</div>  

</div>  

);  

}
```
- this is opposed to say using a useEffect and having the dependency be the value state when the value state changes. this would be more effificient because it eliminates the need to rerender another time. 
- avoid objects as dependencies because javascript objects do not have strict equality since they compare by reference and they will never point to the same blocks of memory
- if you must use objects, you can use the accessors to make sure that the actual depency its checking is a primitive data type and not an object
###### putting parameters of state for setters
look at this code: 

```jsx
import { useEffect, useState } from "react";  

  

function CountSecrets() {  

const [secret, setSecret] = useState({ value: "", countSecrets: 0 });  

  

useEffect(() => {  

if (secret.value === 'secret') {  

setSecret(s => ({...s, countSecrets: s.countSecrets + 1}));  
// see the s here the s is secret state
}  

}, [secret]);  

  

const onChange = ({ target }) => {  

setSecret(s => ({ ...s, value: target.value }));  

};  

  

return (  

<div>  

<input type="text" value={secret.value} onChange={onChange} />  

<div>Number of secrets: {secret.countSecrets}</div>  

</div>  

);  

}
```
- notice that the useEffect callbackfn has parameter s which represents secret state variable. by why doesn't it just call for secrets instead of this new parameter declaration?
	- In react when you use the state setter function you can pass either a new state value or a callback function. Reach will automatically call this function with the current state as its argument. 
	- this ensures that you always working with the latest state which is really important with updates being asynchronous and all
	- **the use of the callback function has benefits over setting value directly**
		- has something to do with making sure that you have the most up to date state values.. not too sure what they mean by this. I think it has something to do with the code below and making sure you get the most up to date state even when they're right after one another #NeedMoreHelp 
```jsx
setSecret({ ...secret, value: "first" });
setSecret({ ...secret, countSecrets: secret.countSecrets + 1 });
// here setting directly, the second set call will use the original state value at render time instead of the updated state from the first set call
```
**definitely review this often because this seems like a big pattern with React that will be helpful and avoid headaches**
- check this article if I'm having infinite loops and lop through and see if one ofhtem looks like the sin commited: https://dmitripavlutin.com/react-useeffect-infinite-loop/

#### Class Components
- most use functional but incase legacy code bases are encountered we should be familiar with class components: 
```jsx
import React, { Component } from "react";

class ClassInput extends Component {
  constructor(props) {
    super(props);

    this.state = {
      todos: [],
      inputVal: "",
    };

    this.handleInputChange = this.handleInputChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleInputChange(e) {
    this.setState((state) => ({
      ...state,
      inputVal: e.target.value,
    }));
  }

  handleSubmit(e) {
    e.preventDefault();
    this.setState((state) => ({
      todos: state.todos.concat(state.inputVal),
      inputVal: "",
    }));
  }

  render() {
    return (
      <section>
        <h3>{this.props.name}</h3>
        <form onSubmit={this.handleSubmit}>
          <label htmlFor="task-entry">Enter a task: </label>
          <input
            type="text"
            name="task-entry"
            value={this.state.inputVal}
            onChange={this.handleInputChange}
          />
          <button type="submit">Submit</button>
        </form>
        <h4>All the tasks!</h4>
        <ul>
          {this.state.todos.map((todo) => (
            <li key={todo}>{todo}</li>
          ))}
        </ul>
      </section>
    );
  }
}

export default ClassInput;

```
- start with the class constructor, remember that in c++ you need a class constructor as well, here you will declare the states and you have to bind the functions declared here to the 'this' keyword
- more on the class components and constructors: https://react.dev/reference/react/Component#constructor
for class component hooks, see: https://www.theodinproject.com/lessons/node-path-react-new-component-lifecycle-methods
#### React Testing
- since we're using Vite for the build environment instead of using JEST, we'll use Vitest and also tools from the react testing library
##### Getting started
- get a vite-react environment going
- then `npm install vitest --save-dev`
- then add `"test": "vitest",` in package.json file under "scripts" and below "build"
- then `npm install jsdom --save-dev` so that vitest will work with html inside of 
- then add to vite.config.js: (right below "plugins")
```js
  test: {
    environment: 'jsdom',
  },
```
- then install react testing library: `npm install @testing-library/react @testing-library/jest-dom --save-dev`
- for the rest see this site: https://www.robinwieruch.de/vitest-react-testing-library/
- at the very end, make sure to install: `npm install @testing-library/user-event --save-dev`
*parking lot:*
- what are assertions in testing? also known as custom matchers?
- what is a container in reference to testing using the testing library
- why do you need to destructure render in order to get it, and sometimes you do not?
	- you access the container by destructure if you need compare a snapshot of the whole component. in earlier examples of vitest testing, only compared the heading, container is for comparing the whole component to make sure there isnt a side effect causing the component to render differently on subsequent re-renders
- What are test ids? why does it seem they are used when we cannot find an appropriate query method?
- what circumstances call for using mocks in tests? what role do the mocks play in those circumsstances and why are they necessary? are there alternatives?
	- see this site to review how mocking helps with components with multiple child components you dont want to test: https://medium.com/@taylormclean15/jest-testing-mocking-child-components-to-make-your-unit-tests-more-concise-18691ef6a0c2
##### conventions of Vitest: 
- `describe()` test suite
- `it()` test cases
- `expect().toBe()` assertions

##### conventions of React Testing Library:
- it starts with a describe() to define what youre testing and it() for what it should do. inside the it():
	- render the component in order to select an element from it usiing the render() with the component inside of it
	- once you render you have to query what youre going to evaluate. then you use assertions `expect().toBe()` to match the query with some expected result to compare against

**what does it mean to query?**
to Query are methods of selecting different elements in a rendered component. there are different ways you can query these rendered components, however there are specific guidelines on how you should do it: 
- if you need query a specific element like a heading, button, form etc, use `screen` object as imported by: `import {render, screen} from "@testing-library/react"` 
- if you need to query a whole component incase you need to do a snapshot, you need to destructure the `render` object to get the main DOM node of your component.
	- *snapshot* - used to check for errors in your component mounting and rendering. checks to make sure that it renders the same thing in atleast two attempts incase side effects are leading to different renders. 
###### queries
- methos that testing library gives you to find elements on the page. types of queries include:
	- get: `getBy`
	- find `findBy`
	- query `queryBy`
- you should prioritize using `getByRole`  along with a `name` option because it queries most everything from mouse interactions to events triggered by assistive technology. if it doesnt work for you, then your UI might be unaccessible. 
	- ex: `getByRole('button', {name: /submit/i})`
- single element selectors: `getBy...`
	- `queryBy`
	- `findBy` return promise that resolves when elemnt is found that matches or time out after 1000ms
		- combination of `getBy` and `waitFor` they accept waitfor options: `await screen.findByText('text', queryOptions, waitForOptions)`
- multiple: `getAllBy`
	- `queryAllBy`
	- `findAllBy`
see here for more on specifics: https://testing-library.com/docs/queries/about/#priority
- avoid using the container element to query for rendered elements!
- see the whole list of queries: https://testing-library.com/docs/dom-testing-library/cheatsheet/
##### simulating user events
- provided by the react testing library is the screen object which contains all the necessary query methods. its the preferred way to accessing the query methods as opposed to trying to destruct the render object for the query methods. 
- in the library `import userEvent from "@testing-library/user-event` you get the `userEvent` object that requires `user = userEvent.setup()` scoped inside your `it("test pass description", ()=>{})` call back function that will need to be an async function 
- you will then `await user.click(button)` so you can match the result 
```jsx
  it("renders radical rhinos after button click", async () => {
    const user = userEvent.setup();

    render(<App />);
    const button = screen.getByRole("button", {name: "Click Me"});

    await user.click(button);

    expect(screen.getByRole("heading").textContent).toMatch(/radical rhinos/i);
  });
});
```
##### On avoiding testing for implementation
- testing implementation details leads to either a false positive or a false negative
- testing for implementation could mean: 
	- if youre testing an application for result of state value being 1, but then you change the state to an array of numbers to allow for multiple at the same time. the function and behavior of the app has not changed but the implementation details have changed. your test would then break and give you a false negative. your functions and app work just fine but your tests are broken because you refactored them. 
	- he simple definition of implementation  details are the things that the end user will not interact with, use, see, or know about. 
	- tests should only see/interact wtih the props passed and the rendered output because the people that are going to be using are the end users interacting with buttons and developers that add content to the website
- I think the point is that you should aim to test what outcomes should be visible to user based on tested userinteractions as opposed to testing an internal variable or state value 
	- perhaps if you find yourself wanting to test a state, then ask yourself how does that state pertain to something the user would interact/see? then instead test that thing
#### Mocking callbacks and components
**what is mocking?** - mocking is when you have functionality in your tests that mimicks whatever it is its mocking. review from [[Intermediate Javascript#More Testing]]
```jsx
it("should call the onClick function when clicked", async () => {
    const onClick = vi.fn();
    const user = userEvent.setup()
    render(<CustomButton onClick={onClick} />);

    const button = screen.getByRole("button", { name: "Click me" });

    await user.click(button);

    expect(onClick).toHaveBeenCalled();
  });

  it("should not call the onClick function when it isn't clicked", async () => {
    const onClick = vi.fn();
    render(<CustomButton onClick={onClick} />);

    expect(onClick).not.toHaveBeenCalled();
  });

```
- here the callback  function is being mocked that either the function was called or it was not called
	- I thought that testing should not involve details that the end users would not interact with or see( i.e the user will not interact with the callback function so why is that being tested)
###### what is act() and what does it offer for those using useEffect and useState for testing?
its wraps your tests that involve a side effect or state updates to make sure that it waits for any updates or setters to complete before it runs any of the assertions. here is a site that illustrates this: https://github.com/mrdulin/react-act-examples/blob/master/sync.md
- look to see where in the odin project they use act and see how its used in context and then reference this guide on what it means when working on testing async functions

##### Vi
- vi imported from vitest is what is primarily used for mocking complex components that import modules, have side effects, async callbacks etc. 
- must be in EMS and not common js imports
###### vi.mock
- substitutes alll imported modules from provided path

## The React Ecosystem

### Type checking with react PropTypes
Why type checking?
	- ensures that you using the correct data in built applications and helps to catch bugs with passing the wrong kind of data. making sure your components are getting the correct type of data
##### getting started: 
- [ ] install npm package to project directory: `npm install --save prop-types`
- inside your file: `import propTypes from 'prop-types;`
##### syntax
```jsx
import React from 'react';
import PropTypes from 'prop-types';

const RenderName = (props) => {
  return <div>{props.name}</div>;
};

RenderName.propTypes = {
  name: PropTypes.string,
};

RenderName.defaultProps = {
  name: 'Zach',
};

export default RenderName;

```
- notice here the use of 'componentName.propTypes' with an object notation declaring that RenderName component expects a prop called 'name' that is a string type
- also notice the option of listing a default prop values just like you might do inline declaring props
- more details on setting prop types and defining it: https://blog.logrocket.com/validate-react-props-proptypes/
### React Router
- what does it mean when you're talking about routing?
	- up this point we have been building single page applications but that changes as your application gets bigger. there is a difference between server based routing which means every link on a page you click is handled by the server requesting that page and clearing everything , and refreshing everything on the page with what you requested. html is quick to load but style sheets and images can get cached which drastically reduces load times and stutters when the resources are shared between links clicked. 
	- there is another option for larger application where its still a single page application with something called client side routing. 
	- routing and specifically *client-side routing* is when javascript will intercept a request from clicking a link and loads/changes what is needed to be changed without having to refresh the page and having the server load a different page. 
	- you'll still see the url change but the page wont have to reload
	- one thing to know for accessibility: refreshing the page like a multi-page application does tells screen readers when there is new content to read. since with CSR you wont get refresh, you need to use the library tools to manually tell screen readers that there is new content to read. 
- What is the big deal with Client side routing with "SPA" or single page appications and why is it what makes reacts promise of "dynamic user interactions", "lightning fast load times" a reality? 
	- *dynmic user interactions:*
	- *lightning fast load-times:* 
*parking lot:*
-  what is an `<Outlet />` component and what is it used for? what results is it supposed to bring it about if a compent has children components that is meant to be rendered as well?

visual of setting up react routers and how to set up navigation and nesting routes and outlet
#### getting started
##### syntax
`npm install react-router-dom`

- client side routing is enabled by creating a `Router` and linking/submitting to pages with `Link` and `<Form>` 
```jsx
import * as React from "react";
import { createRoot } from "react-dom/client";
import {
	createBrowserRouter,
	RouterProvider,
	Route,
	Link,
} from "react-router-dom";

const router = createBrowserRouter([
	{
		path: "/",
		element: (
			<div>
				<h1>Hello world</h1>
				<Link to="about">About Us</Link>
			</div>
		),
	},
	{
		path: "about",
		element: <div>About</div>,
	},
]);

createRoot(document.getElementById("root")).render(
	<RouterProvider router={router} />
);
```
- notice here the use of `createBrowserRouter` to define the possible routes by creating the configuration for a router that can be altered to needs. accepts array of routes. 
	- you can also define as nested components but in reactrouter v6, they recommend adding routes as objects as seen here. 
- notice the `<RouterProvider />` component that will actually channel the defined routes by passing through the above router object.
- finally notice the `<Link />` component that is used instead of `<a href>` that would be used in a server router
- this will render a basic page with a link to an about div

#### Nested Routes
- the general idea is component hierarchy and data is tied to segments of the url:
	- ex: <Books /> -> <BookLayout /> -> 1
		- `localhost3000/books/booklayout/1`
	- good visual on the routing and component hierarchy relationship: https://remix.run/_docs/routing
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import App from "./App";
import Profile from "./Profile";
import Spinach from "./Spinach";
import Popeye from "./Popeye";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "profile",
    element: <Profile />,
    children: [
      { path: "spinach", element: <Spinach /> },
      { path: "popeye", element: <Popeye /> },
    ],
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);

```
- notice here the use of children key with array of children with their own required path and element arguments
- running this would not actually present those two children. if yollu wanted to render the children alongside with the parent object, you would need to make use of the `Outlet` object from `react-router-dom`
```jsx
import { Outlet } from "react-router-dom";

const Profile = () => {
  return (
    <div>
      <h1>Hello from profile page!</h1>
      <p>So, how are you?</p>
      <hr />
      <h2>The profile visited is here:</h2>
      <Outlet />
    </div>
  );
};

export default Profile;
```
- notice on the parent component Profile, you place the `<Outlet />` object where the children are supposed to be rendered when the route is selected. 
	- *notice* you will need logic that naviates to the respective children with `Link` components
- you can also make one of the children render automatically by setting one of them as `index: true` so its a default profile
```jsx
const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "profile",
    element: <Profile />,
    children: [
      { index: true, element: <DefaultProfile /> },
      { path: "spinach", element: <Spinach /> },
      { path: "popeye", element: <Popeye /> },
    ],
  },
]);
```
- notice the first child, the path argument replaced with `index: true` . again this will make it so that that element will render as default along with the parent component
##### Dynamic Segments
- This is when react will take the url and try to "match" during runtime with the available routes. react takes the url "parameter" and feeds it for the path specified as dynamic by the `:variableName`. for example if you have `localhost3000/profile/hello` and you have a path route: `path="/profile/:name"` then from the profile componet, you can use the `useParams` hook to get access to that parameter passed to the URL and render components dynamically based on that: 
```jsx
import { useParams } from "react-router-dom";
import DefaultProfile from "./DefaultProfile";
import Spinach from "./Spinach";
import Popeye from "./Popeye";

const Profile = () => {
  const { name } = useParams();

  return (
    <div>
      <h1>Hello from profile page!</h1>
      <p>So, how are you?</p>
      <hr />
      <h2>The profile visited is here:</h2>
      {name === "popeye" ? (
        <Popeye />
      ) : name === "spinach" ? (
        <Spinach />
      ) : (
        <DefaultProfile />
      )}
    </div>
  );
};

export default Profile;
```
- notice here the deconstrutor for the useParams(); and then you can put logic that reads its content
- here is what the route configuration would look like to accept dynamic routes: 
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import App from "./App";
import Profile from "./Profile";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
  {
    path: "profile/:name",
    element: <Profile />,
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```
- notice the `:name` after the path name 
###### React routers Matching algorithm
- You can run into the problem where you might have pass a url that has the same name as a specified path and also have a path that accepts dynamic names. technically react router could match with both of the paths because the dynamic one will accept and match with any parameter.
- for example if you have url: `localhost3000/profile/new` and you have the routes: 
	- `path="/profile/:name"`
	- `path="/profile/new"` 
- luckily there is an algorithm that works off of specificity like css selectors where it will know if you have a specified path of the same name and choose that one as the matcher for the component
##### Handling bad URLs
- in the config for the router, you can handle unfound pages with `errorElement: <ErrorPage />` added after the element argument
##### passing props through outlets
- in order to pass props to children of a parent component that has the `<Outlet />` component, you need to use something called `context`. this is something that will be gone into more depth but for now, the Outlet component accepts context prop: `<Outlet context={[count, setCount]} />` then you can use the `const [count, setCount] = useOutletContext()` in the child component after importing with `import {useOutletContext} from "react-router-dom"` 
- here is more information on that: https://reactrouter.com/en/main/hooks/use-outlet-context

##### Authorization protected routes
- when authentication is needed from a user account for a specific path, you can embed conditional rendering based on user data such as if they're logged in or not. this involves rerouting the user to a different URL programmatically using the `<Navigate />` component. 
- see this link for more:https://www.geeksforgeeks.org/navigate-component-in-react-router/ 
```js
//navigate component
import { Navigate } from 'react-router-dom';

function ProtectedRoute({ user }) {
  if (!user) {
    return <Navigate to="/login" replace />;
  }

  return <Dashboard />;
```
**Navigate component vs the useNavigate hook**
- when you need to navigate programmatically for example because an event such as a form submitting, use the useNavigate hook from 'react-router-dom'
- when you are trying to redirect in component logic flow such conditional rendering, Navigate component is the way to go. 
```js
//use Navigate hook
import { useNavigate } from 'react-router-dom';

function MyComponent() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/dashboard'); // navigate to /dashboard
  };

  return <button onClick={handleClick}>Go to Dashboard</button>;
}

```
###### how to achieve protected routes with react
- this is for using a restful api as serverside authorization of users. 
- it starts with having an Authorization component wrapper. This is essentially a wrapper component that uses useContext api as a way to manage user, token, login state and functions. This Authorization wrapper accepts component children or even an entire Router so that all your routes have the option of accessing these states and fns. 
```js
import { useState, createContext, useEffect } from 'react'

export const Authorization = createContext();

export function AuthProvider({ children }) {
  const [token, setToken] = useState(localStorage.getItem("token" || ""));
  const [user, setUser] = useState(null);
  const [mode, setMode] = useState("");
  const [loading, setLoading] = useState(false)
  const [error, setError] = useState(null)

  useEffect(() => {
    // store token in ls
    localStorage.setItem("token", token);
  }, [token]);

  // login function sets token and sets user

  // will need to import the url from login 
  const login = async (url, data) => {
    
  }

  // return the context provider with the children in the middle if no loading or error
  return (
      <Authorization.Provider value={{ user, mode, setToken, login }}>
        {!loading && children}
      </Authorization.Provider>
  )
}
```
then you might have a component that wraps a route that is supposed to be protected: 
```js

```

##### Loaders
- loaders in react router is a function that is run and completed *prior* to your component rendering. inside the component that expects it, you can import `useLoaderData` from react-router-dom and `const data = useLoaderData()` to access it. 
- 
#### Fetching Data and Error Handling in REACT
```jsx
import { useEffect, useState } from "react";

const Image = () => {
  const [imageURL, setImageURL] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
      .then((response) => response.json())
      .then((response) => setImageURL(response[0].url))
      .catch((error) => console.error(error));
  }, []);

  return (
    imageURL && (
      <>
        <h1>An image</h1>
        <img src={imageURL} alt={"placeholder text"} />
      </>
    )
  );
};

export default Image;
```
- notice here the use of the null in the url so that the component conditionally renders the response of the fetch if the useEffect hook was successful. this makes the conditional rendering of the image url alot more clear based on the success of the fetch. 
- this does not however communicate anything to the end user if and when you dont get a correct response. for that look at: 
```jsx
useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
    .then((response) => {
      if (response.status >= 400) {
        throw new Error("server error");
      }
      return response.json();
    })
    .then((response) => setImageURL(response[0].url))
    .catch((error) => setError(error));
}, []);
```
- notice the setError for the state error initialized to null that will relay information to user if the respose was not good: 
```jsx
if (error) return <p>A network error was encountered</p>

return (
  imageURL && (
    <>
      <h1>An image</h1>
      <img src={imageURL} alt={"placeholder text"} />
    </>
  )
);
```
- the check for error placed right before the return on the image component to ensure that it wont try to render an incorrect response once the side effect runs
##### Custom Hooks
```jsx
import { useState, useEffect } from "react";

const useImageURL = () => {
  const [imageURL, setImageURL] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
      .then((response) => {
        if (response.status >= 400) {
          throw new Error("server error");
        }
        return response.json();
      })
      .then((response) => setImageURL(response[0].url))
      .catch((error) => setError(error))
      .finally(() => setLoading(false));
  }, []);

  return { imageURL, error, loading };
};

const Image = () => {
  const { imageURL, error, loading } = useImageURL();

  if (loading) return <p>Loading...</p>;
  if (error) return <p>A network error was encountered</p>;

  return (
    <>
      <h1>An image</h1>
      <img src={imageURL} alt={"placeholder text"} />
    </>
  );
};
```
- rewriting the name of the function to have use infront of it somehow allows you to call it in other places and for testing like another react hook. not really seeing why you couldnt just callit it whatver and call it from other places regardless. 
*minimum states for data fetching*
- in react, best practices mandate that each data fetch somes with three mandatory minimum states to have a good user experience: data, loading, error
- good site to review async api fetching with react: https://blog.logrocket.com/modern-api-data-fetching-methods-react/
###### fetching to the server
```js
fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({})
});
```
- when you need to make a post request from an api, you will need to modify the fetch options such as method, changing the headers, and including the payload in the body. Dont forget to stringify it with json first. 
##### multiple fetches and race conditions
- in an event where there are multiple rapid fetches in a side effect called due to user interactions, there is a possibility that fetches requested after another could finish its reponse before hand, due to the nature of how fetches to servers can be unpredicatble and unreliable. this could lead to unexpected and undesired inconsistencies in the UI
- the solution to this is to use an `AbortController`
##### Data fetching and performance
good article on performance and rendering strategies with fetches in react: https://www.developerway.com/posts/how-to-fetch-data-in-react
review this and take notes on it

#### Styling React Apps
##### CSS Modules
useful guide on getting started with modules: https://www.makeuseof.com/react-components-css-modules-style/
- what css modules do is they package the css file and scope it locally so you can avoid local name clashes for css variables. 
###### getting started with css modules
- vite should have compatibility right out of the box. you'll need to organize your components into folders with the jsx component file and a .module.css file. 
- example component: 
```jsx
import styles from "./button.module.css";

export default function Button() {
	return (
		<button className={styles.btn}>Submit</button>
	);
}
```
then in the button.module.css file: 
```jsx
.btn {
	witdh: 90px;
	padding; 10px 20 px;
	border-radius: 10px;
}
```
- notice here the class name in the component is `styles.btn` which takes from the object styles object and then with a dot notation will get the selector and apply it. 
###### Dynamic classnames
- you can use composition to share styles accross different components in different folders or even combine classes so you can extend from classes already declared or even have a central colors.module.css file in the component root folder and pull the color from there. see the article from above for more. 
##### CSS in JS
https://styled-components.com/

due to the virtue of building strong foundations, I should be using CSS modules or css in JS as oppossed to a CSS framework or component library

another article looking over the many libraries of js in css and gives valuable insight into how js in css operates https://css-tricks.com/a-thorough-analysis-of-css-in-js/

- there are two options for declaring styles in your componnet files, tagged template and object styles
	- tagged template is template string literal where you can interpolate dynamic strings with variables into the css property values. uses kabob case just like regular css
	- object styles you use came case and access the css object properties as seen in this article: https://css-tricks.com/a-thorough-analysis-of-css-in-js/ (same as right above)
- The best option for js in css would be styled-components. read through their docs when getting started
- here is an article on how to get the most out of styled-components: https://www.joshwcomeau.com/css/styled-components/
##### css in js vs css modules
- modules are more performant especially when looking at much bigger applications because it has a separate css file that can be cached by the browser while css in js relies on js to inject css into the dom which cannot be cached and could cause perfomance issues with bigger applications
- css in jss gives you the ability for truly dyanmic styling as it's javascript and conditional styling and all the power that comes with js comes with it. css modules are separate css files and you wrwite them in there so you dont have the same range of dynamic abilities. 
\
#### managing state with the context api
outside of using `outlet` component and the usecontext hook, you can access state from other components using the context api 

##### getting started: 
- `import { createContext } from "react";` 
```jsx
import { useState, createContext } from "react";

const shopContext = createContext({
	products: [],
	cartItems: [],
	addTocart: () => {},
});

export default function App() {
  const [cartItems, setCartItems] = useState([
    /* List of Items in Cart */
  ]);
  const products = /* some custom hook that fetches products and returns the fetched products */

  const addToCart = () => {
    // add to cart logic (this adds to cartItems)
  };

  return (
    /* We are going to pass the things that we want to inject to these components using the value prop */
    /* This value prop will overwrite the default value */
    <ShopContext.Provider value={{ cartItems, products, addToCart }}>
      <Header />
      <ProductDetail />
    </ShopContext.Provider>
  );
}
```
core consists of three components: 
1. createContext - takes number, string, object, as seen here, an object that contains arrays, functions etc
2. shopContext.Provider - here we call the component from the name of the context created and wrap the componets that will have access to the things in the createContext. this is what provides the the contexts values to the components no matter how deeply nested they are
3. useContext - in the compents that need access to the context values, you will need to import the useContext from react and deconstruct the values you need from the context as seen below
```jsx
import { useContext } from "react";
// import for ShopContext

export default function ProductDetail() {
  const { products, addToCart } = useContext(ShopContext);
  const product = products.find(/* Logic to find the specific product */);

  return (
    <div>
      {/* Image of the product */}
      <div>
        {/* elements that align with the design */}
        <button type="button" onClick={() => addToCart(product)}>
          Add to Cart
        </button>
      </div>
    </div>
  );
}
```
- notice that you're deconstructing here
- *something of note:* useContext() is not useful in the component where the `<context.Provider>` in the same component. The provider needs to be above the component that is calling useContext().

##### Drawbacks of using the context api
1. performance issues - when updating the state in a context it can cause all the components that are consuming that context to re-render as well even if the state that they are using is not changed. since the object would be updated, that would include the unchanged state that's nevertheless a part of the object that is modified. 
2. code readbility- important to keep code base organzed and minimize nested compents as it could get easy to lose track of all the components that are using your context since there isnt a define limit on how deeply nested a component can be in order to access the context. 
###### possible solutions: 
- use smaller contexts instead of a large one in specific logical categories to limit how often the context object needs to be changed and limit thus the amount of times that components need to render unnecessarily
- another alterative is the react component composition. see this article: https://www.robinwieruch.de/react-component-composition/
- other libraries such as Zustand and Redux but recommend to stick with context api for the rest of the curriculum
- see the react references for the specifics on getting around the shortcomings: https://react.dev/reference/react/useContext * also complete this lesson bc I skipped it basically*
- also this one come back to it: https://kentcdodds.com/blog/prop-drilling

### Reducing state
 - the `useReducer` hook from react allows you to nest more complicated state logic wherein you feed it a function called a reducer that has a switch block with different ways that a state value can be manipulated. 
	 - you also feed it an initial value. 
	 - it will return an array with the current state and the dispatch function. the dispatch takes a `type: value` argument that acts as the action or block in your switch statement to trigger. 
	 - behaves very similarly to state and will not update on the next render with the calling of the dispatch function. 
	 - uses the Object.is() in order to compare if the state has changed. and if its not different, it will not re-render.
```jsx
function reducer(state, action) {
  switch (action.type) {
    case "incremented_count": {
      return { count: state.count + 1 };
    }
    case "decremented_count": {
      return { count: state.count - 1 };
    }
    case "set_count": {
      return { count: action.value };
    }
    default: {
      throw new Error("unknown action: " + action.type);
    }
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });

function handleClick() {
  dispatch({ type: "incremented_count" });
}

```
- here the reducer function is defined and is passed as argument to the useReducer hook along with the orginal value of the count.
	- notice here that the initial value comes in the form of an object. as its an object, you can place other important values inhere like an id, a text value, etc. see the react docs on reducer to see how its implemented
- to use the reducer, you call the dispatch function 
- *note:* reducers must be pure functions, no arguments passed can be modified in the reducers
	- your changes occur in what is returned, you can modify an object or array in place and return that object `return {...todos, id: 0]`
- actions should describe a single user interaction even if that single interaction involves changes in the state in multiple places. (ie. 'reset' instead of five 'setfield' actions that describe how reset is achieved)

##### reducers vs state
its use is by preference, they offer the same performance however there are some considerations to make: 
- reducers take more coding upfront at the trade off of clearer less bloated code when you have really complex state updates that are updating the same state in many different places, and it makes it easier to test and debug complex state logic with reducers
###### initial state functions
- useReducer allows you a third argument that is an initial state function incase your initial state relies on a loop or something with longer computation and relies on a function to be made, y ou do not want that as your initial state becuase it will be re computing that on ever render. that's what the third argument can fix: 
```jsx
function createInitialState(username) {
  const initialTodos = [];
  for (let i = 0; i < 50; i++) {
    initialTodos.push({
      id: i,
      text: username + "'s task #" + (i + 1)
    });
  }
  return {
    draft: '',
    todos: initialTodos,
  };
}

export default function TodoList({ username }) {
  const [state, dispatch] = useReducer(
    reducer,
    username,
    createInitialState
  );
  return (
    <>
      <input
        value={state.draft}
        onChange={e => {
          dispatch({
            type: 'changed_draft',
            nextDraft: e.target.value
          })
        }}
      />
// notice that i left out the rest of the function as its not pertinent
```
you'll see here that the third argument in the initialization of the useReducer is the function that is 

### Refs and Memoization
#### useRef hook
- this is the solution to not being able to use query selector to change class names and the likes, such as changing text content. this is in direct opposition to using something like document.queryselector to hold reference to elements on the page. here is a good article on using useRef for the many ways that you can use web api such as queryselector and getelementbyid : https://www.meje.dev/blog/useref-not-queryselector
- here is an article on the many use cases for useRef beside the usual of getting reference to elements inthe dom this article is essential and notes should be taken  https://overreacted.io/making-setinterval-declarative-with-react-hooks/
```jsx
import { useRef, useEffect } from "react";

function ButtonComponent() {
  const buttonRef = useRef(null);

  useEffect(() => {
    buttonRef.current.focus();
  }, []);

  return <button ref={buttonRef}>Click Me!</button>;
}
```
- after importing from react, you use the useRef() and initialize to null
- this is meant to focus on the button as soon as the page loads so a useEffect is handy for this 
- attach a ref{} prop to your component which will connect to the useRef()
- useRefs do **not** trigger rerenders! good to know
react docs on the useRef hook: https://react.dev/reference/react/useRef\
- *note* do not use useRef for displaying any information because of the fact it does not cause a re-render of react components. If you need to display anything, you need to use a state variable. 
	- another note is that you should not read a ref during rendering or write to it.
	- you can however read or write refs in event handlers or in useeffect 
- make sure to refer to the react docs for troubleshooting

#### useMemo hook
this is used to cache a longer computation: 
```jsx
import { useMemo } from "react";

function Cart({ products }) {
  const totalPrice = useMemo(() => {
    return products.reduce(
      (total, product) => total + product.price * product.quantity,
      0
    );
  }, [products]);

  return (
    <div>
      {/* Some other content in the cart */}
      {/* Products to display */}
      <p>
        Total Price: <strong>${totalPrice}</strong>
      </p>
      {/* Some button to checkout */}
    </div>
  );
}

```
- the syntax for useMemo is the same as the syntax for useEffect
- *useMemo* should really only be used when it is absolutely needed. 
- useMemo will have expensive calculations from repeating unless the dependencies change but is the useMemo is used to update a state and there is expensive calculations in the children components, that will not stop the component from re-rendering because the state update will re-render children components. to solve this there is also memo function that you can wrap an expensive component that actually will prevent the component *if the props in the component have not changed* . 
	- this component will be prevented even if the parent is re-rendering. pretty cool. see example: 
```jsx
import React, { useState, memo } from "react";

const ButtonComponent = memo(({ children, onClick }) => {
  let i = 0;
  let j = 0;
  const ITERATION_COUNT = 10_000;
  while (i < ITERATION_COUNT) {
    while (j < ITERATION_COUNT) {
      j += 1;
    }
    i += 1;
    j = 0;
  }

  return (
    <button type="button" onClick={onClick}>
      {children}
    </button>
  );
});

```
- notice here the component ButtonComponent wrapped in the `memo()`

##### Difference between useMemo and useCallback
- they are both very similar expect that useCallback is only for caching functions and useMemo is for everything. 
- while useMemo you need an anonomous function invocation and then placing your function inside of it(if you wish to cache a function call) useCallback does not need the additional arrow function: 
```jsx
import { useCallback } from "react";

// Inside a component
// Without useCallback
const handleClick = () => setCount((prevState) => prevState + 1);
// With useCallback
const handleClick = useCallback(
  () => setCount((prevState) => prevState + 1),
  []
);
// or
const memoizedHandleClick = useCallback(handleClick, []);
```
- notice that its just a function call and the desired function to cache inside of it, and of course the dependency array after it. 
- use between this and useMemo is largely down to preference but I should know the difference for an interview question
##### When to use either
- optimizations come at a cost. only use if you need to make direct comparasions for referential comparisons of non-primitive data types such as objects and functions 
- another use case is when you have a very computationally expensive calculation
- see this article for more on tips of examples for the the two usecases I mentioned here: https://kentcdodds.com/blog/usememo-and-usecallback

### React references
- see this lesson to see useful links to stay connected what is happening with react and where you should be going after this: https://www.theodinproject.com/lessons/node-path-react-conclusion
- 

#### React with RESTful API
- when you have react client, you will need to fetch from your server api that could be deployed on local host or on an actual Paas service. Your react app needs to be able to distinguish between accessing the api url depending on the environment its in. 
	- solution: make a .env.development and .env.production file (separate) that react will pick to use depending on if you use `npm start` or `npm run build`
		- `npm start` - .env.development 
		- `npm run build` - .env.production  

#### modularization
- in effort to speed up production I will be adding to npm or git a collection of frequent reused components that can be imported and used in other projects: 
###### components
- form  
- input made up of a label and input element just pass props
- navigation button - made up of use navigation and button 
- not found router component - meant to catch all paths not specified in the router definition, with `"*"` 
- error boundary - takes error object and handles all excpetions during run time (not for user validation)
###### utility functions
		
- fetch utlity function - abstracts all the header processes 



### test 
this is a test to make sure obsidian is syncing with github
