## Prerequisites

Before you can setup your Proto Watch development environment you need to have Git, NodeJS and CCTray or CCMenu installed and working.

It's up to you how you install these and as long – as they work correctly it doesn't matter – but if you're not sure you can follow these instructions.

### Windows setup instructions
1. Install [Git](https://desktop.github.com/)
2. Install [Node](https://nodejs.org/download/)
3. Install [CCTray](http://en.freedownloadmanager.org/Windows-PC/CruiseControl-NET-CCTray-FREE.html)

### OS X setup instructions

This article will help you get Node and NPM installed using Homebrew (our preferred way of installing dev tools on OS X)

1. [Installing Node.js and npm using Homebrew on OS X](https://thechangelog.com/install-node-js-with-homebrew-on-os-x/)
2. Install [CCMenu](http://ccmenu.org/)

## Setting up your teams project

Now that you have Git and NodeJS installed you are ready to download this Git repo and setup your local development environment.

**Now git clone your teams repo!**

```shell
cd path_to_team_repo
./go start
```

The script should run your initial setup, then start your app. You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080).