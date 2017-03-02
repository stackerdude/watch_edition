A View With Buttons provides has a buttonEvents property which allows you to specify the behaviour of each button on the watch when the page is active (visible to the user).

When the user clicks one of the buttons, top, bottom, left, right, or face the corresponding method will be called.

## Example

      buttonEvents: {
        face: 'select',
        top: 'goUp',
        bottom: 'goDown',
        left: 'goLeft',
        right: 'goRight'
      },

      select() { // ... },

      goUp() { // ... },

      goDown() { // ... },

      goLeft() { // ... },

      goRight() { // ... },