---
layout: post
title:  "Adding in MongoDB and Mongoose"
author: graeme
categories: [ JavaScript, MongoDB, Mongoose, tutorial ]
image: assets/images/blog-images/4.jpg
---

Using databases enables users to store data that can be used dynamically on portals, applications and websites. There are two types of databases: SQL (relational) and NoSQL (non-relational). MongoDB is a NoSQL database and the reason I am using this is because relational databases require all items to be related and defined ahead of time. This means that it can be restrictive and quite messy if, say, a new field has to be included after the database has been created. However, with NoSQL, this is not the case; there are no tables that need to be defined, things can be stored in a JSON format as key/value pairs, and there is a lot of flexibility when adding in new fields at a later date.

MongoDB is also the most popular database to use with NodeJS (think of the MEAN stack: MongoDB, Express, Angular, NodeJS).
Mongoose makes it easier to interact with MongoDB and provides a schema-based solution that helps with keeping the data organised and easy to handle.

### Setting-up MongoDB

Inside the app.js file, the first thing to do (once everything has been installed and required) is to connect to the database using Mongoose. If a database has not been set up yet, then this can be done dynamically by entering the following and running Node:

```js
mongoose.connect("mongodb://localhost/cambridgegigs");
```

Still inside the app.js file, set up the schema to contain all of the fields relating to what you are uploading. For the gig, I set up a schema to include everything required for each gig (band name, suppers, venue, etc) as well as a couple of extra fields that are going to help with the general flow of the website.

The schema is as follows:

```js
var gigSchema = new mongoose.Schema ({
    name: String,
    nameForUrl: String,
    supports: String,
    venue: String,
    venueForUrl: String,
    date: String,
    ticketsUrl: String,
    price: String,
    image: String,
    facebook: String,
    twitter: String,
    youtube: String,
    spotify: String,
    bandcamp: String,
    description: String,
    author: {
        id: {
            type: mongoose.Schema.Types.ObjectId,
            ref: "User"
        },
        username: String,        
    },
    
});
```

You can see that an author has been set up that will be linked to each gig that is set up. This will be covered in a later post when setting up users.

At the end of the code you will need to include a mongoose model for the schema:

```js
var Gig = mongoose.model ("Gig", gigSchema);
```

This code will be getting moved to another file later on in the project, but for the time being everything is included in the app.js file. Do not worry, a clean up will be completed soon!

To test out whether this has worked, the following code can be included in the app.js file:

```js
Gig.create(
    {
        name: 'One Gig', 
        image: "https://www.testurl.com/icon.png"
    }, function (err, gig) {
        if (err) {
            console.log(err);
        } else {
            console.log (gig);
        }
    });
```

What this is going to do is create a gig with the ‘name’ and image’ info, and the function pass two arguments (error and gig) if there is an error then the error message will be printed to the console. Else, if the gig went through correctly, then the details will be printed. As you can see, I do not need to include all of the details from the schema in this upload – I can make a gig in the database using only one or two fields.

Now that the ability to create gigs is there, to get all the gigs and display them will require coding a ‘get’ request as below:

```js
app.get("/gigs", function(req, res) {
    Gig.find({}, function (err, allgigs) {
        if (err) {
            console.log (err);
        } else {
            res.render("gigs/all-gigs", {gigs:allgigs})
        }
    })
    
});
```

What this is doing is for the’/gigs’ URL all of the gigs in the database will be found and the ‘all-gigs’ express template will be generated containing all the gigs in the database. That hardcoded array used to test can now be removed.

The ‘post’ request can also now be amended. Whereas before we were pushing the new gig into the hardcoded array, we can now push it to the database and the items in the database will be displayed on the page instead:

```js
app.post("/gigs", function (req, res) {
    //get data from form and add to gigs array
    var name = req.body.name;
    var image = req.body.image;
    var newGig = {name:name, image:image}
    // Crate a new gig and save to the database
    Gig.create (newGig, function (err, newGig) {
        if (err) {
            console.log (err)
        } else {
            res.redirect("/gigs")
        }
    })
});
```

And we have now included data persistence into this website. The functionality will be improved later on in the project, but for now we have something that works.