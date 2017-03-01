# Use Test Driven Development to create a menu page

## Create the following new files:

```bash
client/spec/pages/menuPage.spec.js
client/src/js/collections/options.js
client/src/js/models/option.js
client/src/js/pages/homePage.js
client/src/js/pages/index.js
client/src/js/pages/menuPage.js
client/src/templates/pages/menu.hbs
```

## MenuPage.spec.js
```javascript
const MenuPage = require('../../src/js/pages/menuPage');
const App = require('../../src/js/app');
const eventHub = require('watch_framework').EventHub;

let page;

window.App = App;

describe('The Menu Page', () => {

    beforeEach(() => {
        page = new MenuPage();
    });

    describe('menulist', () => {
        it('should contain 5 items', () => {
            page.render();
            expect(page.collection.length).toEqual(5);
        });
    });

    describe('rendering', () => {
        it('should produce the correct HTML', () => {
            page.render();
            expect(page.$el).toContainText("first option: up");
        });
    });

});

```


## options.js

```javascript
const Option = require('../models/option');
const Backbone = require('backbone');


const Options = Backbone.Collection.extend({
    model: Option,
});

module.exports = Options;

```

## option.js

```javascript
const Backbone = require('backbone');

const Option = Backbone.Model.extend({
    defaults: {
        direction: 'up',
        action: 'click',
    },
});

module.exports = Option;
```

## homePage.js

```javascript
const Page = require('watch_framework').Page;

const template = require('../../templates/pages/home.hbs');
const $ = require('jquery');

const homePage = Page.extend({

    id: 'home',

    template,

    buttonEvents: {
        right: 'goToContacts',
        top: 'scrollUp',
        bottom: 'scrollDown',
        face: 'goToMenuPage',
    },

    goToContacts() {
        window.App.navigate('contacts');
    },

    scrollUp() {
        $('#watch-face').animate({
            scrollTop: '-=70px'
        });
    },

    scrollDown() {
        $('#watch-face').animate({
            scrollTop: '+=70px'
        });
    },

    goToMenuPage() {
        window.App.navigate('menu');
    },

    render() {
        this.$el.html(this.template());
        return this;
    },

});

module.exports = homePage;
```
## index.js

```javascript
const page404 = require('./404Page');
const team = require('./teamPage');
const home = require('./homePage');
const contacts = require('./contactsPage');
const eventsList = require('./eventsList');
const eventDetails = require('./eventDetails');
const menu = require('./menuPage');

module.exports = {
  404: page404,
  team,
  home,
  contacts,
  eventsList,
  eventDetails,
  menu,
};

```

## menuPage.js

```javascript
const Menu = require('watch_framework').Menu;
const OptionsCollection = require('../collections/options');
const template = require('../../templates/pages/menu.hbs');

let menuList;

const menuPage = Menu.extend({

    id: 'menu',

    template,

    initialize() {
        this.collection = new OptionsCollection();
    },

    render() {
        menuList = this.collection;
        menuList.add([{
                direction: 'up',
                action: 'first option',
            },
            {
                direction: 'down',
                action: 'second option',
            },
            {
                direction: 'left',
                action: 'third option',
            },
            {
                direction: 'right',
                action: 'fourth option',
            },
            {
                direction: 'screen',
                action: 'fifth option',
            },
        ]);

        const directions = menuList.pluck('direction');
        const actions = menuList.pluck('action');

        this.$el.html(this.template({
            option1: actions[0],
            option2: actions[1],
            option3: actions[2],
            option4: actions[3],
            option5: actions[4],
            value1: directions[0],
            value2: directions[1],
            value3: directions[2],
            value4: directions[3],
            value5: directions[4],
        }, ));

        return this;
    },
});

module.exports = menuPage;
```

## menu.hbs

```html
<h1>This is our menu page</h1>
<div class="menu">
    {{option1}}: {{value1}}
</div>
<div class="menu">
    {{option2}}: {{value2}}
</div>
<div class="menu">
    {{option3}}: {{value3}}
</div>
<div class="menu">
    {{option4}}: {{value4}}
</div>
<div class="menu">
    {{option5}}: {{value5}}
</div>

```
