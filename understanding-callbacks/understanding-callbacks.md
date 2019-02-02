# Understanding Callbacks

Callbacks seem to be a sticking point for people new to programming. Put simply, callbacks are functions that are passed into another function as a parameter. With the many ways one can define a funciton in JavaScript, it's no wonder why callbacks get confusing.


## Anatomy of a Function

JavaScript has many ways of defining a funciton, but they all follow a similar pattern and have the same pieces, they just look differently. There is more technical terminology surrounding functions, but we are going to gloss over them for now. ( If you are interested, feel free to look up "Function Declarations" and "Function Expressions" ).

### Normal Functions (Named Functions)

Normal functions, are something you will see everywhere in JavaScript. Understanding the anatomy of these will help you understand all the other types of functions.

~~~javascript
function funkyFunction(music, isWhiteBoy) {
  if (isWhiteBoy) {
    console.log('Play: ' +  music);
  }
}
~~~

This is actually called a function declaration and is broken into a few parts.

1. The `function` keyword
  * This tells the JavaScript compiler you are making a named function
2. The name
  * This is the name of the function, and what you will use when you call it. It is also used in stack traces
3. The arguments
  * everything between `(` and `)` is an argument, these must be seperated by commas if there is more than one. There may also be nothing between the `()` if the function does not take any arguments. The paranthesis are required.
4. The function body
  * This is where the function actually does something. This code gets run with whatever values are passed into the parameters.

Calling a function looks similar to declaring it without the `function` keyword and the body. One passes it the values you want the parameters to represent.

~~~javascript
funkyFunction('that funky music', true);
~~~

This will print `"Play: that funky music"` in the terminal.

### Anonymous Functions

These are very similar to normal functions, with a few small differences. Anonymous functions are not 'named', and have a few different syntaxes. Even though they cannot have a name, they can be assigned to a variable (a function expression). Even though you can still call these functions if you assign them to a variable, they are not the same as a decleration. Anonymous functions can still be used without assinging them to a variable by passing them into other functions as a `callback`.
(Which will become more clear later).

Each of the functions below are identical to the funkyFunction above in how they are called and work. 

~~~javascript
// This example is still an anonymous function even though we used the `function` keyword. It doesn't have a name.
const funkyFunction = function(music, isWhiteBoy) {
  if (isWhiteBoy) {
    console.log('Play: ' +  music);
  }
}
~~~

~~~javascript
// This is called an arrow function, we'll get into these soon.
const funkyFunction = (music, isWhiteBoy) => {
  if (isWhiteBoy) {
    console.log('Play: ' +  music);
  }
}
~~~

An anonymous function is just a function that does not have a name, this doesn't mean that it cannot be called. Each of the above functions can be called exactly the same way:

~~~javascript
funkyFunction('that funky music', true);
~~~

#### Arrow Functions

These are just a shorter way to write a function. They do have some special rules however, and understanding the rules imposed by arrow functions will help you understand callbacks.  

* If there is only one argument, the `()` can be ommitted
* if arrow functions are one line, the brackets `{}` can be omitted.
  * When omitting the brackets, the arrow function returns the evulated expression. (The result of the calculation)

All the functions below are identical

~~~javascript
const playThe = (funky) => {
  return funky + " music";
}

const playThe = funky => {
  return funky + " music";
}

const playThe = funky => funky + " music";

// You can call these functions like: `playThe('blues')`
~~~

Below are some examples of an arrow function wtihout an argument (These functions are all identical as well). Notice the `()` in place of any named arguments 

~~~javascript
const playThat = () => "funky music";

const playThat = () => { return "funky music"; }

const playThat = () => {
  return "funky music";
}
~~~

### Key Point

Notice how all the functions above have a very similar order of things? The only large difference is the syntax, but each of them have a very similar structure. The biggest exception being the named funcitons vs anonymous functions.

## What Callbacks Look Like

You may have seen callbacks and not realized it. They are used frequently in JavaScript and it is very difficult to read JavaScript without understanding them. Below is an example you may have seen before.

~~~javascript
const notes = ['do', 'ray', 'me'];

notes.forEach((note) => console.log(note));
~~~

This is the `forEach` array method. This method simply takes a `callback` function as it's argument. (Don't forget that `forEach` is a function itself).

There are many other ways to do the same thing (as is tradition in JavaScript), below are a few more ways to write this code:

~~~javascript
const notes = ['do', 'ray', 'me'];

notes.forEach((note) => { 
  console.log(note);
});

notes.forEach(function(note) {
  console.log(note); 
});

// This one is tricky, but will make more sense later
notes.forEach(console.log); 
~~~

## How Callbacks Work

To state it once more: Callbacks are just functions passed into other functions as arguments (as a parameter).

### Iterator Functions

Below is what `forEach` might look like under the hood, notice it calls the `callback` function each time it loops over an item.

~~~javascript
function myForEach(array, callback) {
  for (let i = 0; i < array.length -1; i++) {
    callback(array[i]); // This is when the callback function gets called, or executed
  }
}

// You would call it like this:
const myArry = [2, 3, 4, 2];
myForEach(myArry, (item) => {
  console.log(item + 2); 
})
~~~

> WOAH, hold up. Where did `item` come from? 

This came from the function `myForEach` calling the callback with an argument. The line with `callback(array[i])` is calling the callback function, which we defined inline as an anonymous function. Below are more examples of how this could be called.

~~~javascript
const myArry = [2, 3, 4, 2];

myForEach(myArry, item => console.log(item + 2)); // We do not need the `()` in this case, as we only have one argument

myForEach(myArry, function(item) {  // We can pass arguments to this kind of anonymous function as well
  console.log(item + 2) 
});

function printItemPlusTwo(item) {
  console.log(item + 2);
}

myForEach(myArry, printItemPlusTwo); // `item` is passed into the funciton, we do not need to declare it here because we declared it elsewhere. It is the same as the 'console.log' example above except we decalred our own function.

~~~

Another good example of how callbacks work might be the `.map` method (read more on MDN), below is one way it might be implemented.

~~~javascript
function myMap(array, callback) {
  const myNewArray = [];

  for (let i = 0; i < array.length - 1; i++) {
    const callbackResult = callback(array[i]);
    myNewArray.push(callbackResult); 
  }

  return myNewArray;
}


// This could be called like this:
const addedArray = myMap([1, 2, 3], (arrayNum) => {
  return arrayNum + 2; 
});


// OR
const addedArray = myMap([1, 2, 3], (arrayNum) => arrayNum + 2)
~~~

### Event Listeners (DOM)

Event listeners in JavaScript seem to be confusing to people, but after understanding callbacks, these should be a lot easier to understand. 

let's review what they look like, see if you can pick out the parts of them.

~~~javascript
const element = document.querySelector("#myId");
element.addEventListener('click', (event) => {
  // Do something
});
~~~

If you notice, the second argument (value you pass into a funciton) to `addEventListener` is a function. In this case it's an anonymous arrow funciton. This piece of code could be written like this and behave identically.

~~~javascript
const element = document.querySelector("#myId");
element.addEventListener('click', function(event) {
  // Do something
});
~~~

Part of what confuses people is the `event` object. Where does it come from? How does it get there? 

This event object is passed into the callback function by the `.addEventListener` function. A function is calling another function.

This is because.... Callbacks are just functions passed into another function.

That means we can declare a function outside of the argument list and just add it by name as well. Like so:

~~~javascript
function myEventHandler(event) {
  // do something, probably with 'event'
}

const element = document.querySelector("#myId");
element.addEventListener('click', myEventHandler);
~~~

Notice how we didn't 'call' the function called `myEventHandler`? If we were to call it inside the parameter list, the function we called `myEventHandler` would run immediately and give the `addEventListener` the result of calling that function. (in this case, it would be undefined)

## Conclusion

Callbacks are an important part of JavaScript, they are vital to understand, even with the onset of promises and async/await. Callbacks get called by another funciton, so you don't have to call them in the arguments, ( Calling a function is using a function's name and adding `()` to the end of it, like `console.log()` )

These are something that you will learn if you give yourself time, understanding how they work will make your JavaScript carrier a lot easier!

