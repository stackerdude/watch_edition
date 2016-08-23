# Generic styles

These should be placed in `client/src/app.scss`

All pages will have a red background

    .page {
        background-color: red;
    }

# Page specific styles

Given the example page:

    var myPage = Page.extend({

        // ...

        id: 'my-page'

        // ...

    });

1. Create a new SCSS file `client/src/styles/pages/_my_page.scss`

2. Include the SCSS file in `client/src/app.scss` with the following code `@import 'pages/my_page';`

3. Add your custom styles using the selector `#my-page` to limit the scope.

    #my-page {

        p {
            color: red;
        }

    }