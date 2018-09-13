# Creating Your First Notification

The watch is capable of creating different types of notifications. For this exercise we'll be creating a "Demo" notification that pops up saying "This is a demo notification"

 ✨ **(S U R P R I S E !)** ✨

 We'll be using TDD AGAIN. This is your life now...

Here are the principles again for your reference:

* Write a failing test
* Write just enough code to make the test pass
    * YAGNI - You Ain't Going To Need It
* Refactor
* Write the next failing test
* Rinse and repeat

### Write a failing test
We want our Demo notification to say "This is a Demo Notification: [message]" where [message] is our custom message sent through the form. 

Create the file `client/spec/notifications/DemoNotification.spec.js`

Let's add a test to check for the phrase "This is a Demo Notification:"

```javascript

const DemoNotification = require("../../src/js/notifications/DemoNotification");

describe("DemoNotification", () => {
    describe("#render", () => {
      it("should render my page correctly", () => {
        const notification = new DemoNotification();
        expect(notification.render()).toContain("This is a Demo Notification:");
      });
    });
});

```

Run the test with `./go test:dev`. 
The test should fail with an output that looks something like this:

```bash

FAIL  client/spec/notifications/DemoNotification.spec.js
  ● Test suite failed to run

    Cannot find module '../../src/js/notifications/DemoNotification' from 'DemoNotification.spec.js'

    > 1 | const DemoNotification = require("../../src/js/notifications/DemoNotification");
        |                          ^
      2 | 
      3 | describe("DemoNotification", () => {
      4 |     describe("#render", () => {

      at Resolver.resolveModule (node_modules/jest-resolve/build/index.js:221:17)
      at Object.<anonymous> (client/spec/notifications/DemoNotification.spec.js:1:26)

```

### Make the test PASS ! (...yeah!!)

#### create the javascript file
We need to define our Demo Notification now to make this test pass 😤
All notifications will extend our Base Notification which is essentially a page (a type of page).

Create the file `client/src/notifications/DemoNotification.js`

```javascript

const BaseNotification = require("watch-framework").BaseNotification;
const NotificationHub = require("watch-framework").NotificationHub;

module.exports = class DemoNotification extends BaseNotification {
  template = require("../../templates/DemoNotification.hbs");
};

```

#### create the content
Like our pages, we use handlebars to hold our html content in a template property. We call the template method to return its contents aka our demo notification message.

Create a new file `client/src/templates/DemoNotification.hbs` and add our notification like so:

```html
This is a Demo Notification:
<div>
  {{message}}
</div>
```

Like every other page we need to export it to be used in other files. In this case we can append `module.exports = DemoNotification` or export it straight when declaring the class as we did in our javascript file `module.exports = class DemoNotification extends BaseNotification`

```javascript
const DemoNotification = require('./notifications/DemoNotification');
```

### Link the Notification

We're almost there !! Now all we have to do is link it to be displayed in the dropdown list of options.

In `notifications.js` we import our new notification and add it to the list. You should have something like this:
```javascript

const AlertNotification = require('./notifications/AlertNotification');
const DemoNotification = require('./notifications/DemoNotification');

const notifications = [
  {
    type: "demo",
    label: "Demo",
    defaultValue: "Our First Notification!",
    view: DemoNotification,
  },

```

### Let's check out how it looks...
On the home page there should now be our Demo option in the dropdown list and when you send it to the watch...
It should now display with some message
```
This is a Demo Notification: [message]
```

Congratulations !!
But you know what...It kinda looks a bit boring 💩 
So let's make it look a little... cuter! 🌸🍉💕(◠︿◠✿)

### Styling the Notifications Page
All the styling for our notifications is contained in `./framework/styles/notification.scss`
The black background of the pop-up really isn't that appealing. Let's change the background colour to something lighter and also put a shiny, pink border around it!
Something like this...:
```css
#notification-container {
  background-color: #f2ece4;
  color: #036;
  border-color: #b37399;
  box-shadow: 0 0 10px #b37399;
```

Hmm...🤔🤔 it's not that cute. something is missing!!

### Adding an Image
There is only one person who can save us now...
![](https://www.photospng.com/uploads/pusheen-on-the-phone-graphic.png)
  **^ ^ ^ PUSHEEN**

Let's add Pusheen or an image of your choice to the `client/src/images` folder.

In our handlebars page add it in the image tag and you should have something like this:
```html
<img src="../images/busyPusheen.png" height="100">
```

Let's see how it looks!
Purrfect ~ ♡ 
(Hahahahahahaha get it? because Pusheen is a cat and cats PURR)

Good job!!