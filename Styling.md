# Generic styles

You can create styles which will apply to any page.

1. Open `client/src/styles/app.scss`

2. To give all pages a red background by default add the following code

        #watch {
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