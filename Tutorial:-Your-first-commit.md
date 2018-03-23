Everyone on the team should complete this exercise as soon as they have access to the team repo.

## Instructions

1. Set up the project: [Installation Instructions](https://github.com/twlevelup/watch_edition/wiki/Installation)
2. Git pull to get the latest code ```git pull --rebase```ask a trainer if you're not sure what ```--rebase``` does
3. In the `client/spec/pages` folder, create a new file called `teamPage.spec.js`.
4. Add the following test that checks for your name in the team page 
```javascript

const TeamPage = require('../../src/js/pages/teamPage');

let page;

  describe('template', () => {
    it('should contain the correct text', () => {

      page = new TeamPage();
      expect(page.template()).toContain('Bob');
    });
  });

```
5. Run  
```./go pre-commit``` (OS X)  
```npm -s run test``` (Windows)   
This will run the pre-commit checks - something should fail.
6. Fix the failing test by adding your name and your pairs name to the team page in ```client/src/templates/teamPage.hbs```
7. Run the tests again ```./go test``` – everything should pass.

## Before you push

1. Check the CI build (see below), do not pull unless it's is green!
2. Run ```git pull --rebase```
3. Fix any merge conflicts
4. Run
```./go pre-commit``` (OS X)
```npm -s run test``` (Windows)
5. Repeat steps 2-5 until all tests have passed and all conflicts have been resolved

## Push your code 

7. Run ```git add -p``` to add your changes. 
8. Run ```git commit -m "[COMMIT MESSAGE]``` (Set your commit message to ```"[STORY NO/STORY DESCRIPTION][Bruce/Sheila] Initial commit"``` replacing ```[Bruce/Sheila]``` with, you guessed it, you and your pair's name.)
9. Git pull to get the latest changes ```git pull --rebase```
10. ```./go pre-commit```
11. Push your changes ```git push origin master```

## Check the build status

To view the build status and get notifications about the build status:

Add the following XML config to CCTray or CCMenu on your dev machine

	https://circleci.com/gh/twlevelup/watch_edition.cc.xml

You can also access the CI server and view the status of the build here [Circle CI](https://circleci.com/gh/twlevelup/watch_edition)