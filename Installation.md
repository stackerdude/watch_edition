## Prerequisites

Before you can setup your Proto Watch development environment you need to have Git, NodeJS and CCTray or CCMenu installed and working.

It's up to you how you install these. As long as they work correctly it doesn't matter, but if you're not sure you can follow these instructions.

### Windows Setup Instructions

1. Install [Git](https://git-scm.com/downloads)
2. Install [Node](https://nodejs.org/en/) (the 'current' version)
3. Install [CCTray](http://sourceforge.net/projects/ccnet/files/CruiseControl.NET%20Releases/CruiseControl.NET%201.8.5/)
4. Git clone your teams repo - further instructions on cloning a repository can be found [here](https://help.github.com/articles/cloning-a-repository/)
5. Add `https://circleci.com/gh/twlevelup/{your_repo_name}.cc.xml` to CCTray

### OS X Setup Instructions

This article will help you get Node and NPM installed using Homebrew (our preferred way of installing dev tools on OS X)

1. Install [Git](https://git-scm.com/downloads)
2. [Installing Node.js v10 and npm using Homebrew on OS X](https://www.dyclassroom.com/howto-mac/how-to-install-nodejs-and-npm-on-mac-using-homebrew)
3. Install [CCMenu](http://ccmenu.org/)
4. Git clone your teams repo - further instructions on cloning a repository can be found [here](https://help.github.com/articles/cloning-a-repository/)
5. Add `https://circleci.com/gh/twlevelup/{your_repo_name}.cc.xml` to CCMenu
   
**Now run the initial setup and start the app!**

```shell
cd path_to_team_repo
npm install
./go start
```

The script should run your initial setup, then start your app. You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080)
