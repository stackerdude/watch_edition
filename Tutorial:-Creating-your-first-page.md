For the purpose of this exercise we'll create a new page called "Demo".

## Test Driven Development

The principles of Test Driven Development are straightforward:

* Write a failing test
* Write just enough code to make the test pass
  * YAGNI - You Ain't Going To Need It
* Refactor
* Write the next failing test
* Rinse and repeat


### Write a failing test

Open `client/spec/pages/homePage.spec.js`

Add the following test:
```javascript

describe('#leftButtonEvent', () => {
  it('should take the user to the demo page', () => {
    const props = {
      navigate: () => { },
    };

    const page = new HomePage(props);
    spyOn(page, 'navigate');

    page.leftButtonEvent();
    expect(page.navigate).toHaveBeenCalledWith('demo');
  });
});

```
Run the tests with `./go test`

This test should fail along lines similar to the the following:
```bash

FAIL  client/spec/pages/homePage.spec.js
  ● HomePage › #leftButtonEvent › goes to demo page

    expect(spy).toHaveBeenCalledWith(expected)

    Expected spy to have been called with:
      ["demo"]
    But it was not called.

      at Object.<anonymous> (client/spec/pages/homePage.spec.js:58:29)
          at new Promise (<anonymous>)
          at <anonymous>
      at process._tickCallback (internal/process/next_tick.js:160:7)

```

## Get the test to pass

To get this test passing we need to ensure that when a leftButtonEvent from the homepage occurs that navigate is being called with ‘demo’.

The first step is to add the leftButtonEvent() function in the homePage.js file, that parses ‘demo’.

```javascript
  leftButtonEvent() {
    this.navigate('demo');
  }
```
This gives the left button from the home page some logic and will make our test pass.

## Create the page

Almost every page starts the same way.

First create a new file called `demoPage.js` inside `client/src/js/pages`

The new page will be extending the basePage.js so we will need to require that at the top, and then use extend it in the class declaration.

```javascript

  const BasePage = require('./BasePage');

  class DemoPage extends BasePage {
  template() {
    return `
      return `hello demoPage`;
    `;
  }
  }

  module.exports = DemoPage;

```

### Link the page

All of our pages require a template which allow us to return html content to display.

This is the starting point for every new page. We’re creating a new type of view which extends the base page we then append the module.exports = DemoPage; to be able to access this classes return content outside of this file.

So we have our page and our leftButtonEvent() is trying to navigate to our demo page, to link these together we need to require our demoPage in our routes file.

```javascript
const HomePage = require('./pages/homePage');
const ContactsPage = require('./pages/ContactsPage/');
const TeamPage = require('./pages/teamPage');
const FourOhFour = require('./pages/404Page');
const DemoPage = require('./pages/demoPage');

module.exports = {
 '/': HomePage,
 'contacts': ContactsPage,
 'team': TeamPage,
 '404': FourOhFour,
 'demo': DemoPage
};
```

## Check it out
Now go to your app's home page and click on the left button.

You should arrive at a new page. But there is no content.

Let's fix that now.

## Lets create some content!

### ...first, write the test

We want our Demo page to contain the text "This is a demo", so we're going to start by writing a test for that.

In the `client/spec/pages` folder, create a new file called `demoPage.spec.js`.

Add the following test.
```javascript
const DemoPage = require('../../src/js/pages/demoPage');

let page;

describe('The Demo Page', () => {
  beforeEach(() => {
    page = new DemoPage();
  });

  describe('rendering', () => {
    it('should produce the correct HTML', () => {
      page.render();
      expect(page.$el).toContainText('Hello, i am the demopage');
    });
  });
});
```
Run all the tests by entering the command:

`./go test`

We expect our new test to fail along lines something like this:
```bash
FAIL  client/spec/pages/demoPage.spec.js
  ● The Demo Page › rendering › should produce the correct HTML

    expect(string).toContain(value)

    Expected string:
      "hello demoPage"
    To contain value:
      "Hello, i am the demopage"

      at Object.<anonymous> (client/spec/pages/demoPage.spec.js:9:31)
          at new Promise (<anonymous>)
          at <anonymous>
      at process._tickCallback (internal/process/next_tick.js:160:7)

```
## Adding some content

In order to display some content you'll need to add template method.

We want the page to display the text "Hello, i am the demopage" so we will do the following to the template() function in demoPage.js:

```javascript
template() {
  return `Hello, i am the demopage`;
}
```

Now click on the left button again (or refresh the page) - and you should see your text 'Hello, i am the demopage'.

Run the tests again.

This time, they should pass.

## Using templates

Returning strings in your template method gets messy quickly, especially once you start adding more content and using HTML tags.

### First write a test

We're going to use a template to display the following HTML:
```html
<h1>This is a demo</h1>
<p>What a great page!</p>
```
Go back to `demoPage.spec.js` and edit our previous test so it reads:
```javascript

describe('rendering', () => {
  it('should produce the correct HTML', () => {
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
const template = require('../../templates/pages/demo.hbs');

const demoPage = Page.extend({

  id: 'demo',

  template,

});
```
Now it's time to add your template. In `client/src/templates/pages` make a file called `demo.hbs` with the the following content:
```html
<h1>This is a demo</h1>
<p>What a great page!</p>
```

The last thing to do is update your render method to return the template contents instead of a string:
```javascript
render() {
    this.$el.html(this.template());
    return this;
}
```
Run the tests again. This time, they should pass.

## Passing data to a template

The best thing about templates is you can pass data to them, this is allows you to make variations of a page without having to create multiple versions.

### Write a new test

In `demoPage.spec.js` add a new test:
```javascript
it('should pass a variable to the template', () => {
  page.render();

  expect(page.$el).toContainHtml('<h2>Welcome, John Smith!</h2>');
});
```
Run the tests and watch them fail.

Change the render method in `client/src/js/pages/demoPage.js` to look like this:
```javascript
render() {
    this.$el.html(this.template({name: 'John Smith'}));
    return this;
}
```
Change the contents of the template to look like this:
```html
<h1>This is a demo</h1>
<h2>Welcome, {{name}}!</h2>
<p>What a great page!</p>
```
