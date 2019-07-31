---
layout: post
title:  "Objects and Methods"
author: graeme
categories: [ JavaScript ]
image: assets/images/blog-images/6.jpg
---

Objects group together a set of properties (variables and arrays) and methods (functions) to create a model made up of what are called **key/value pairs** in a readable and recognisable way. A property details the make-up of the object (such as the name, age, gender, etc.) and a **method** represents a task that is associated with the object (for example, checking how many rooms are available at a hotel by subtracting the number of booked rooms by the number of total rooms).

The following object represents a hotel that has four properties and a method:

```js
let hotel = {
  name: 'Overlook',
  rooms: 40,
  booked: 20,
  roomTypes: ['twin', 'double', 'single'], // properties end
  checkAvailability: function () {
    return this.rooms - this.booked;
  } // method
};
```

The object above is created using **literal notation**. This means that the object contains:

* Curley braces with the properties and methods stored within the braces.
* Key/values are separated with a colon.
* Each keyvalue pair is separated using a comma

The properties and methods within an object can then be accessed using **dot notation or square bracket syntax**:

```js
let hotelName = hotel.name; // dot notation
let roomsFree = hotel ['checkAvailability'](); // square bracket syntax
```

Notice that when using square bracket syntax the property or method must be in quotation marks like you would with a string.

The DOM can then be manipulated using the object. Example code is below:

```js
let hotel = {
  name: 'Overlook',
  rooms: 40,
  booked: 20,
  roomTypes: ['twin', 'double', 'single'],
  checkAvailability: function () {
    return this.rooms - this.booked;
  }
};
let elName = document.getElementById('hotelName');
elName.textContent = hotel.name;
```

What is happening is that a variable with the name ‘elName’ is getting the element with the ID ‘hotelName’ within the HTML and then the text content within that ID is being amended to include the name of the hotel from the object.

Another method of creating an object is using **constructor notation**. The following is an example of that format:

```js
let hotel = new Object ();
hotel.name = 'Quay';
hotel.rooms = 40;
hotel.booked = 20;
hotel.checkAvailability = function () {
  return this.rooms - this.booked;
}
```

Notice that a ‘new Object ()’ function is called which creates an empty object. The properties and methods are then created using dot notation (nameOfFunction.property), with the keys and values being separated by an equals sign. The key/valye pairs are then separated by a semi-colon.

To update an object you can use either dot notation or square brackets:

```js
hotel.name = 'Park';
hotel['name'] = 'Park';
```

However, you cannot update methods using square bracket syntax.

### Creating Many Objects: Constructor Notation

Functions can be used as a template for creating objects when you want several objects to represent similar things.

```js
function Hotel (name, rooms, booked) {
  this.name = name;
  this.rooms = rooms;
  this.booked = booked;
  this.checkAvailability = function () {
    return this.rooms - this.booked;
  };
}
```

The above code uses a function called ‘Hotel’ (notice the capital ‘H’ when creating objects like this as opposed to other functions, which normally begin with a lowercase letter) that is used as a template for creating that represent hotels. The uppercase letter is supposed to help remind developers to use the new keyword when they create an object using that function.

The function has three parameters, with each one setting the value of the property in the object.

The ***‘this’*** keyword is used instead of the object name to indicate that the property or method belongs to the object that this function creates.

Once the template has been created, you can then create instances of the object using the constructor function:

```js
let quayHotel = new Hotel ('Quay', 40, 25)
/* name: 'Quay',
    rooms: 40,
    booked: 25,
    checkAvailability: function () {
      return this.rooms - this.booked;
  }
}; */
```

Below is an example of creating and accessing an object using constructor notation:

```js
let quayHotel = new Hotel ('Quay', 50, 25);
let detailsQuay = quayHotel.name + ' rooms: ' // Quay rooms:
    detailsQuay += quayHotel.checkAvailability(); // Quay rooms: 25
let elQuay = document.getElementById ('hotelQuay');
elQuay.textContent = detailsQuay; // Object appears on the page within hotelQuay element
```