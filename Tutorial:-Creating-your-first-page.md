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

Add the following test above the test for `#rightButtonEvent`:
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
Run the tests with `./go test:dev`. This will continually run the tests as you make changes to your code.

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

  describe('template', () => {
    it('should contain the correct text', () => {
      expect(page.template()).toContain('This is a demo');
    });
  });
});

```
Check your test runner. If it is not running, you can start it by executing `./go test:dev`.

We expect our new test to fail along lines something like this:
```bash
 FAIL  client/spec/pages/demoPage.spec.js
  ● Test suite failed to run

    Cannot find module '../../src/js/pages/demoPage' from 'demoPage.spec.js'

    > 1 | const DemoPage = require('../../src/js/pages/demoPage');
      2 | 
      3 | let page;
      4 | 
```

Almost every page starts the same way.

First create a new file called `demoPage.js` inside `client/src/js/pages`

The new page will be extending the basePage.js so we will need to require that at the top, and then use extend it in the class declaration.

```javascript

const BasePage = require('watch-framework').BasePage;

class DemoPage extends BasePage {
  template() {}
}

module.exports = DemoPage;

```
All of our pages require a template function, which is why we have an empty placeholder. The return of this function is what the app looks to insert into the watch face html and allow it to be displayed.

This is the starting point for every new page. We’re creating a new type of view which extends the base page, we then append `module.exports = DemoPage;` to allow the page to be exported and used in other files

```javascript
const DemoPage = require('./pages/demoPage');
```
Which imports the page and allow access to the functions within.

### Link the page

So we have our new page demoPage.js and we have our leftButtonEvent() in homePage.js which is trying to navigate there, to link these together we need to require our demoPage in our `routes.js` file.

```javascript
const HomePage = require('./pages/homePage');
const ContactsPage = require('./pages/ContactsPage');
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

You should arrive at a new page. But it will show 'undefined' as the template function we added above doesn't return anything.

Let's fix that now.

## Lets create some content!

In order to display some content we will need the template function to return something.

We want the page to display the text "This is a demo" so we will do the following to the template() function in demoPage.js:
```javascript
template() {
    return `This is a demo.`;
}
```
It's best to put your template function towards the end of the file to keep things readable.

Now click on the left button again (or refresh the page) - and you should see your text 'This is a demo'.

Run the tests again.

This time, they should pass.