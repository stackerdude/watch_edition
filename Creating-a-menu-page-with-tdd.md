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
'use strict';

var MenuPage = require('../../src/js/pages/menuPage'), App = require('../../src/js/app'), eventHub = require('watch_framework').EventHub,
  page;

window.App = App;

describe("The Menu Page", function() {

  beforeEach(function() {
    page = new MenuPage();
  });

  describe('menulist', function() {
    it('should contain 5 items', function() {
      page.render();
      expect(page.collection.length).toEqual(5);
    });
  });

  describe('rendering', function() {
    it('should produce the correct HTML', function() {
      page.render();
      expect(page.$el).toContainText("thing: up");
    });
  });

});

```


## options.js

```javascript
'use strict';

var Option = require('../models/option');

var Options = Backbone.Collection.extend({
  model: Option
});

module.exports = Options;

```

# option.js

```javascript
'use strict';

var Option = Backbone.Model.extend({
  defaults: {
    direction: "up",
    action: "click"
  }
});

module.exports = Option;
```

## homePage.js

```javascript
'use strict';

var Page = require('watch_framework').Page;

var homePage;
homePage = Page.extend({

  id: 'home',

  template: require('../../templates/pages/home.hbs'),

  buttonEvents: {
    right: 'goToContacts',
    top: 'scrollUp',
    bottom: 'scrollDown',
    face: 'goToMenuPage'
  },

  goToContacts: function () {
    window.App.navigate('contacts');
  },

  scrollUp: function () {
    $('#watch-face').animate({scrollTop: '-=70px'});
  },

  scrollDown: function () {
    $('#watch-face').animate({scrollTop: '+=70px'});
  },

  goToMenuPage: function () {
    window.App.navigate('menu');
  },

  render: function () {
    this.$el.html(this.template());
    return this;
  }

});

module.exports = homePage;
```
## index.js

```javascript
'use strict';

module.exports = {
  404: require('./404Page'),
  team: require('./teamPage'),
  home: require('./homePage'),
  contacts: require('./contactsPage'),
  eventsList: require('./eventsList'),
  eventDetails: require('./eventDetails'),
  menu: require('./menuPage')
};
```

## menuPage.js

```javascript
'use strict';

var Menu = require('watch_framework').Menu;
var OptionsCollection = require('../collections/options');

var menuList;

var menuPage = Menu.extend({

  id: 'menu',

  template: require('../../templates/pages/menu.hbs'),

  initialize: function() {
    this.collection = new OptionsCollection;
  },

  render: function() {

    menuList = this.collection;
    menuList.add([
      {
        direction: "up",
        action: "thing"
      },
      {
        direction: "down",
        action: "another thing"
      },
      {
        direction: "left",
        action: "thing"
      },
      {
        direction: "right",
        action: "another thing"
      },
      {
        direction: "screen",
        action: "thing"
      }
    ]);

    var directions = menuList.pluck("direction");
    var actions = menuList.pluck("action");

    this.$el.html(this.template(
      {
        option1: actions[0],
        option2: actions[1],
        option3: actions[2],
        option4: actions[3],
        option5: actions[4],
        value1: directions[0],
        value2: directions[1],
        value3: directions[2],
        value4: directions[3],
        value5: directions[4]
      }
    ));

    return this;
  }
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
