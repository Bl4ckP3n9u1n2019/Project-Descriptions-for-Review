# For Reviewer
## How Grading Works
We have created a document that gives rubric specific instructions to help you grade this project.You can access the document here: [Health Tracker - Best Practices](https://docs.google.com/document/d/1RewU2A88u9AWJ-y70FJl-4bPxAUhTPBp8iUPvM5HoQM/pub)

It is VERY IMPORTANT that you read this document before you begin evaluating projects. In order to meet specifications every review must follow the guidelines given in the document.

#Project Overview
![Project Roadmap](http://i.imgur.com/9FOltK1.jpg)

**This is an optional project - not required to complete your Nanodegree.**

Using Backbone, you will develop a single page app that tracks the user's calorie intake, and optionally, other health-related metrics. Typing food names into the search field will display a list of matching foods as provided by the health API. Users will be able to select an item from the list, and the item will be added to the list of foods the user is tracking. The total calorie count will also update to reflect the new daily total.

## Why this Project?
It's important that web developers have experience with multiple organizational libraries and frameworks. This experience is important to employers, and helps reiterate that there are many different tools for organizing applications.

## How does this help my Career?
* Employers are looking for developers who have experience with multiple libraries and frameworks, and who are willing and able to learn new ones.
* This project will further your experience building applications, specifically with Backbone

# Project Details
## How will I complete this Project?
1. Review our <a href="https://www.udacity.com/course/ud990-nd" target="_blank">Backbone course</a>.
2. Write code required to get a project started
3. Write code required to add a search bar to the application
4. Write code required to query a health API when the user searches, and return the results in a list (<a href="https://developer.nutritionix.com/docs/v1_1" target="_blank">Nutritionix has a good one</a>)
5. Write code required to add an item to the data store when clicked
6. Write code required to show the items in the data store, and to display the total number of calories

If you use Firebase and run into issues, check out the Potential Issues section below.


## Helpful Resources

* <a href="http://backbonejs.org/#Getting-started" target="_blank">Getting Started</a>
* <a href="http://tutorialzine.com/2013/04/services-chooser-backbone-js/" target="_blank">Building a Simple Backbone App</a>
* <a href="http://arturadib.com/hello-backbonejs/" target="_blank">Hello Backbone</a>
* <a href="http://addyosmani.github.io/backbone-fundamentals/#backbone-basics" target="_blank">Diving Deeper with Backbone</a>
* <a href="http://addyosmani.github.io/backbone-fundamentals/#exercise-1-todos---your-first-backbone.js-app" target="_blank">Building a Todo Application from Scratch</a>
* <a href="http://addyosmani.github.io/backbone-fundamentals/#exercise-2-book-library---your-first-restful-backbone.js-app" target="_blank">Building a Book Library App from Scratch</a>
* <a href="http://backbonejs.org/docs/backbone.html" target="_blank">Backbone.js Annotated Source Code</a>


## Potential Issues
If you decide to use Firebase to store your data instead of localStorage and you see the below error in the console, the following explanation might be helpful for you.

<pre><code>Uncaught Error: Firebase.child failed: First argument was an invalid path: "undefined". 
Paths must be non-empty strings and can't contain ".", "#", "$", "[", or "]"</code></pre>

<hr>

When creating a model in your collection, you might write something like the following:

<pre><code>var foodItem = new app.FoodItem({
  name : this.model.get('name'),
  calories : this.model.get('calories')
});

app.FoodItems.create(foodItem);
</code></pre>

_(this is a toy example, so don't copy and paste it directly)_


This makes sense. We're creating a backbone `FoodItem` model, and putting it into our `FoodItems` collection. But sending a newly instantiated model in will likely cause the operation to fail if you're using Firebase, and you'll see that above error in the console.

It's a particularly nasty error because it doesn't point you directly to the problem. If you spend time debugging this, you might trace the error up to the line `app.FoodItems.create(foodItem)` in our toy example above.

So what is that line doing? It's passing `foodItem`, our model item, into `app.FoodItems.create` to add it to the collection. If we log foodItem out, we'll find that there's much more in it than `name` and `calories`. That's because Backbone is tracking all kinds of other things when we tell it to make a new `FoodItem`. We don't want Firebase to track all the other keys that Backbone creates for new models for two reasons: First, there's something in Backbone's model that Firebase doesn't like. Maybe one ot hose extra keys that Backbone added contains one of the prohibited characters that the error warned us about. And secondly, we only want to store `name` and `calories` because that's all we care about.

So, it we pass an object literal with _only_ the data that we actually want to store, we don't get the error anymore.

<pre><code>app.FoodItems.create({
  name : this.model.get('name'),
  calories : this.model.get('calories')
});
</code></pre>

So there's an exploration of this error, what's happening, and one way to get around it. Feel free to explore more on your own!

# Evaluation and Submission
## Evaluation
Your project will be evaluated by a Udacity reviewer according to the rubric below. Be sure to review it thoroughly before you submit. All criteria must "meet specifications" in order to pass. 
![r1](http://lh3.googleusercontent.com/pYDrp2rshl5F28ZGBx27lfiDJPQChZysIvuW6p887wSOi38goOUM7yRUEZjWzVYYjMNAd7QFA-kJvbUPCVA=s0#w=975&h=427)
![r2](http://lh3.googleusercontent.com/osb0WwK-AHGftwrqFAzbo5jo57hOsMgbICi0n9beOTphh48t5IGlI_6t_NFsYiwrbz3XFgiZzQwXbPn2Lp0=s0#w=975&h=433)
![r3](http://lh3.googleusercontent.com/MIKvA3xXn-g_S0dBRJYF40bKNC9BhGtnjmSvtw3D8T3PWLZCAWpmcejsLbeVFT5uhBTQS5j6UVjhj1Deo2w=s0#w=975&h=280)

## Submission
1. If build tools are used, submit both your source and production code in the same repository in separate directories.  These directories are usually named ```src``` and ```dist``` respectively.
2. If build tools are used the gulp or grunt.js file as well as the package.json file must be included in the submission.
3. If build tools are used, the instructions for building the project and running the tool must be included in the README.md. You may find the short [Writing READMEs course](https://www.udacity.com/course/writing-readmes--ud777) helpful.
4. The node_modules directory may contain thousands of files and should not be contained in the submission. See the forum post [how to remove node_modules directory from Github repository](https://discussions.udacity.com/t/how-to-remove-node-modules-directory-from-github-respository/40929) for instructions.
5. The master branch is the default Github repository branch. If you wish to submit another branch, you'll need to set it as the [new default branch](https://help.github.com/articles/setting-the-default-branch/) inside your Github repository.
6. When you're ready to submit your project go back to your <a href="https://www.udacity.com/me" target="_blank">Udacity Home</a>, click on Project 5.2, and we'll walk you through the rest of the submission process. Due to the high volume of submissions we receive, please allow up up to **7 business days** for your evaluation to be returned.
7. If you are having any problems submitting your project or wish to check on the status of your submission, please email us at **frontend-project@udacity.com** or visit us in the <a href="http://discussions.udacity.com" target="_blank">discussion forums</a>.


## What's Next?
You will get an email as soon as your reviewer has feedback for you. In the meantime, review your next project and feel free to get started on it or the courses supporting it!
