**Note!** Data saved into the storage module is not saved to disk. Any information you add to the storage after the app has started will be lost when you close the browser window.

# Loading JSON files in to the storage module

1. Open `client/src/storage/index.js`

2. Require your JSON file `var myData = require("json!./my_data.json");`

3. Modify the Storage function to assign your JSON to a suitable property


        function Storage() {
            // ...
            this.myData = myData;
            // ...
        }


4. Open the view or file you wish to access the data from

5. Require the storage module `const storage = require('../../storage');` (path may vary slightly)

6. Access the data `const foo = storage.myData.foo;`