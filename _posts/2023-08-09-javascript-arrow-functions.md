---
tags: js
---

# js: Arrow functions

This is your basic JavaScript function.  It's a "function declaration".

```javascript
function yell(msg){
    return msg.toUpperCase();
}
```

The other type of function is called a "function expression", where you save the function into a variable.

```javascript
const yell = function(msg){
    return msg.toUpperCase();
}
```

Both of these will work with "arrow functions" which were introduced into JavaScript with ES6.  (If you don't need to support IE11, you can use ES6 based JavaScript)

It's good to understand arrow functions because many online code examples will assume that you do.

Let's learn about these by considering how to work with an array.

```javascript
const names = ['Ben', 'Sue', 'Reed', 'Johnny'];
```

We could loop through this array using the forEach() array method:

```javascript
names.forEach(function(){});
```

Notice how it's an entire function being passed as the argument to the forEach() method.

Also notice that the function doesn't have a name.  It's an anonymous function.  Now let's expand it to make is more readable.

```javascript
names.forEach(function(){
    // do stuff here.
});
```

Looping over an array is only useful if we can access each entry in the array, so we make up a some temporary variable to do that.

```javascript
names.forEach(function(name){
    console.log('the name is:', name);
});
// the name is: Ben
// the name is: Sue
// the name is: Reed
// the name is: Johnny
```
Often it's helpful to add another variable to keep track of which index of the array we are working on.

The forEach() array method provides that as the optional second argument.  Just provide a second variable name to get the index.

```javascript
names.forEach(function(name,i){
    console.log('the name at index ' + i + ' is: ' + name);
});
// the name at index 0 is: Ben
// the name at index 1 is: Sue
// the name at index 2 is: Reed
// the name at index 3 is: Johnny
```

## Arrow function syntax

1. remove the keyword 'function' from the left side of the ()
2. add a 'fat arrow' => to the right side of the ()

```javascript
names.forEach(function(){}); // becomes...
```

```javascript
names.forEach(()=>{}); // everything else remains the same.
```

```javascript
names.forEach((name,i) => {
    console.log('the name at index ' + i + ' is: ' + name);
});
```

if you don't need more than a single parameter, you also don't need the parenthesis around the parameter...

```javascript
names.forEach(name => {
    console.log('the name is: ' + name);
});
```

Often arrow functions allow you to write a simple one-liner.  When you do that, you can even get rid of the extra {}

```javascript
names.forEach(name => console.log('the name is: ' + name));
```

Also no extra `;` at the end of a statement on the right side of the arrow.

```javascript
names.forEach(name => console.log('the name is: ' + name);); // wrong!
```
```javascript
names.forEach(name => console.log('the name is: ' + name));  // right!
```

## So, other than shorter syntax, why bother using an arrow function?

### Reason 1: Implict returns

Very often functions are built to return some computed value.  A one-line arrow function assumes this, allowing you to skip writing a 'return' line.

This is more relevant with iteration methods that expect a return, like .map()

```javascript
let newNames = names.map((name,i) => name+'_NEW' ); // map() loops through an array and RETURNS a new array.
console.log(newNames)
// (4) ['Ben_NEW', 'Sue_NEW', 'Reed_NEW', 'Johnny_NEW']
```

### Reason 2: Arrow functions don't change 'this'

```javascript
const btn = document.querySelector('.btn');

btn.addEventListener('click', function(){
    console.log(this); // <button class="btn">mybtn</button>
});

btn.addEventListener('click', () => {
    console.log(this); // Window {window: Window, self: Window, document: document, name: '', location: Location, …}
});
```

In Javascript the `this` keyword is always a reference to the object that called the function.

An ordinary function rebinds `this`.  An anonymouse function (arrow function) doesn't.

The confusion around using `this` IMO is best avoided by not trying to force JS to work in the Object-oriented programming (OOP) paradigm with classes.  
