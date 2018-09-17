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

describe('#faceButtonEvent', () => {
  it('should take the user to the demo page', () => {
    const props = {
      navigate: () => { },
    };

    const page = new HomePage(props);
    spyOn(page, 'navigate');

    page.faceButtonEvent();
    expect(page.navigate).toHaveBeenCalledWith('demo');
  });
});

```
Run the tests with `./go test:dev`. This will continually run the tests as you make changes to your code.

This test should fail with an output similar to the following:
```bash

FAIL  client/spec/pages/homePage.spec.js
  ● HomePage › #faceButtonEvent › goes to demo page

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

To get this test passing we need to ensure that when a faceButtonEvent from the homepage occurs that navigate is being called with ‘demo’.

The first step is to add the faceButtonEvent() function in the homePage.js file, that parses ‘demo’.

```javascript
  faceButtonEvent() {
    this.navigate('demo');
  }
```
This gives the face button from the home page some logic and will make our test pass.

## Create the page

### ...first, write the test

We want our Demo page to contain the text "This is a demo", so we're going to start by writing a test for that.

In the `client/spec/pages` folder, create a new file called `demoPage.spec.js`.

Add the following test.
```javascript
const DemoPage = require('../../src/js/pages/demoPage');

describe('The Demo Page', () => {
  let watchFace;
  beforeEach(() => {
    document.body.innerHTML = `<div id='watch-face' style='height: 100px; width: 100px;'></div>`;
    watchFace = document.getElementById('watch-face');
  });

  describe('#render', () => {
    it('should contain the correct text', () => {
      const page = new DemoPage();
      expect(page.render()).toContain('This is a demo');
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

### ...now make the test pass
#### create the javascript file

First create a new file called `demoPage.js` inside `client/src/js/pages`

The new page will be extending the basePage.js so we will need to require that at the top, and then use extend it in the class declaration.

```javascript

const BasePage = require('watch-framework').BasePage;

class DemoPage extends BasePage {
  template = require('../../templates/demoPage.hbs');
}

module.exports = DemoPage;

```

#### ...now create the content file

All of our pages require a template property that contains the imported handlebars file which holds html content. The content of the template file can be returned by calling the template method. 

We will create the handlebars file we are importing in the demoPage.js. Create a new file called `demoPage.hbs` inside `client/src/templates` and add this line:

```html
<p>This is a demo</p>
```

To add content to a page, you must edit the handlebars file.

If you'd like to learn a little more about handlebars (.hbs) you can read more [here](https://www.sitepoint.com/a-beginners-guide-to-handlebars/) 

#### final notes

This is the starting point for every new page. We’re creating a new type of view which extends the base page, we then append `module.exports = DemoPage;` to allow the page to be exported and used in other files

```javascript
const DemoPage = require('./pages/demoPage');
```
which imports the page and allow access to the functions within.

### Link the page

So we have our new page demoPage.js and we have our faceButtonEvent() in homePage.js which is trying to navigate there, to link these together we need to require our demoPage in our `routes.js` file.

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


## Time to check it out
Now go to your app's home page and click on the face button.

You should arrive at a new page that displays

```
This is a demo
```

And the tests should pass 💯 🥇 👯 🍡 

If the above is true, congratulations, you've made your first page! 🎉🎉🎉🎉