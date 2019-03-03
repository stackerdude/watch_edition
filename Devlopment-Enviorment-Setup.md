## Setting up the Devlopment Enviorment 
Your devlopment enviorment, also know as an IDE(Intergrated Devlopment Enviorment) 
is where you will build all of the components of the watch app. The tool we are using 
is called Gitpod. Gitpod is a cloud based IDE that allows teams to work on a common git 
repository. Using a tool like this makes the setup of your IDE much easier as difference in 
devlopment machines (Mac vs Windows vs Linux) will not cause issues. 

### Setting up Gitpod
1. Add `gitpod.io#` to the start of the github link of your teams repo  
    `gitpod.io#https://github.com/twlevelup/syd-2019-s1-<teamname>`
2. Click `Login with Github and launch workspace`
3. Authorize Typefox, (the makers of gitpod) to access your github account. This allows them to 
make commits on your behalf. 
4. After this, there should be a small load time and you will be redirected to the online IDE

### The IDE

![Alt text](gitpod_ide.png?raw=true "Title")

#### The Editor (the red sqaure)
This is where your will write the actual code that control the watch application 
#### The Terminal (the blue square)
This is where you can run commands that will test, compile and run you application. From a more technical perspective, 
this is a `bash` terminal running  in a docker enviorment. Test this our by running 
1. `./go install`  
This will install all of the dependencies for the project.  
You will get more familiar with the terminal as you progress through the tutorials and have more some hands on
experience

### The Project Explorer (the purple square)
This shows you all the files in the git repository. You will mainly be working in the `client` folder, 
but feel free to look at any of the other files. One of the amazing things about git is that is nearly 
impossible to make a change that you can't undo