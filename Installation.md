## Prerequisites

Before you can setup your Proto Watch development environment you need to have Git, NodeJS and CCTray or CCMenu installed and working.

It's up to you how you install these. As long as they work correctly it doesn't matter, but if you're not sure you can follow these instructions.

### Windows Setup Instructions

1. Install [Git](https://desktop.github.com/)
2. Install [Node](https://nodejs.org/download/)
3. Install [CCTray](http://en.freedownloadmanager.org/Windows-PC/CruiseControl-NET-CCTray-FREE.html)
4. Git clone your teams repo

**Now run the initial setup and start the app!**

```shell
cd path_to_team_repo
npm install
npm start
```

You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080)

### OS X Setup Instructions

This article will help you get Node and NPM installed using Homebrew (our preferred way of installing dev tools on OS X)

1. Install [Git](https://desktop.github.com/)
2. [Installing Node.js and npm using Homebrew on OS X](https://thechangelog.com/install-node-js-with-homebrew-on-os-x/)
3. Install [CCMenu](http://ccmenu.org/)
4. Git clone your teams repo

**Now run the initial setup and start the app!**

```shell
cd path_to_team_repo
./go start
```

The script should run your initial setup, then start your app. You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080)

### OS X Docker Setup Instructions

1. Install [Git](https://desktop.github.com/)
2. Install [CCMenu](http://ccmenu.org/)
3. Install [Docker](https://docs.docker.com/docker-for-mac/) for Mac
4. Git clone your teams repo

**Now build and run the app inside a Docker container!**

```shell
cd path_to_team_repo
docker-compose up
```

You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080)

### Windows Docker Setup Instructions

When installing Docker for Windows, make sure you read the installation instructions. Docker for Windows requires 64bit Windows 10 Pro and Microsoft Hyper-V.

1. Install [Git](https://desktop.github.com/)
2. Install [CCTray](http://en.freedownloadmanager.org/Windows-PC/CruiseControl-NET-CCTray-FREE.html) 
3. Install [Hyper-V](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/quick_start/walkthrough_install) on Windows 10
4. Install [Docker](https://docs.docker.com/docker-for-windows/) for Windows
5. Git clone your teams repo

**Now build and run the app inside a Docker container!**

```shell
cd path_to_team_repo
docker-compose up
```
In case localhost:8080 cannot open due to a refused connection, type the following command into your docker terminal:

```
docker-machine ip dev
```
Type the ip address returned instead of 'localhost' into your browser e.g. http://192.168.99.104:8080

You should now be able to view the demo Proto Watch app in your browser at [http://localhost:8080](http://localhost:8080)