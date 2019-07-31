---
layout: post
title:  "ECMA6 – Some Key Features"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/8.jpg
---

With the evolution of JavaScript there have been some advancements in the way code is written in order to make it easier to read and faster to run. The advancements have reduced the amount of code written as well as making the code more efficient and dynamic. I am not going to cover everything new in ECMA6 (and beyond!) but highlight a few of the most useful ones that I have learned through the courses I take. This post will more than likely be updated in the futre to include some newly found ECMA6 scripts.

Note – if you are worrying about cross browser compatibility then Babel is your friend. Babel is a compiler that will transform your ECMA6 code into something vanilla Jacascript that can be understood by all browsers.

#### Const and Let

Instead of using ‘var’ let and const should be used.

**‘Const’** means that the variable cannot be reassigned. This means that you cannot provide the const variable a value at the start of the code, and then reassign it a difference value further on down the code. If you try and change the value of a const variable then an error will occur:

```js
const greeting = "Hi there"
const greeting = "Hello" // error: Uncaught SyntaxError: Identifier 'greeting' has already been declared
```

However, ‘const’ variables are not completely immutable. If an object is assigned as a const then it can be mutated but cannot be reassigned further down in the code. The following is perfectly legitimate:

```js
const obj = {
  name: "bobby",
  experience: 100,
  wizardLevel: false
}
obj.wizardLevel = true;
console.log (obj.wizardLevel) // true
```

**‘Let‘** variables can be reassigned, but let provides the variable with better scope access. Let is only seen within the local scope and cannot be called ouside of the scope it is in:

```js
const player = 'bobby';
let experience = 100;
let wizardLevel = false;
if (experience > 90) {
  let wizardLevel = true;
  console.log ("inside function: " + wizardLevel); // true
}
console.log ("outside function: " + wizardLevel); // false
```

Any time the let variable is wrapped around curly braces it is being used in a new scope where it can be accessed. However, if we changed the wizardLevel variable to var then the following happens:

```js
const player = 'jim';
let experience = 100;
var wizardLevel = false;
if (experience > 90) {
  var wizardLevel = true;
  console.log ("inside function: " + wizardLevel); // true
}
console.log ("outside function: " + wizardLevel); // true
```

This is because wizardLevel has already been changed in the if statement, and that means that change has been made globally rather than locally.

## Destructuring

Taking the below object as an example:

```js
const obj = {
  name: "bobby",
  experience: 100,
  wizardLevel: false
}
```

In order to assign the object values to variables we used to have to do the following:

```js
const player = obj.player;
const experience = obj.experience;
let wizardLevel = obj.wizardLevel;
```

However, in ECMA6, you can destructure an object by doing the following:

```js
const {player, experience} = obj;
```

This will then do as the top two statements are doing. It will assign the const variables player and experience as their object key values. Same for let:

```js
let {wizardLevel} = obj;
```

## Object Properties

ECMA6 also introduced a new was of assigning object properties names, making it more effiecient, dynamic and easier to update, especially when there are lots of objects with the same key/property names:

```js
const keyFirstName = "first name";
const keyLastName = "last name";
const obj = {
  [keyFirstName]: 'tim',
  [keyLastName]: 'jones',
}
console.log(obj)
// first name: "tim"
// last name: "jones"
// age: 24
```

Say for instance there is a list of variables for the object keys that may change at some point in the future, these keys can be declared in a seciton of the code and amended later on. For the example above, keyFirstName is currently ‘first name’, but lets say that later on you want to change that key to be capitalised to ‘First Name’. Well, instead of going through every object and changing the key format, you can just change the variable in the code which will then update that key for the rest of the objects.

The syntax for constructing an object using variables has also been cut short. The following code was used to construct an object of variables:

```js
var a = 'test';
var b = true;
var c = 789;
var okObj = {
  a: a,
  b: b,
  c: c
};
```

However, the following can now be written, producting the same output:

```js
var okObj = { a, b, c };
```

## Template Strings

```js
let firstName = 'John';
let lastName = 'Smith';
let nickName = "Smithy";
let age = 60;
```

When writing out a string constaining variables we used to write it out as below:

```js
const greeting = "hello " + firstName + ' ' + lastName + " aka " + nickName
console.log (greeting); // hello John Smith aka Smithy
```

This could get quite tedious and prone to errors. Using back ticks (“) we can constuct a template sting using dollar signs and curly braces:

```js
const newGreeting = `Hello there ${firstName} ${lastName} aka ${nickName}. You are ${age - 10}.`
console.log (newGreeting); // Hello there John Smith aka Smithy. You are 50.
```

This makes things a lot more easier to write and instantly makes it more readable. You can even edit code inside the braces.

We can then use the template in a function and assign the variables to be arguments, having default argument values, that can be read by the function:

```js
function funcGreeting (firstname='', lastname = '', nickname = '', age2=30) {
  return `Hello there ${firstname} ${lastname} aka ${nickname}. You are ${age2}.`
};
console.log (funcGreeting()); //Hello there   aka . You are 30.
```

## Arrow Functions

A normal function written in vanilla JavaScript is written below:

```js
function add (a, b) {
  return a + b;
};
```

However, these can now be made shorter using **arrow functions**:

```js
const add2 = (a, b) => a + b;
```

This is a lot easier to write than constantly writing function and curly braces. The structure is: assign the function to a variable, equals sign, arguments, arrow, and then what to return or what to do.