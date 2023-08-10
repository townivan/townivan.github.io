---
tags: JavaScript
---

# JavaScript: Event Listeners

When using regular JavaScript, sometimes known as vanilla JavaScript, don't write your event listeners like this:

```html
<button class="btn" onclick="myFunction()">mybtn</button>
```

The two main reasons (there are others) for avoiding this are:

1. It restricts you to a single event type for that element.  In the above example you would only be able to have one 'click' event.
2. It makes a global event handler which can easily overwrite existing code or be overwritten by later code.

Better to use .addEventListener

Let's say we have a basic button in our HTML.

```html
<button class="btn">mybtn</button>
```

**NOTE:** .addEventListener automatically returns the event object when it triggers.  This is often assigned to a variable 'e' by developers.

If you console.log the event object you will see a lot of useful information about your triggered event.  The most useful are:

1. e.target
2. e.currentTarget

e.currentTarget always refers to the element to which the event handler has been attached, as opposed to e.target, which identifies the element on which the event occurred and which may be its descendant.

A basic anonymous function:

```js
const btn = document.querySelector('.btn');
btn.addEventListener('click', function(e){
    console.log(e);
});
```

A basic arrow function:

```js
const btn = document.querySelector('.btn');
btn.addEventListener('click', e => {
    console.log(e); 
});
```

**Better than both of those** is to use the selector/method/event pattern below:

```js
const btn = document.querySelector('.btn');
btn.addEventListener('click', myFunction1);

function myFunction1(e){
    console.log('welcome to myFunction1()...')
    console.log(e)
    e.preventDefault(); // optional to stop the event from bubbling
}
```

What about passing parameters?  Wrap it in a function:

```js
const btn = document.querySelector('.btn');
btn.addEventListener('click', (e)=>{myFunction2(e, 'lalala')});

function myFunction2(e, input1){
    console.log('welcome to myFunction2...')
    console.log(e)
    console.log('input1:', input1)
}
```

If you are dynamically adding buttons, you have to add an event listener event each time you create the DOM element... **OR** you can use event delegation to watch for events than happen on a parent...

```html
<div class="parent">
    <button class="btn">mybtn</button>
</div>
```

```js
parent.addEventListener('click', myFunction3);

function myFunction3(e){
    console.log('welcome to myFunction3(e)...')
    console.log('e.target:', e.target)
    console.log('e.currentTarget:', e.currentTarget)
    if (e.target.matches('.btn')) { // a basic selector
        console.log('Clicked our btn:', e.target)
    }
}
```

Special performance note:  If you are using touch or wheel event listeners use *passive* event listeners.  [Learn more](https://developer.chrome.com/en/docs/lighthouse/best-practices/uses-passive-event-listeners/)

```js
const btn = document.querySelector('.btn');
btn.addEventListener('touchstart', myFunction1, {passive: true});
```

## Helpful links on this subject

[https://blog.webdevsimplified.com/2022-01/event-listeners/](https://blog.webdevsimplified.com/2022-01/event-listeners/)

[https://ultimatecourses.com/blog/avoiding-anonymous-javascript-functions](https://ultimatecourses.com/blog/avoiding-anonymous-javascript-functions)

[https://plainenglish.io/blog/passing-arguments-to-event-listeners-in-javascript-1a81bc397ecb](https://plainenglish.io/blog/passing-arguments-to-event-listeners-in-javascript-1a81bc397ecb)

[https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)



