---
layout: post
title:  "Advanced Functions: Closures, Currying, Compose"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/9.jpg
---

In this section I am going to be covering **closures**, **currying** and **compose**. This should hopefully take my function understanding to a new level as well as help to make my code more efficient. The following code block contains an example function written in vailla JavaScript:

```js
function first() {
  var greet = "Hi";
  function second() {
    alert (greet)
  }
  return second;
}
var newFunc = first();
newFunc(); // an alert box containing the greeting "Hi"
```

We can now turn this into an arrow function by taking off the function keyword and assigning the function to a const variable:

```js
const first = () => {
  const greet = "Hi";
  const second = () => {
    alert (greet);
  }
  return second;
}
const newFunc = first();
newFunc();
```

### Closures

One thing to note about functions is how closures work. A general rule in JavaScript is that child elements have access to their parent elements but parent elements do not have access to their child elements. Basically, closures indicate that a function was ran and executed but it is never going to run again; however, it will remember that there are references to the variables inside of the function and so the child scope of the function will always have access to the parent scope.

If we add a new variable in the function above:

```js
const first = () => {
  const greet = "Hi";
  const second = () => {
    alert (greet);
    const name = 'bobby';
  }
  return second;
}
const newFunc = first();
newFunc();
```

In order for the function ‘second’ to run, it is entirely dependant on the variable ‘greet’ as that is what it is alerting. The function ‘second’ has access to the ‘greet’ variable as they are within the same scope. However, the new variable ‘name’ will only be accessible through the function ‘second’ and will not be seen outside of that function. It can gain access to it’s parent elements, but the parent elements of the function ‘second’ (the constant ‘first’) do not have access to it’s child elements.

### Currying

Currying is the process of taking a function that accepts multiple arguments and transforms it into a function containing a sequence of nested functions that are run one at a time. Let’s take a look at the below function:

```js
const multiply = (a, b) => a * b;
multiply (2, 4) // 8
```

Here we called the multiply function in full with both arguments. However, in a curried version of the function it looks like this:

```js
const curriedMultiply = (a) => (b) => a* b;
curriedMultiply (2)(4) //8
```

But what is happening here? We take the function called ‘curriedMultiply’ and call in only one parameter:

```js
const curriedMultiply = (a) => (b) => a* b;
curriedMultiply (3); // (b) => a* b
```

What is returned is the second part of the function, as this ‘curriedMultiply’ function contains nested functions. With each new variable (until the number of variables are exhausted) what is returned is a series of functions that take one argument that will eventually resolve to a value. So, for the above function we can add in the second parameter separately in brackets to completely run the function:

```js
const curriedMultiply = (a) => (b) => a* b;
curriedMultiply (2)(4) //8
```

Effectively we are saying a = 2, b = 4, now run a * b.

Why do we need to do this? Well, this makes the function more accessible. For example, we can put the curried function into a new variable and do something with it. In the code block below a new variable called ‘multiplyBy5’ is created that contains the ‘curriedMiltiply’ curried function and contains the value of 5. The value 5 acts as variable ‘a’ in the curried multiplier. Every time ‘multiplyBy5’ is run ‘a’ is assigned the value of five and now the function is waiting for the value of ‘b’.

Now we can run function within the ‘multiplyBy5’ variable, allocating another value which acts as ‘b’ in the curried multplier function. This completes the function, exhausting the number of open variables, and the function is able to run. What is returned is 5 (a) multiplied by the number passed through ‘muliplyBy5’:

```js
const curriedMultiply = (a) => (b) => a* b;
const multiplyBy5 = curriedMultiply (5); // (b) => a* b
console.log (multiplyBy5(5)); //25
console.log (multiplyBy5(10)); //50
```

This creates a function that is then easy to recyle using different values.

### Compose

Compose is the act of putting two functions together to form a third function where the output of one function is the input of another. Sounds confusing, right? Let’s look at the below code block of a competed compose function:

```js
const compose = (f, g) => (a) => f(g(a))
const sum = (num) => num +1;
compose (sum, sum)(5); //7
```


1. Looking at the compose function first – ‘f’ and ‘g’ are both functions and ‘a’ is an input value. This is obvious by looking at the brackets.
2. We then have a function called ‘sum’ that takes an input of ‘num’ and then adds 1 to that number.
3. The ‘compose’ function takes two arguments of sum (those values are ‘f’ and ‘g’), and the second bracket assigns ‘a’ to the value of 5.

Taking this step by step, what is happening is as follows:

Step 1:

First off, ‘a’ is asigned the value of 5:

```js
// Function runs...
const compose = (f, g) => (a) => f(g(5)) // a = 5
const sum = (num) => num +1;
console.log (compose (sum, sum) (5));
```

Step 2:

Once that parameter has run, the function ‘g’ is run with an input value of 5. The function ‘g’ uses the ‘sum’ function which takes the value of ‘num’ (at this point ‘num’ is ‘a’ which equals 5) and adds 1 to it.

```js
const compose = (f, g) => (a) => f(sum(5)) // the g function is run. g = sum. Sum is just saying 'give me 5 (a) and then 5 (a) + 1. Which equals 6.
const sum = (num) => num +1;
console.log (compose (sum, sum) (5));
```

The output of ‘g’ is now 6:

```js
const compose = (f, g) => (a) => f(6); 
const sum = (num) => num +1; 
console.log (compose (sum, sum) (5));
```

Step 3:

Now that function ‘g’ has run, function ‘f’ can now run. This does much the same as function ‘g’ – the input for ‘f’ is the output of ‘g’ (6), the ‘sum’ function is run and 1 is added to it:

```js
const compose = (f, g) => (a) => f(6) // f is now sum. Sum now equals 6. 6 plus 1 = 7
const sum = (num) => num +1;
console.log (compose (sum, sum) (5));
```

The final output is 7.