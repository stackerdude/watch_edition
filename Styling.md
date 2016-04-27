# Generic styles

These should be placed in `client/src/app.scss`

All pages will have a red background

    .page {
        background-color: red;
    }

# Page specific styles

Replace my page with the name of your own page.

Add an id attribute in the page view

    var myPage = Page.extend({

        // ...

        id: 'my-page'

        // ...

    });

Now create a new SCSS file `client/src/styles/pages/_my_page.scss`

Include the file in `client/src/app.scss` with the following code `@import 'pages/my_page';`

Now add your custom styles

    #my-page {

        p {
            color: red;
        }

    }