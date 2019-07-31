---
layout: post
title:  "Dynamic HTML Table With JSON Data"
author: graeme
categories: [ JavaScript, tutorial ]
image: assets/images/blog-images/2.jpg
featured: true
---
For this exercise, I have been tasked with taking some JSON data and inputting it into a table. There are so many different ways of doing this, but as I am trying to up my game with JavaScript, I will be completing this task using vanilla JavaScript (no jQuery required!). I have been given a JSON file with some contacts (there are no nested objects in this one – this will come in a later exercise), and I will be using a JavaScript file containing my script and an HTML file for displaying the data. I am not going to do any styling in this exercise.

The files for this exercise can be downloaded from this [GitHub Repository](https://github.com/GraemeElliott/JavaScript_Exercises/tree/master/exercise_1).


## The JSON Data

JSON (or JavaScript Object Notation) is a lightweight data format that can easily be created and exchanged between the browser and a server. The data is in name/value pairs, both of which are in double-quotation marks and separated between a colon:


```
    [{“first_name”: “John”, “last_name”:”Smith”}]
```

Here is a sample of the JSON data I will be using. There are 1,000 objects I will need to display but the below shows just three (reason being I would like to see what I am working with).

```js

[{"id":"17b78bad-876d-49c4-89d0-53a8cb165e06","first_name":"Johny","middle_name":"233.86.192.59","last_name":"Scapens","gender":null,"email":"jscapens0@globo.com","website":"http://disqus.com/nisl.jpg","avatar":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAI6SURBVDjLpZJbaJJxGMaHgdcFXURdBLtZrGitiFh0uhjRVRTVWI1as7mQakhjyyEkRAcaHSCrj0xrWGuuoVsr25qzfeYObh6yJJdzavoZs3Sy8PhJ8vR9EoHkotXFA/+b3+//vC9vEYCi/8mvh8H7nTM8kyF0LpoacCazLxzxbM/bb1S3OUo8GQtz/iggGfi1O0NaAzS8kQwCURqBORrTX9LQf5jHQ3KWlA1RnAUFeneGsATSoKIZOGdTsAWSMPuTsFNJeL7SEOoF4GtrUKuuShUUvJpKUd4wnYMtDDj5KQGTN4FRTyInOvH8MDonL6BKuRcFBey8fqYyC0/4Ehhn4JGZOBp1AtT1VkOkrYfMKIKgsxq7b+zErssV0TyBxjaf9UVomBh4jPnVyMCG6ThbGfKRVtwebsK1wdO4+JIPce8xbBGXI0+gMkWoqZ/137jjIBlY/zEGnqoO+2R7wGvfj/N9x3FAWonNojKUCUtTeQKlMUT02+fgCqVzs7OwzhnLyd4HU2xlCLsOYlPz+sI7uK8Pcu4O+EnNRAhWfwKOzym8Y2LyxCAf9GGHZDvKm9Zha2NptudcRUnBQ7rZ5+G0aVzEpS4nJelwZMXt9myL3Bpskyq9FmUzQuZu2B63QCXcEH50ak3Jb4KF0i+p5D5r3aYeJeoRNCgwfq8BCv7q8F8L2Dw9u5HbcWateuj6IXi0V0HUrsCiBGweNBRzZbxVasXJYkhrll1ZtIDNnaPLl9w6snRlwSX+a34AgPPwSZzC+6wAAAAASUVORK5CYII=","city":"Chandmanĭ","country":"MN","postal_code":null,"street_number":"967","street_name":"Grasskamp"},
{"id":"72a22bb0-d82e-4ffb-8392-3fdda288fb86","first_name":"Udale","middle_name":null,"last_name":"Paolillo","gender":"M","email":"upaolillo1@icio.us","website":"https://cnet.com/in/tempor/turpis.js","avatar":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAKFSURBVDjLpVPfSxRRFP52Z3aXXdOd1V11NbYHUUQRtRIi38pCCQoi6KWX/oRefeq1t94TgyCJhKiHWgwki4pgU3YxonzQ1BXBrXHd2Z2Ze2fuTPdef0Sl9NDA5dyBc77vO+c7N+D7Pv7nU/+VsLCwcN913RuO46g8gkd5KKUiPgocpaBQKMR5wYSmadcikRgIL4LnQWbzmkRCw8xM9nAF+Xx+VBQnk8n2uro6rHzbgGD3PB+e73EgH4yDEUIOB+DJ2UwmI++WZcPhxYuFeQ7gHZwLF8dkG38BPHj9I1Ovr0PXdXR3d+8yM4ae3gHJ7u+xi9Z/UzD1Vo9Sh005O8Wx5mgUiqIgl8thYGBQSi/kczwyyc44YPrSlV8KOKvKJ1qIhAKdqtaCT8ub6EhUZIJQwJiH3r6Tkn1fhb83g6Ds06ZtFnE7Y2FACXhQm7rwfjWCdMcg5uZeIfviKZgcoodS/Qomy3fBRykJJEDVpO2E/3AgrJdqCCkewlobJp7NS8+Hhk5j+vFDuMzF5Nd7WC1tShUHLRiWlVICQM32OZiNrW0H8ZiK9IkOvFt8g/7qMhKNTcJ+3Gq6Da9RrIInwaWCHcPqog6BaTuomARGzcZSUUfZIIgeP4XsR4bh4XN7FvoyCjChQCk1Xw4bJplNaWGlwgvDXIqq8B0PBrhdDGsrJZztaUUmHZV2it7FRsbjDdylD1DLhlVtiAVDYkg1i2B9YwfGdg1W1YZdJWiMEIxc70cymZKS91e/tSUlHVLLVXM26IdGP383UCzqjlOzxxl1l5hNSy6lGyNnyr0vZ57f4cV9+49JxF172RfVNMyrlS3niWuR865Fj+Wmb9I/lnONn+xRr/UnsVG4KayFAQcAAAAASUVORK5CYII=","city":"Fort Worth","country":"US","postal_code":"76129","street_number":"389","street_name":"Forster"},
{"id":"5cdcff4b-9c66-402d-825c-ee16935420c4","first_name":"Hadley","middle_name":null,"last_name":"Base","gender":"M","email":"hbase2@washington.edu","website":"http://cocolog-nifty.com/vestibulum/eget.aspx","avatar":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAALoSURBVDjLhZP9S1NRHIf3D+gfURRhL2gFFQYFiSkEIkZFI8kfyjIUNNFCrOnMFxKJMTfCKNEl5AxUVCx1bm6NdMMkx97ci5vTjTn3otvdy9326dxbiinRhQ/n3MN9nnO+557DAcDZH7VanSuXy4VTU1OL4+Pjm8PDw4HBwUGTRCIRf+wXXz34/V5Ho9FkEFhE4ITT6YTf78f29jYikQhCoRAMBj3E3a/otyJ+v1DQnvmX4A88abVakU6nEY1GwUgcDgd8Ph+SySTSSQo0ZYJ8egCvO+qV7W2NmXsCZmYGTiQSYB6apsG8WywWBINBVhqnNhAL65GKreDrRC+aX1b2swICXyTLToXDYRbY2dlhJevr6zAajWDGk0kakZAR8bCBXUWCpKb6Uar26ZNcDoFFa2trYGIymViIqZkRud1uth+PhYhAR0An6W+RFcahVCpRXl4u4mRnZ+N/qbh/BZMfShDZ9rLiQCAAm82GsrKyJVag0+lgNpuhUqnQ19fHQkzrcrlgNi5DN/EAWytS2Ba6Ybfbsbq6Co/HAy6X62MFDLwLMRImzBiTlppr2DRIQIct0I/chVY7i3mdBUbHBopLbm0dEjDZhc3LKmgGihDbHENsowt+6zgWx+qh0jvwRWtEQdFN/aESdkU5OUQ8y4fPNITYWjPm2s8hsTWEH+/zMK8exTvpBApuFPX8cxNLiy/APtOAuLcPlKUMc205iDrqEbRNYKH3NvILC1N5+dcvsQdJIBCIFAoFPEHyK9d/Qm/XYklaigDZuOhqLSLmO7+zco+U8gYOhQDC6lzt3kns7OzM4Lc2T38alcDmNUD3TQjHXBfiHjE7e2SFS0o4y7aUrQKUewQK/mmvoulk1t5l4vF4Gc8a6noeVz2k1d15oHxWxP0ziHnJHnil+/IZ9I4Oru8SyBqOSzkHr2dVVeVlRcf5qKI1JyVvyU7Lms6kZbxTKdmLLFrWeCJGIGrm+TFqpv4oNV13RPkLngD4bMIOcuMAAAAASUVORK5CYII=","city":"Raduzhnyy","country":"RU","postal_code":"601380","street_number":"9114","street_name":"Warbler"}]

```

As you can see from the sample data, there are some inconsistencies. Some may/may not have values for specific keys such as the avatar, email or street_name, and sometimes the data value may not even be consistent with that the key is. I will not be cleaning the data for this exercise, but it is worthwhile noting this for future experience.

#### Connecting to the JSON data

You can connect to JSON data using XMLHttpRequest, AJAX and Fetch. As the data I am working with is locally stored, the best route to use local JSON data is by using Fetch. While XMLHttpRequest (or XHR) is still a popular method of accessing JSON data, it is bulky, old, and does not allow for data streaming.

A simple Fetch request looks like this:

```js
fetch(url)
.then (function(response) {
    console.log(response);
    })
.catch(function(error) {
    console.log(error);
});
```

The code starts with making the fetch request and inside it is a URL/link to the data. A .then function is called to do the next task of making a call to the data and returning a response. Once this has happened then, the response is logged to the console. There is also a .catch in the code which is used when an error occurs – I will not be using .catch on this basic exercise, I will be focussing solely on .then.

For the sake of testing, I have put some sample data into a JSON file called ‘sample.json’ and set the local directory address as the URL:

```js
fetch("./data/sample.json")
    .then(function (response) {
    console.log (response);
});
```

So I have fetched the data, called for a response in a function, and then printing that response out in the browser console to make sure I am connected to the data. When I inspect the code in the browser console, I can see that the request has worked as I am getting a response back with a status code of 200.

I can change the response to use a JSON method which will parse the data and return it in a JSON format:

```js
fetch("./data/sample.json")
    .then(function (response) {
    console.log (response.json());
});
```

As you can see, this brings back three arrays (the JSON objects), and I can go in and see that the JSON data’s returned. But this is not the best method of doing this – it is usually broken out as so:

```js
fetch("./data/sample.json")
    .then(function (response) {
    console.log(response);
    return response.json()
})
    .then(function (json) {
    console.log(json)
});
```

The first .then function returns the response to the data (everything is running ok). A json() method then takes the response stream and reads it to completion, returning a promise that resolves with the result of parsing the data as JSON. Once this is done, then another .then function logs the JSON data returned to the console.

The JSON data can then be accessed by calling specific keys or object positions. The code below looks at the first object (object 0), gets the key called “first_name” and returns its value:

```js
fetch("./data/sample.json")
    .then(function (response) {
    console.log(response);
    return response.json()
})
    .then(function (json) {
    console.log(json[0].first_name)
});
```

The JSON data is now set up and connecting successfully – now it’s time to set up the table.

#### The HTML Table

A HTML table has this standard format:

```html
<table style="width:100%">
    <tr>
    <th>Firstname</th>
    <th>Lastname</th> 
    <th>Age</th>
    </tr>
    <tr>
    <td>Jill</td>
    <td>Smith</td> 
    <td>50</td>
    </tr>
    <tr>
    <td>Eve</td>
    <td>Jackson</td> 
    <td>94</td>
    </tr>
</table>
```

Inside a <table> tag there are <tr> tags for table rows, <th> tags for table headers and <td> tags for table data.

As the table needs to be dynamic to handle however much data is in the data file, the data and row tags will be added to this table in the code. All that needs to be included in the HTML file is a simple HTML table that is as follows:

```html
<table class="table">
</table>
```

Now it’s time for the challenging part!

#### Creating the headers

All of the code being used to create the table is going to be in one function called tableData. This makes the function reusable which is great coding practice. Below is the code that creates the headers for the HTML table by using the names of the keys in the JSON data:

```js
//Get JSON, run function
fetch("./data/contacts.json")
        .then(function (response) {
        return response.json();
    }).then(function (json) {
        tableData(json);
});
// Function
function tableData (data) {
    // Create Headings
    let objectKeys = Object.keys(data[0]);
    let table = document.querySelector('table');
    let headerRow = document.createElement ('tr');
    for (let keyName of objectKeys) {
            let headerCell = document.createElement('th');
            headerCell.append(document.createTextNode(keyName));
            headerRow.append(headerCell);
        };
    table.append(headerRow);
};
```

First, the tableData function is called inside Fetch once a successful response has been achieved (see line 8). Inside the tableData function, the JSON data is passed through as a parameter called ‘data’.

The next step is to grab the object keys and assign them as the header titles in a variable or statement. The let statement is being used as, scope wise, let allows you to locally assign values that cannot be called outside of the function where it is present. Assigning the objectKeys value as the names of the keys of the JSON objects is achieved by using the Object.keys method. Basically this looks at the first object within the data parameter and returns all of its keys. Assuming that the first object has all of the keys required (even if there are no values for every key) this is a good starting point.

The property ‘table’ is assigned a querySelector which is used to select the HTML table which has been assigned the class name ‘table’. And the headerRow property creates the <tr> tags (which will be used throughout the code).

As the table needs to be dynamic, a loop must be used to iterate through all of the JSON data in the provided file. The For loop is as follows:

```js
for (let keyName of objectKeys) {
    let headerCell = document.createElement('th');
    headerCell.append(document.createTextNode(keyName));
    headerRow.append(headerCell);
};
```

For each instance of a key name obtained through objectKeys, a cell is created as a table header (<th>). After the header tag is assigned, a text node is appended to the tag which will display the name of the key. This will then be appended to the header row (<tr>), and the headerRow is then appended to the table.

#### Inputting the data

For loops are also used for the data section, which can get quite complex as there are nested loops.

```js
// Table Data
for (let i = 0; i < data.length; i++) {
    let dataRow = document.createElement('tr');
    for (let keyName of objectKeys) {
        let dataCell = document.createElement('td');
        if (data[i][keyName] === null) {
            dataCell.append(document.createTextNode("Not Known"));
        } else if (data[i][keyName].startsWith("data:image")) {
            let img = document.createElement('img');
            img.src = data[i][keyName];
            dataCell.append(img);
        } else {
            dataCell.append(document.createTextNode(data[i][keyName]));
        };
        dataRow.append(dataCell);
    };
    table.append(dataRow);
}
```

The first For loop iterates through the whole length of the JSON file for its length and increments. Upon each increment, a row is created (as with the header row).

Another For loop then iterates through the object keys and for each key a data cell is created (<td>).

An if statement is now included, which states the following:

* If the key name === null (a value in the JSON data) then a text node is assigned to that data cell which will be ‘Not Known’.
* Else, if the data of the key starts with ‘data:image’ (for the avatar data, this is a data URI scheme for images) then it will be assumed it is an image, and an image tag will be applied which will contain the image link. This means the image will be shown instead of the text link.
* Else, a data cell will be created and will contain the value of the key.

The data cells will then be appended to the data row, which will then be appended to the table.

And the code is now complete. You can download the code for this exercise by visiting this [GitHub Repository](https://github.com/GraemeElliott/JavaScript_Exercises/tree/master/exercise_1).