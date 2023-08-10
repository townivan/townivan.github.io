# JavaScript: Event Listeners

When using regular JavaScript, sometimes known as vanilla JavaScript, don't write your event listeners like this:

```js
<button class="btn" onclick="myFunction()">mybtn</button>
```

The two main reasons (there are others) for avoiding this are:

1. It restricts you to a single event type for that element.  In the above example you would only be able to have one 'click' event.
2. It makes a global event handler which can easily overwrite or be overwritten by later code.

Better to use .addEventListener

Let's say we have a basic button in our HTML.

```js
<button class="btn">mybtn</button>
```

```js
// basic anonymous function which passes the event object (the only allowed param)
const btn = document.querySelector('.btn');
btn.addEventListener('click', function(e){
    console.log(e);  // e.target and e.currentTarget are useful properties of e
});
```

```js
// basic arrow function which passes the event object (the only allowed param)
const btn = document.querySelector('.btn');
btn.addEventListener('click', e => {
    console.log(e); 
});
```

```js
// better to use the selector/method/event pattern (best for being able to remove an eventListener later)
const btn = document.querySelector('.btn');
btn.addEventListener('click', myFunction1);

function myFunction1(e){
    console.log('welcome to myFunction1()...')
    console.log(e)
    e.preventDefault(); // optional to stop the event from bubbling (doesn't work if passive mode is activated... see below)
}
```

```js
// what about passing parameters?  Wrap it in a function
const btn = document.querySelector('.btn');
btn.addEventListener('click', (e)=>{myFunction2(e, 'lalala')});

function myFunction2(e, input1){
    console.log('welcome to myFunction2...')
    console.log(e)
    console.log('input1:', input1)
}
```

If you are dynamically adding buttons, you have to add an event listener event each time you create the DOM element... **OR** you can use event delegation to watch for events than happen on a parent...



```js
<div class="parent">
    <button class="btn">mybtn</button>
</div>

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



