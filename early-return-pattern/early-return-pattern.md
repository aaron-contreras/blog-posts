# Early Return Pattern

People new to programming sometimes struggle to understand returning early inside a function. Especially if they come from a language like Ruby, which has implicit returns. Today we're going to explore what an early return is, and what it can be used for in the context of JavaScript.

## Understanding `return`

To understand what an early return is, you must first understand what `return` does in a function. Put simply, `return` returns a value from the function, it could be anything. In JavaScript you can return anything from a string, to an object, and even another function. When a `return` statement has been found, the function ends immediately and return's the value to whatever called the funciton.

~~~javascript
function timesTwo(x) {
  return x * 2;
}

console.log(timesTwo(21));
~~~

In this example you would expect `42` to be logged to the console, and you'd be correct. The `timesTwo` function returned the result of `x * 2` to `console.log`, and `console.log` printed the value to the console.


## Early Returns

An early return is a `return` statement that is placed before some other code has been run.

~~~javascript
function notFunkyFunction() {
  console.log('... And just when, it hit me, somebody turned around and shouted:')
  return
  console.log('Play that funky music white boy');
}

notFunkyFunction();
~~~

This function will only log `'... And just when, it hit me, somebody turned around and shouted:'` and will never log `'Play that funky music white boy'` due to the `return` statement. Using this, we can do some neat things to make our code look cleaner.

## Early Return pattern

Since we can use a `return` statement to end a function immediately, we can take advantage of it. Lets look at a traditional `if else` statement and how one might convert it to the early return pattern.

~~~javascript
function healthBarColor(health, maxHealth, shield) {
  const percentLeft = (health / maxHealth) * 100;

  if (shield) {
    return 'blue'
  } else if (percentLeft < 15) {
    return 'red';
  } else if (percentLeft < 60) {
    return 'yellow';
  } else {
    return 'green';
  }
}

console.log(healthBarColor(30, 124, false));
~~~

In this case, we will find the value `'yellow'` in the console. This looks OK, but it can be cleaner with the use of an early return. Let's refactor `healthBarColor` to use this pattern now.

~~~javascript
function healthBarColor(health, maxHealth, shield) {
  const percentLeft = (health / maxHealth) * 100;

  if (shield) { return 'blue'; }
  if (percentLeft < 15) { return 'red'; }
  if (percentLeft < 60) { return 'yellow'; }
  return 'green';
}

console.log(healthBarColor(30, 124, false));
~~~

This code is functionally the same as the code above, but it is arguably more readable and is shorter. This works because when we `return` from a function, the function ends then and there and gives us the value we desire. We can clean this up even more though, with a quirk of JavaScript. In JavaScript, if you have an if statement that is one line, you can omit the curly braces ( `{` `}` ). That would look like this:

~~~javascript
function healthBarColor(health, maxHealth, shield) {
  const percentLeft = (health / maxHealth) * 100;

  if (shield) return 'blue';
  if (percentLeft < 15) return 'red';
  if (percentLeft < 60) return 'yellow';
  return 'green';
}

console.log(healthBarColor(30, 124, false));
~~~

Now we have some clean, and easy to understand code that is still peformant.

## Gotchas

Although this pattern is very clean when using returns, it can have a negative impact on performance (although normally miniscule) when mis-using this pattern. Lets look at an examples.

~~~javascript
function inventoryStatus
}
~~~