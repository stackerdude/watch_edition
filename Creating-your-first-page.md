For the purpose of this exercise we'll create a new page called "Demo".

## Create a new link on your home page

Go to `client/src/js/pages` and edit the file called `homePage.spec.js`.

```
buttonEvents: {
    right: 'goToContacts',
    top: 'scrollUp',
    bottom: 'scrollDown',
    left: 'goToMyDemoPage'
}

```
## Test Driven Development

The principles of Test Driven Development are straightforward:

* Write a failing test
* Write just enough code to make the test pass
* Refactor
* Write the next failing test
* Rinse and repeat

### Write a failing test

Open `client/spec/pages/homePage.js`

Add the following test:
```javascript
describe('left', function () {
    it('should take the user to the demo page', function () {
        spyOn(window.App, 'navigate');
        page.configureButtons();
        eventHub.trigger('left');
        expect(window.App.navigate).toHaveBeenCalledWith('demo');
    });
});
```
This test should fail along lines similar to the the following:
```bash
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 33 of 35 (1 FAILED) (skipped 2) (0.054 secs / 0.035 secs)
TOTAL: 1 FAILED, 32 SUCCESS

1) should take to my demo page
     The Home Page button event handlers left
     Expected spy navigate to have been called with [ 'demo'  ] but it was never called.
```
## So let's create the method...

In the file `homePage.js` add the following method:
```javascript
goToMyDemoPage: function() {
    window.App.navigate('demo');
},
```
## A common starting point
Almost every page starts the same way.

First create a new file called `demoPage.js` inside `client/src/js/pages`

Your new page will be based on the generic pageView so you need to add the following line
```javascript
'use strict';

var Page = require('watch_framework').Page;
var demoPage = Page.extend({

    id: 'demo'

});

module.exports = demoPage;
```
What you're doing here is creating a new type of page which extends the functionality of the default page in the framework.

Now in `client/src/js/pages/index.js` you need to add your page to the exports:
```javascript
module.exports = {
    // existing content...
    demo: require('./demoPage')
}
```
This is the starting point for every new page. What's going on here is you're creating a new type of view which extends the default page and giving it a custom ID. The ID attribute is used in a few different ways, the most important thing is to make sure that all your pages have a unique id attribute. If the ID attribute is based on the name of the page this you're generally unlikely to run in to any issues.

## Check it out
Now go to your app's home page and click on the left button.

You should arrive at a new page. But there is no content.

Let's fix that now.

## First, write the test

We want our Demo page to contain the text `This is a demo`, so we're going to start by writing a test for that.

In the `client/spec/pages` folder, create a new file called `demoPage.spec.js`.

Add the following test.
```javascript
'use strict';

var DemoPage = require('../../src/js/pages/demoPage'),
    page;

describe('The Demo Page', function() {
    
    beforeEach(function() {
        page = new DemoPage();
    });
    
    describe('rendering', function() {
        it('should produce the correct HTML', function() {
            page.render();
            expect(page.$el).toContainText('This is a demo');
        });
    });
});

```
Run all the tests by entering the command:

`./go test`

We expect our new test to fail along lines something like this:
```bash
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 34 of 36 (1 FAILED) (skipped 2) (0.043 secs / 0.037 secs)
TOTAL: 1 FAILED, 33 SUCCESS

1) should produce the correct HTML
     The Demo Page rendering
     Expected ({ 0: HTMLNode, context: HTMLNode, length: 1 }) to contain text 'This is a demo'.
```
## Adding some content

In order to display some content you'll need to add render method.

We want the page to display the text `This is a demo` so we will do the following:
```javascript
render: function() {
    this.$el.html("This is a demo");
    return this;
}
```
It's best to put your render method towards the end of the file to keep things readable.

Now click on the left button again (or refresh the page) - and you should see your text 'demo page'.

Run the tests again.

This time, they should pass.

## Using templates

Returning strings in your render method gets messy quickly, especially once you start adding more content and using HTML tags.

### First write a test

We're going to use a template to display the following HTML:
```html
<h1>This is a demo</h1>
<p>What a great page!</p>
```
Go back to `demoPage.spec.js` and edit our previous test so it reads:
```javascript
describe('rendering', function() {

  it('should produce the correct HTML', function() {
    page.render();

    expect(page.$el).toContainText('This is a demo');
    expect(page.$el).toContainHtml('<p>What a great page!</p>');

  });
});
```
Run the tests. Our new test should fail something like this:
```bash
PhantomJS 2.1.1 (Mac OS X 0.0.0): Executed 34 of 36 (1 FAILED) (skipped 2) (0.096 secs / 0.072 secs)
TOTAL: 1 FAILED, 33 SUCCESS

1) should produce the correct HTML
     The Demo Page rendering
     Expected ({ 0: HTMLNode, context: HTMLNode, length: 1 }) to contain html '<p>What a great page!</p>'.
```
## Get the tests to pass

Add a template attribute to your page object, to keep things readable keep it near the ID attribute. It should look like this:
```javascript
template: require('../../templates/pages/demo.hbs')
```
Now it's time to add your template. In `client/src/templates` make a file called `demo.hbs` with the the following content:
```html
<h1>This is a demo</h1>
<p>What a great page!</p>
```

The last thing to do is update your render method to return the template contents instead of a string:
```javascript
render: function() {
    this.$el.html(this.template());
    return this;
}
```
Run the tests again. This time, they should pass.

## Passing data to a template

The best thing about templates is you can pass data to them, this is allows you to make variations of a page without having to create multiple versions.

### Write a new test

In `demoPage.spec.js` add:

```
 
```

Change the render method in `client/src/js/pages/demoPage.js` to look like this:
```javascript
render: function() {
    this.$el.html(this.template({name: 'John Smith'}));
    return this;
}
```
Change the contents of the template to look like this:
```html
<h1>{{name}}'s page</h1>
<p>What a great page!</p>
```
