For the purpose of this exercise we'll create a new page called "Demo".

## The Starting point

Create a new file called `demoPage.js` inside `client/src/js/pages`

Your new page will be based on the generic pageView so you need to add the following lines

    'use strict';

    var Page = require('../framework/page');
    var demoPage = Page.extend({

        id: 'demo'

    });

    module.exports = demoPage;

This is the starting point for every new page. What's going on here is you're creating a new type of view which extends the default page and giving it a custom ID. The ID attribute is used in a few different ways, the most important thing is to make sure that all your pages have a unique id attribute. If the ID attribute is based on the name of the page this you're generally unlikely to run in to any issues.

## Adding some content

In order to display some content you'll need to add render method.

If we wanted the page to display the text `demo page` we could do the following:

    render: function() {
        this.$el.html("demo page");
        return this;
    }

## Using templates

Returning strings in your render method gets messy quickly, especially once you start adding more content and using HTML tags.

Add a template attribute to your page object, to keep things readable keep it near the ID attribute. It should look like this:

     template: require('../../templates/pages/demo.hbs')

Now it's time to add your template. In `client/src/templates` make a file called `demo.hbs` with the the following content:

    <h1>This is a demo</h1>
    <p>What a great page!</p>

The last thing to do is update your render method to return the template contents instead of a string:

    render: function() {
        this.$el.html(this.template());
        return this;
    }

## Passing data to templates

The best thing about templates is you can pass data to them, this is allows you to make variations of a page without having to create multiple versions.

Change the render method in `client/src/js/pages/demoPage.js` to look like this:

    render: function() {
        this.$el.html(this.template({name: 'John Smith'}));
        return this;
    }

Change the contents of the template to look like this:

    <h1>{{name}}'s page</h1>
    <p>What a great page!</p>




