You can specify the behaviour of each button on the watch when the page is active (visible to the user) by implementing (overriding them from the basePage) the functions below.

When the user clicks one of the buttons, top, bottom, left, right, or face the corresponding method will be called.

```javascript
  rightButtonEvent() {
  }

  leftButtonEvent() {
  }

  topButtonEvent() {
  }

  bottomButtonEvent() {
  }

  faceButtonEvent() {
  }
```
for example the leftButtonEvent() is overridden on the client/src/js/pages/ContactsPage/index.js
```javascript
  leftButtonEvent() {
    this.navigate('/');
  }
```