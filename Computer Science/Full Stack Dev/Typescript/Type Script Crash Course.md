typescript docs: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any
**parking lot:**
type
interface
string / number / boolean
arrays
object types
optional properties (?)
union types (|)
function parameter/return types
type inference


### Type by Inference
- much of typescript is javascript but smarter. it gives your variables a type without explicity giving a type to primitives
```ts
const hello = "hello world!" // :string

```

### interface
- for user defined types and objects, you can make an interface to define what the objects types should be
```ts
interface User {
name: string;
id: number;
}
const user: User {
name: "Hayes,
id: 0,
}
```
- You can also use classes like below: 
```ts
interface User {

name: string;

id: number;

}

class UserAccount {

name: string;

id: number;

constructor(name: string, id: number) {

this.name = name;

this.id = id;

}

}

const user: User = new UserAccount("Murphy", 1);
```

- in functions, this is how you would use interfaces to define parameter types and expected return values
```ts
function deleteUser(user: User) {

// ... parameter of type User

}

function getAdminUser(): User {

//... assuming return value of type User

}
```

### Additional primitive types
- Typescript along with js primitives like boolean, int, etc has a few noteworthy types; 
	- `any` , 
	- `unkown`
	- `never`
	- `void`
- these are all helpful for defining interfaces 

### Composing Types: Unions
- User defined type by joining other primitives
	- `type MyBool = true | false;`
	- this is a type that is basically a boolean
- helpful usecase: 
```ts
type WindowStates = "open" | "closed" | "minimized";

type LockStates = "locked" | "unlocked";

type PositiveOddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```
- You can also use unions to handle different types: 
```ts
function wrapInArray(obj: string | string[]) {

if (typeof obj === "string") {

return [obj];

(parameter) obj: string

}

return obj;

}
```
- if a string then return string, if array, return the array
### Composing Types: Generics
- generics allow arrays to have types instead of allowing anything in there
```ts
type StringArray = Array<string>;

type NumberArray = Array<number>;

type ObjectWithNameArray = Array<{ name: string }>;
```
- more generics in user defined objects
```ts
interface Backpack<Type> {

add: (obj: Type) => void;

get: () => Type;

}

// This line is a shortcut to tell TypeScript there is a

// constant called `backpack`, and to not worry about where it came from.

declare const backpack: Backpack<string>;

// object is a string, because we declared it above as the variable part of Backpack.

const object = backpack.get();

// Since the backpack variable is a string, you can't pass a number to the add function.

backpack.add(23);

Argument of type 'number' is not assignable to parameter of type 'string'.
```


### Typescript's Structured Type system
- it appears to be flexible in accepting objects that have more than what is defined, and just takes what fits. for example: 
```ts
interface Point {

x: number;

y: number;

}

function logPoint(p: Point) {

console.log(`${p.x}, ${p.y}`);

}


const point = { x: 12, y: 26 };
logPoint(point);
// logs "12, 26"

// notice here that point was never declared as a Point type, yet it takes what fits

const point3 = { x: 12, y: 26, z: 89 };

logPoint(point3); // logs "12, 26"

const rect = { x: 33, y: 3, width: 30, height: 80 };

logPoint(rect); // logs "33, 3"

const color = { hex: "#187ABF" };

logPoint(color);

Argument of type '{ hex: string; }' is not assignable to parameter of type 'Point'. Type '{ hex: string; }' is missing the following properties from type 'Point': x, y
```

### Narrowing
- roughly narrowing is when you have multiple types as parameters and you have a function with a union with some function that for example only accepts one of those types, typescripts type guard analysis will detect that you're trying to pass a parameter that has potential to not work in a used function. prevents future bugs. for example: 
```ts
function padLeft(padding: number | string, input: string): string {

if (typeof padding === "number") {

return " ".repeat(padding) + input;

}

return padding + input;
```
- above .repeat(number) is a string method that returns the string its attached it n number of times. becuase you pass a union, TS is smart enough to see that's an issue. 