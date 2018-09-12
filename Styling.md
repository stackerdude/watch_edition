# Generic styles

You can create styles which will apply to any page.

1. Open `client/src/styles/app.scss`

2. To give all pages a red background by default add the following code
```
#watch {
    background-color: red;
}
```

# Page specific styles

You can find an example of this in `client/src/main.scss`

```
@import './styles/pages/home.scss'

...
```

1. Create a new SCSS file `client/src/styles/pages/my_page.scss`

2. Include the SCSS file in `client/src/main.scss` with the following code `@import './styles/pages/my_page.scss';`

3. Add your custom styles using the selector `#my-page` to limit the scope.
```
#my-page {
    p {
        color: red;
    }
}
```