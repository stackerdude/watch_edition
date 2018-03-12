Everyone on the team should complete this exercise as soon as they have access to the team repo.

## Instructions

1. Set up the project:

[Installation Instructions](https://github.com/twlevelup/watch_edition/wiki/Installation)
2. Git pull to get the latest code ```git pull --rebase```ask a trainer if you're not sure what ```--rebase does```
3. Have a look at the test in ```teamPage.spec.js```
4. Edit the test so that it says your name in the <your name here>.  
5. Run the below commands
```./go pre-commit``` (OS X)  
```npm -s run test``` (Windows)   

This will run the pre-commit checks - something should fail.
6. Fix the failing test by adding your name to the team page in ```team.hbs```
7. Run the pre-commit checks again – everything should pass. ```./go pre-commit```
8. Set your commit message to ```"[TASK][your_name/pairs_name] check-in dance initial commit"``` replacing ```your_name``` with, you guessed it, your name.
9. Git pull to get the latest changes ```git pull --rebase```
10. ```./go pre-commit```
11. Push your changes ```git push```
12. Repeat for the other person in your pair.

You may need to pull in the latest changes before you can push your own. Follow the [Continuous Integration](https://github.com/twlevelup/watch_edition#continuous-integration) steps.
