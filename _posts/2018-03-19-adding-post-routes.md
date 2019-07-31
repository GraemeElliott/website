---
layout: post
title:  "Adding POST Routes"
author: graeme
categories: [ JavaScript, tutorial ]
image: assets/images/blog-images/3.jpg
---

The first back-end task for the Cambridge Gigs project is to create a POST route which will enable users of the site to log-in and post new gigs by using a web form. Users will eventually have the ability also to edit and delete the gigs they have uploaded, but for the time being the main aim is to get them up there. Once the ability is there to post, then I can use CRUD (Create, Read, Update and Delete) to manage the workflow more efficiently.

The main objectives of including the POST route include:

* Setup a new gig POST route
* Add in body-parser
* Set up route to show form
* Add basic unstyled form

To set up a POST route, go to the app/index.js file (mine is called app.js) and include the following route:

```js
app.post("/gigs", function (req, res) {
    //get data from form and add to gigs array
    //re-direct back to gigs page
})
```

This is the barebones of what is required; more will be added soon.

Next, NPM install Body Parser, and in the app.js file include it in the list of required variables at the top:

```js
bodyParser = require ("body-parser");
```

and then include the following ‘app.use’ code:

```js
app.use (bodyParser.urlencoded({extended: true}));
```

The form will be included in its own EJS template. A new .ejs file named ‘new-gig’ is created, and below the POST route for the form a GET route is included:

```js
var gigs = [
  {name: 'Gig One', image: "https://www.testurl.com/icon.png"},
  {name: 'Gig Two', image: "https://www.testurl.com/icon.png"}
  ]
```

The POST route can now be updated to take the elements from the form, create a variable called ‘newGig’ and then push that variable into the array above. Once that has been submitted the user will be directed to the ‘/gigs/’ page to view all of the gigs:

```js
app.post("/gigs", function (req, res) {
    //get data from form and add to gigs array
    var name = req.body.name;
    var image = req.body.image;
    var newGig = {name:name, image:image}
    gigs.push(newGig)
    //re-direct back to gigs page
    res.redirect("/gigs")
});
```

This data will be posted to a database when that functionality has been created. But, for now, this POST route is up and running.

