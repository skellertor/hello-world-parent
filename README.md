
### Hello World with node.js and git submodules
![octocat](http://i.giphy.com/TW6M5r0ncBHcQ.gif)
Git has a handy little way of including children git repositories within a parent repository. One reason we would want to employ this strategy is explained in their documentation.

> It often happens that while working on one project, you need to use another project from within it. Perhaps it’s a library that a third party developed or that you’re developing separately and using in multiple parent projects. A common issue arises in these scenarios: you want to be able to treat the two projects as separate yet still be able to use one from within the other.

Today I'm going to write a simple `Hello World!` app using node.js and git submodules. 

#### Setting things up

- First I'm going to create a git repository named `hello-world-parent`. Open up a CLI and type
```
mkdir hello-world-parent
```
- Open a web browser and browse to github or bitbucket and create a repo of the same name.

- Back to your command line. Initialize it as a git repo by changing directory into it and initializing it
```
cd hello-world-parent
git init
git remote add origin https://github.com/{user}/hello-world-parent.git
```
\* __Be sure to adapt the origin to your repo and user__

- Let's create the index file and add it to git
```
touch index.js
git add index.js
```

- Next let's create a second git repo by repeating the previous steps except were going to name the directory `hello-world-child`

- Instead of creating a stand-alone file we are going to create a directory named `lib`
```
mkdir lib
```

- Inside our `lib` directory we're going to create a `functions.js` file
```
cd lib
touch functions.js
```

- Open the `functions.js` file in your favorite text editor and insert these lines
```
module.exports = {
    print: function (string) {
        console.log(string)
    }
};
```

- Make sure you add the lib directory and all its' contents to git
```
git add lib/
```

- Back to our `hello-world-parent`. Open up `index.js` in a text editor and paste the following lines
```
var lib = require('./hello-world-child/lib/functions');
lib.print('Hello World!');
```

- If you try to run this now it will throw errors because `lib` isn't available yet....

#### Adding git submodule

- Still in the root of the `hello-world-parent` simply type
```
git submodule add https://github.com/{user}/hello-world-child.git
```
\* __be sure to replace user with your repo user name__

- Now the `hello-world-child` repo is available in `hello-world-parent`! Run
```
node index.js
```

Voila! The console prints out "Hello World!". You're probably thinking 
```
¯\_(ツ)_/¯ that's it???
```
Yes, that's it. 
Next tutorial we will cover working on a project with submodules.

