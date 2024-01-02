---
tags: js
---

# js: Spread and Rest

## TLDR snippet!

```js
const pNodeList = document.querySelectorAll('p');
const pArray = [...pNodeList]; // This is spread.  Notice that it lives in an array.

function myProfile(firstName, lastName, ...more) { // This is rest.  Notice that it is a parameter to a function.
  return more; // Any extra received arguments are put into an array that we named 'more'.
}
console.log(myProfile('Ed', 'Smith', 18, 'Male', 'Boxer')); // (3) [18, 'Male', 'Boxer']
```

## TLDR summary

> The three dots in JavaScript indicate either the **spread** or **rest** operator for arrays&mdash;which were introduced in ES6.  
> The **spread syntax** allows an expression to be **expanded in places where multiple arguments are expected**.  
> The **rest parameter** syntax is used for **functions with a variable number of arguments**.  

___

## Examples...

Some of these helpful examples came from [https://hackernoon.com/javascript-cheatsheet-spread-operators](https://hackernoon.com/javascript-cheatsheet-spread-operators)

### 1. string to array - a simple example to illustrate how spread works

```js
const myString = "Here we go!";
const myStringToArray = [...myString];
console.log(myArray); // (11) ['H', 'e', 'r', 'e', ' ', 'w', 'e', ' ', 'g', 'o', '!']
```

### 2. nodelist to array - a VERY common use for spread

querySelectorAll gives you a nodelist, not an array. The common forEach() can iterate that, but map() needs an array.

Often you use map() when you want an entirely new array, and/or you want to chain with filter() and reduce().

```js
let elements = document.querySelectorAll('li');
console.log(elements); // NodeList(5) [li, li, li, li, li]

let elementsArray = [...document.querySelectorAll('li')];
console.log(elementsArray); // (5) [li, li, li, li, li]
```

### 3. concat to an array with spread

```js
const names1 = ['Bill', 'Jill'];
const names2 = ['Pam', 'Sam'];
names1.push(...names2);  // This is spreading an array into a function.  It almost looks like rest.
console.log(names1); // (4) ['Bill', 'Jill', 'Pam', 'Sam']
```

### 4. merge arrays with spread

```js
const names1 = ['Bill', 'Jill'];
const names2 = ['Pam', 'Sam'];
const names3 = [...names1, 'Chuck', ...names2];
console.log(names3); // (5) ['Bill', 'Jill', 'Chuck', 'Pam', 'Sam']
```

### 5. merge objects with spread

```js
const user1 = { name: 'Aaron', age: 11, };
const user2 = { name: 'Barry', dob: "2/2/2022"};
const mergedUsers = {...user1, ...user2};
console.log(JSON.stringify(mergedUsers)); // {"name":"Barry","age":11,"dob":"2/2/2022"}
// Matching properties "update" to the second object.  Non-matching properties are created.
// The order matters, if we had done:
const mergedUsers = {...user2, ...user1};
console.log(JSON.stringify(mergedUsers)); // {"name":"Aaron","dob":"2/2/2022","age":11}
```

### 6. simple array clone* with spread

```js
const names1 = ['Fred', 'Sally'];
const names2 = [...names1];
// common error: "const names2 = names1" merely creates a reference to names1.
```

### 7. Common ES6 style in React to update* an array with spread

Example code here, followed by an explanation.

```js
setTodos(prevTodos => {
    return [...prevTodos, {id: uuidv4(), name: name, complete:false}];
})
```

**Note:** *The spread operator (...) is the tool of choice here, specifically because it creates a NEW array rather than updating the existing array.  This immutability concept is a major part of the functional programming pattern that React uses.

Updating state is achieved by using the `useState` hook in React. (a hook is a built-in React function)

useState returns an array with two items:
the first is a variable that is used to store your state.
the second is an updater function to update that first variable.

In React, you will see the following pattern for a state-based variable:

```js
const [state, setState] = useState(initialState);
```

for example:

```js
const [todos, setTodos] = useState([]);  // passing an initial empty array to useState()
// or
const [count, setCount] = useState(0); // passing an intial 0 to useState()
```
 
Because **useState returns an array**, it's annoying to use something like:

```js
const todos = useState([])[0];
const setTodos = useState([])[1];
// or
const count = useState(0)[0];
const setCount = useState(0)[1]
```

ES6 destructuring makes this easier by automatically assigning array entries to variables:

```js
const [todos, setTodos] = useState([]); 
```

The above gives you two const variables: todos and setTodos.  An array and an updater function.

The same works for saving a state as a simple number:

```js
const [count, setCount] = useState(0); // destructuring.  count=state-saved variable.  setCount=initial value for that variable.
```

The above gives you two const variables: count and setCount.  A variable and an updater function.
See: [https://react.dev/reference/react/useState](https://react.dev/reference/react/useState)

```js
const [todos, setTodos] = useState([]); // destructuring.  todos=state-saved array of objects.  setTodos=function to modify that array.
```

So, how is this related to ES6 spread operator?

The updater function can receive the next state directly **OR** a function which calculates it from the previous state.  

Here is an example.  

```js
setTodos(prevTodos => {
    return [...prevTodos, {id: uuidv4(), name: name, complete:false}];
})
```

In the above, we are:

1. Updating based on the current state.  (adding a new entry to the array of objects)
2. Since our update is based on the current state, we pass a function which does that work to the updater function.
3. Making that function concise by using an arrow function.
4. Using spread to make the update even more concise&mdash;without modifying the original array.

The return statement is returning an array.  Notice the starting and ending brackets [].

The return statement is using the spread operator (...) to create a new array that is the previous array with a new entry appended to it.

I'm sure you are wondering about that `uuidv4()` function.  It's just a way to use the nifty guid generation thing in JS.  (React wants unique ids in collections of data)

```js
function uuidv4(){
    return self.crypto.randomUUID();
}
```

## Helpful links on this subject

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

[https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID)


