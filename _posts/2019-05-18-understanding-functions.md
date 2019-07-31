---
layout: post
title:  "Understanding Functions"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/5.jpg
---

Functions are used to group a series of statements together in order to fulfil a specific task. If there are parts of a script that repeat the same task then a function can be used to create the script for the task and can then be called within the script where necessary. Functions also offer a way to store the steps needed to achieve a task.

### Basic Function Declarations

The following are examples of **function declarations** which create functions that can be called later in the code.

The basic structure of a function declaration is as follows:

```js
function nameOfFunction (par1, par2) {
    // Code block
}
```

The function consists of:

* A **name** (unless you are writing an anonymous function) which can be used to call the function when needed. It should describe the task that it is performing.
* **Parentheses** which could contain **parameters** that is information required for the function to run. However, if no parameters are required then this can be left blank.
* A **code block** inside **curly braces**, which is the statement of the task being performed.
* When you write a function and expect a response, a **return** statement can be used to return the required value.

```js
function calculateAge (currentYear, birthYear) {
  return currentYear - birthYear;
};
let age = calculateAge(2019, 1990);
console.log(age) // returns 29
```

As can be seen from the above code, the function ‘calculateAge’ is called in the variable ‘age’ with the two parameters 2019 and 1990.

Multiple values can also be obtained from a function:

```js
function getSize (width, height, depth) {
  let area = width * height;
  let volume = width * height * depth;
  let sizes = [area, volume];
  return sizes;
}
let areaOne = getSize (3,2,3) [0];
let volumeOne = getSize (3,2,3)[1];
```

What is happening in the above code is there are two variables – ‘area’ and ‘volume’ – that calculate the area and volume of three given parameters. The two values are then stored in an array called ‘sizes’ which means that instead of getting both area and volume, an individual variable can be obtained by using the index of the array (by using [0] or [1]).

### Function Expressions

A **function expression** is where the interpreter would expect to see an expression but instead contains a function. The name of the function is usually omitted, but the variable it is contained within is given a name. If there is no name given then this is known as an anonymous function.

```js
let area = function(width, height) {
    return width * height;
}
let size = area(3, 4)
console.log (size) // returns 12
```

In a function expression, the function is not processed until the interpreter gets to the statement. This means the function cannot be called before the interpreter has discovered it, and any code that appears up to that point can alter what goes inside the function.

### Exercise:  Creating a tip calculator with a function

In this exercise you must you must create a function that takes in an array of values and calculates a tip percentage based on the amont of the bill. The three bills are $124, $48 and $268. If the value is less than $50 then the tip is 10%, if between $50 and $200 then it is 15%, and if it is greater than $200 then the tip is 20%.

To start this exercise you can start by creating your arrays:

```js
let tipPercent = [0.1, 0.15, 0.2];
let bills = [124, 48, 268];;
let total = [];
```

There are three variables – the tip percentage, the bills, and a total. The reason for the total is we will calculate the total bill required at the end.

The function can now be created. Start off with either a function expression or a function declaration. I will use a declaration that passes through an array as a parameter:

```js
function tipsCalculator (array) {
    // Code block
}
```

The code block will contain the function code. When complete, it looks as follows:

```js
for (let i = 0; i < array.length; i++) {
    if (array[i] < 50) {
      total.push(array[i] + (array[i] * tipPercent[0]));
  
    } else if (array[i] >= 50 && array[i] < 200) {
      total.push(array[i] + (array[i] * tipPercent[1]));
      
    } else {
      total.push(array[i] + (array[i] * tipPercent[2]));
  
    }
  }
```

Let’s break this down. Firstly, as there are three potential outcomes based on the amount of the fill, if statements can be used. There are three percentage brackets, so we can use ‘else if’. The psudo code looks like this:

```js
if (i < 50) { // where i is the bill of the meal
    outcome 1; // apply the first percentage
} else if i >= 50 && i < 200 {
    outcome 2; // apply the second percentage
else {
      outcome 3; // apply the third percentage
}
```

The required outcome is to populate the ‘total’ array with the totals for each bill (bill + tip). This means that the calculation for each bill amount will need to be pushed into the total array. The equation to use is ‘bill amount + (bill amount * tip percentage)’. The calculation in brackets calculates the how much of a tip to give, which is then added on to the bill amount to get the final bill.

As we are iterating through an array, this will need to be placed into a ‘for loop’.

```js
for (let i = 0; i < array.length; i++) {
    // Code block
};
```

For loops are dicussed in another post, but the general syntax is to start off with an iterator (let i=0) followed by a condition (in this case, the iterator must be less than the array length) and then an incrementor or decrementor.

The full function looks as follows:

```js
function tipsCalculator (array) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] < 50) {
      total.push(array[i] + (array[i] * tipPercent[0]));
  
    } else if (array[i] >= 50 && array[i] < 200) {
      total.push(array[i] + (array[i] * tipPercent[1]));
      
    } else {
      total.push(array[i] + (array[i] * tipPercent[2]));
  
    }
  };
}
```

There are various things you can do to retrieve the output. You can return the value of total that can be used elsewhere in the code. However, for this exercise we will console.log the bills amount (as a reminder) and then console.log the total, which will contain values based on the function criteria met.

```js
function tipsCalculator (array) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] < 50) {
      total.push(array[i] + (array[i] * tipPercent[0]));
  
    } else if (array[i] >= 50 && array[i] < 200) {
      total.push(array[i] + (array[i] * tipPercent[1]));
      
    } else {
      total.push(array[i] + (array[i] * tipPercent[2]));
  
    }
  };
  console.log (bills);
  console.log (total);
}
```

We can now call the function passing in the bills array:

```js
tipsCalculator(bills);
// [124, 48, 268] = bills amount
// [142.6, 52.8, 321.6] = totals for bills + tip
```