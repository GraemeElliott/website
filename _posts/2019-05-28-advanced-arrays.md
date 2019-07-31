---
layout: post
title:  "Advanced Arrays: Map, Filter, Reduce"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/10.jpg
---

When searching for help online using Google, Stack Overflow, Reddit, etc. I have always seen answers to problems using three methods called Map, Filter and Reduce. However, up until this point, I have ignored these methods as they were new with ECMA advancements (so, the browser compatibility can be patchy) and I was wanting to get a firm grasp of more beginner to intermediate JavaScript first before moving on to these advanced methods. Whilse this post describes the basic functionality, I hope you will see how useful these methods are. This post will be updated as I learn more about them.

#### Map

Before I can really explain Map I have to remember how I used to iterate through an array in JavaScript using For Loops. Taking an array of numbers (array) what I would like to do is iterate through this array and multiply the numbers in the array by 2. I would then like a new array consisting of those new values.

I can do this using a For Loop:

```js
const array = [1, 2, 3, 4, 5];
let newArray =[];
for (i=0; i < array.length; i++) {
  const num = array[i] * 2;
  newArray.push (num)
};
console.log(newArray);
```

I can also use forEach:

```js
const array = [1, 2, 3, 4, 5];
const multiplyArray = [];
const newArray = array.forEach ((num) => {
  multiplyArray.push(num * 2);
})
console.log (double);
```

However, a new method I can use is Map:

```js
const array = [1, 2, 3, 4, 5];
const mapArray = array.map ((num) => {
  return num * 2;
})
console.log (mapArray);
```

The benefit of Map is that you do not need to declare an empty array for the new values to be pushed into. The Map method creates a new array with the results of calling a provided function on every element in the calling array. But there is a fundemental difference between For Loops and Map – with Map it is iterating through the array and assigning the new value to a new array each time it runs. However, with For Loops it iterates through the array but it’s actions are not limited – it can do anything it wants based on the array it is iterating through. This makes the function within Map a pure function as there are no side-effects. It returns a value and that is all. The above code block can also be written short hand as below:

```js
const mapArray = array.map (num => num * 2);
```

### Filter

Filter is a powerful method that I love. This can be used to filter an array based on set conditions:

```js
const array = [1, 4, 34, 99, 67];
const filterArray = array.filter (num => {
  return num > 5
});
console.log (filterArray) // 34, 99, 67
```

What the above code block is doing is getting the array, and filtering based on the parameter ‘num’ (each number in the array) and returning all of those numbers that are greater than 5. As this is iterating throiugh an array and returning  an array of numbers (like Map) a return statement must be used. Like Map, this can be written in short form too:

```js
const filterArray = array.filter (num => num > 5);
```

### Reduce

Reduce is a really powerful method that has a lot of functionality. I will only be going through one way of using it:

```js
const array = [1, 2, 3, 4, 5];
const reduceArray = array.reduce ((accumulator, num) => {
  return accumulator + num;
}, 0)
console.log (reduceArray) // 15
```

The Reduce method takes two parameters: the function and the accumulator value, The accumulator within the function is the starting point, or default value, of the method and this is where the function will start. ‘num’ (as always) are the values within the array. What is happening in the code block above is it is starting at 0 and then going through each array value and summing the numbers. The final value (0 + 1 + 2 + 3 + 4 +5) is 15. If we were to start at another number then the value will change:

```js
const array = [1, 2, 3, 4, 5];
const reduceArray = array.reduce ((accumulator, num) => {
  return accumulator + num;
}, 5)
console.log (reduceArray) // 20
```

These three methods are very powerful and are well worth remembering and using in the future.