---
tags: js
---

# js: Debounce simplified

## TLDR snippet!

```js
const debounce = (mainFunction, delay) => {
    // Declare a variable called 'timer' to store the timer ID
    let timer;

    // Return an anonymous function that takes in any number of arguments
    return function (...args) {
        // Clear the previous timer to prevent the execution of 'mainFunction'
        clearTimeout(timer);

        // Set a new timer that will execute 'mainFunction' after the specified delay
        timer = setTimeout(() => {
            mainFunction(...args);
        }, delay);
    };
};
```

___

## Using wrapping function with debounce

Using a debounce function can be confusing at first.  Especially when you see a mix of function declarations and function expressions.

In case you need some background.  Debouncing is a method for avoiding "over-clicking" and only make one function call.

You choose a delay, let's say 2 seconds.  Once the first click happens, the timer begins.  Until the 2 seconds ends, any additional click will cancel the previously scheduled click and restart the timer.


```js
// Define a function called 'searchData' that logs a message to the console
function searchData() {
    console.log("searchData executed");
}

// Create a new debounced version of the 'searchData' function with a delay of 3000 milliseconds (3 seconds)
const debouncedSearchData = debounce(searchData, 3000);

// Call the debounced version of 'searchData'
debouncedSearchData();
```

The debounced version of your function is the only one that is a function expression.  (saving a function to a variable)

You can get arrow-function style debounce functions, but I think the example at the top is easiest for understanding how they essentially work.

## Throttle vs. Debounce

These techniques are similar.  Simply put, both help you postpone and reduce the rate of some execution. Assuming you are calling decorated functions returned by throttle/debounce repeatedly...

- Throttle: the original function will be called at most once per specified period.
- Debounce: the original function will be called after the caller stops calling the decorated function after a specified period.

## Helpful links on this subject

[https://dev.to/jeetvora331/javascript-debounce-easiest-explanation--29hc](https://dev.to/jeetvora331/javascript-debounce-easiest-explanation--29hc)
