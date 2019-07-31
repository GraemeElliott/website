---
layout: post
title:  "Coding Challenge: Loops and Iteration"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/7.jpg
---

This coding challenge is going to help cement what I learned about functions and objects using loops and iteration. Whilst the principals are easy to grasp, at this point I am still a beginner and need to apply this new found knowledge in order to code better in the future. Practice makes perfect and all that jazz!

### The Challenge

John and his family went to 5 different restaurants. The bills were $124, $48, $268, $180 and $42.
John likes to tip 20% of the bill when the bill is less than $50, 15% when the bill is between $50 and $200, and 10% if the bill is more than $200.

Implement a tip calculator using objects and loops that:


1. Create an object with an array for the bill values
2. Add a method to calculate the tip. This method should include a loop to iterate over all the paid bills and do the tip calculations.
3. As an output, create:
   * A new array containing all of the tips
   * An array containing final paid amounts (amount + tip) – HINT: Start with two empty arrays as properties and then fill them up in the loop.

Advanced task:

Mark’s family also went on a holiday, going to 4 different restaurants. The bills were $77, $375, $110, and $45.
Mark likes to tip 10% of the bill when the bill is less than $100, 20% when the bill is between $100 and $300, and 25% if the bill is more than $300.


1. Implement the same functionality as before, this time using the new tipping values.
2. Create a function (not a method) to calculate the average of a given array of tips. HINT: loop over the array and in each iteration store the current sum in a variable (starting from 0). After you have the sum of the array, divide it by the number of elements in it (this will calculate the average).
3. Calculate the tip for each family member.
4. Log to the console who out of Mark and John paid the highest tips on average.

### Part 1

Start by creating the object for John’s tipping calculator:

```js
let john = {
  fullname: 'John Smith',
  bills: [124, 48, 268, 180, 42],
  calcTips: function () {
    this.tips = []; // array for 3.1
    this.finalValues = []; // array for 3.2
    for (i = 0; i < this.bills.length; i++) {
      // Determine the percentage based on tipping rules
      // Add results to the corresponding arrays
  }
};
```

At the moment John’s name has been added to the object as well as the bills from each restaurant. A method has been created to calculate the tips which includes two empty arrays (one for tips and the other for final values) and a for loop is going to be used to determine the percentage tips and total values based on the values in the bill array. There are two things that this for loop is going to achieve:

1. Determine the percentage of the tip based on the tipping rules (using if statements)
2. Add the results to the corresponding arrays

I started by writing my for loop as follows:

```js
for (i = 0; i < this.bills.length; i++) {
  // Determine the percentage based on tipping rules
  let percentage;
  if (this.bills[i] > 50) { // this.bills[i] means for each bill in the bills array
    percentage = .2;
  } else if (this.bills[i] >= 50 && this.bills[i] < 200) {
    percentage = .15;
  } else {
    percentage = .1;
  }
};
```

What is happening is that the for loop is looping through the bills array, and for each value in the array (this.bills[i]) the relevant percentage rule will be applied. The percentage value is then stored in the ‘percentage’ variable and can then be used in a calculation. However, as the ‘this.bills[i]’ variable has been written three times, and this can be cleaned up by declaring a new variable that will store the current bill value:

```js
for (i = 0; i < this.bills.length; i++) {
  // Determine the percentage based on tipping rules
  let percentage;
  let bill = this.bills[i];
  if (bill < 50) {
    percentage = .2;
  } else if (bill >= 50 && bill < 200) {
    percentage = .15;
  } else {
    percentage = .1;
  }
};
```

Now that we have the percentage value calculation rules set up, we can add the results to each array based on the output required:

```js
this.tips[i] = bill * percentage; //calculates the tip value
this.finalValues[i] = bill + (bill * percentage); // calculates the final value
```

The first statement takes the ‘tips’ empty array, and ass in the values from each bill and multiplies that value by the percentage in order to calculate the tip value for each meal. The outputs are as follows:

```js
[18.599999999999998, 9.600000000000001, 26.8, 27, 8.4]
```

The next statement takes each bill value from the bills array and adds on the percentage value as calculated in the statement above. This will then produce the final values for each meal. The method can then be called and logged to the console for further inspection:

```js
let john = {
  fullname: 'John Smith',
  bills: [124, 48, 268, 180, 42],
  calcTips: function () {
    this.tips = []; // array for 3.1
    this.finalValues = []; // array for 3.2
    for (i = 0; i < this.bills.length; i++) {
      // Determine the percentage based on tipping rules
      let percentage;
      let bill = this.bills[i];
      if (bill < 50) {
        percentage = .2;
      } else if (bill >= 50 && bill < 200) {
        percentage = .15;
      } else {
        percentage = .1;
      }
      // Add results to the corresponding arrays
      this.tips[i] = bill * percentage; //calculates the tip value
      this.finalValues[i] = bill + (bill * percentage); // calculates the final value
    };
  }
};
john.calcTips();
console.log (john);
```

Output:

```js
{fullname: "John Smith", bills: Array(5), calcTips: ƒ, tips: Array(5), finalValues: Array(5)}
bills: (5) [124, 48, 268, 180, 42]
calcTips: ƒ ()
finalValues: (5) [142.6, 57.6, 294.8, 207, 50.4]
fullname: "John Smith"
tips: (5) [18.599999999999998, 9.600000000000001, 26.8, 27, 8.4]
__proto__: Object
```

### Part 2 (Advanced Task)

Like the previous task, the first step is to create the object for Mark:

```js
let mark = {
  fullname: 'Mark Jones',
  bills: [77, 375, 110, 45],
  calcTips: function () {
    this.tips = [];
    this.finalValues = [];
    for (i=0; i < this.bills.length; i++) {
      let percentage;
      let bill = this.bills[i];
      if (bill < 100) {
        percentage = .1;
      } else if (bill >= 100 && bill < 300) {
        percentage = .2;
      } else {
        percentage = .25;
      }
      this.tips[i] = bill * percentage;
      this.finalValues[i] = bill + (bill * percentage);
    };
  }
};
mark.calcTips();
console.log (mark);
```

Now it is time to calculate the averages using a function. Start off by creating a function for creating the averages. This will pass in the argument ‘tips’ which will be the tips array:

```js
function calcAverage (tips) {
  let sum = 0;
  for (let i = 0; i < tips.length; i++) {
  };
};
```

We will be looping through the tips values array so this will require a for loop, and there is a variable called ‘sum’ which starts at 0. This is because when calculating the average we will need to sum up all of the tip values and then divide by the number of tips to get the average.

```js
function calcAverage (tips) {
  let sum = 0;
  for (let i = 0; i < tips.length; i++) {
    sum += tips[i];
  };
  return sum / tips.length;
};
```

The logic to sum up all of the tip values is then created. What is happening is it will take the tips array (for example, the array contains [2, 6, 4]), the variable will start at 0 then add on 2, then 6, then 4 to get a total sum of 12. Then the value returned is sum/tips.length (the sum of the array divided by the number of values).

Using dot notation we can add a key/value pair for the average of the tips using the function we have just created:

```js
john.average = calcAverage(john.tips);
mark.average = calcAverage(mark.tips);
console.log(john);
console.log(mark);
```

What is happening is that both John and Mark are having a new key added called average, which equals the values calculated using the ‘calcAverage’ function passing through each of their tips arrays. The updated objects are then logged to the console.

Output for John:

```js
{fullname: "John Smith", bills: Array(5), calcTips: ƒ, tips: Array(5), finalValues: Array(5), …}
average: 18.080000000000002
bills: (5) [124, 48, 268, 180, 42]
calcTips: ƒ ()
finalValues: (5) [142.6, 57.6, 294.8, 207, 50.4]
fullname: "John Smith"
tips: (5) [18.599999999999998, 9.600000000000001, 26.8, 27, 8.4]
__proto__: Object
```

Output for Mark:

```js
{fullname: "Mark Jones", bills: Array(4), calcTips: ƒ, tips: Array(4), finalValues: Array(4), …}
average: 31.9875
bills: (4) [77, 375, 110, 45]
calcTips: ƒ ()
finalValues: (4) [84.7, 468.75, 132, 49.5]
fullname: "Mark Jones"
tips: (4) [7.7, 93.75, 22, 4.5]
__proto__: Object
```

As can be seen, Mark paid the most on average in tips.

We can log this result to the console:

```js
if (john.average > mark.average) {
  console.log (john.fullname + " paid the most on average in tips. The average value was $" + john.average);
} else if (john.average < mark.average) {
  console.log(mark.fullname + " paid the most on average in tips. The average value was $" + mark.average);
} else {
  console.log (john.fullname + " " + john.fullname + " both paid the same amount on average in tips.")
}
// Mark Jones paid the most on average in tips. The average value was $31.9875
```