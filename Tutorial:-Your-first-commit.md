Everyone on the team should complete this exercise as soon as they have access to the team repo.

## Instructions

1. Set up the project: [Installation Instructions](https://github.com/twlevelup/watch_edition/wiki/Installation)
2. Git pull to get the latest code ```git pull --rebase```ask a trainer if you're not sure what ```--rebase does```
3. Add a new test to ```teamPage.spec.js``` that checks for your name in the team page
4. Run  
```./go pre-commit``` (OS X)  
```npm -s run test``` (Windows)   
This will run the pre-commit checks - something should fail.
5. Fix the failing test by adding your name and your pairs name to the team page in ```teamPage.js```
6. Run the tests again – everything should pass. ```./go test```
7. Set your commit message to ```"[TASK][Bruce/Sheila] Initial commit"``` replacing ```your_name``` with, you guessed it, your name.
8. Git pull to get the latest changes ```git pull --rebase```
9. ```./go pre-commit```
10. Push your changes ```git push```
11. Repeat for the other person in your pair.

You may need to pull in the latest changes before you can push your own. Follow the [Continuous Integration](https://github.com/twlevelup/watch_edition#continuous-integration) steps.


1. 
