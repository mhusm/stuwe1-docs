
# Getting started in Studio Web/Mobile 2019 <!-- omit in toc --> 
- [Our techstack - a short introduction](#our-techstack---a-short-introduction)
  - [Contentful](#contentful)
  - [Vue.js and Sass](#vuejs-and-sass)
  - [Heroku and Node.js](#heroku-and-nodejs)
  - [Dev Server](#dev-server)
  - [Git and Github](#git-and-github)
- [Getting started with the project](#getting-started-with-the-project)
  - [Install Git](#install-git)
  - [Install Node.js](#install-nodejs)
  - [Install Visual Studio Code](#install-visual-studio-code)
  - [Get a Github account](#get-a-github-account)
  - [Clone the project from Github](#clone-the-project-from-github)
  - [Install the project dependencies](#install-the-project-dependencies)
- [Looking at the project in the browser](#looking-at-the-project-in-the-browser)
- [Getting to know VS Code and Project](#getting-to-know-vs-code-and-project)
- [Changing the style](#changing-the-style)
- [Sharing my changes with the my team](#sharing-my-changes-with-the-my-team)
  
## Our techstack - a short introduction
![Techstack](/public/techstack.png "Techstack")

### Contentful
We use [Contentful](https://www.contentful.com/) as our content management system (CMS). In the CMS you can manage any content that is used in your application, for example images and text, but also coordinates for the map. Having a CMS means we don't have to change the code just to add a new image or change a text. Learn more about Contentful in their [Beginner's guide](https://www.contentful.com/r/knowledgebase/contentful-101/).

### Vue.js and Sass
Many modern web application are written in a JavaScript framework like [Vue.js](https://vuejs.org/). These framework try to make it easier for developers to create user interfaces. Vue.js is similar to React and Angular, but has a reputation of being easy to learn. We also use [Sass](https://sass-lang.com/) which is an extension of CSS.
 
### Heroku and Node.js
To make your application available to people on the internet, you have to run a web server somewhere. We use [Heroku](https://dashboard.heroku.com/) which provides a platform to run Node.js. [Node.js](https://nodejs.org/en/) runs our server-side code. Depending on your project, you may not have a lot of code running on the server, but you need at least some code that delievers your HTML, CSS and Javascript files to the browsers.

### Dev Server
While you are working on your project, it would be inconvenient if you had to send all your changes to Heroku to see if your code works. For that reason we use a local development server that runs on your machine. 

### Git and Github
Git helps us to work with other people on the same project by providing version control. But even if you work alone, it is good to use version control. It allows you to go back to a working state, if you mess something up. Git can be quite complex to use, but we will start with the basics in this class. It is integrated in the IDE that we will use, so you don't have to use the command line if you don't want to. A project in Git is called a repository.
There are many tutorial for how to use Git, for example [this one](https://www.atlassian.com/git/tutorials).
We store our Git repositories here on [Github](https://github.com/). Github can be connected to Heroku so that whenever you push a change to Github, Heroku deploys your new code.

## Getting started with the project
The goal of the following steps is to have to project set up on your machine so you can start working.

### Install Git
* [Git](https://git-scm.com/)

### Install Node.js
* [Node.js](https://nodejs.org/en/), choose the LTS version.

### Install Visual Studio Code
[Visual Studio Code](https://code.visualstudio.com/) is an integrated development environment (IDE) for web development. It has editors for writing code but also helps you with other tasks like using Git. 
* Install VS Code (unless you already have your preferred IDE).

### Get a Github account
* If you don't have a Github account, create one.
* (Optional) sign up for the [student pack](https://education.github.com/pack).
* Generate an SSH key following [these instructions](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
* Ask your team mate who created the project to add you as a project member on Github.

### Clone the project from Github
* Open VS Code.
* Open the folder where you want to have your project.
* Go to the project on Github and press the green *Copy or Download* button. Copy the SSH URL.
* In VS Code open a terminal (View=>Terminal). In a terminal we can execute commands. We use the $ sign to say something should be executed in the terminal. Don't copy the $, but everything that follows it.
* Execute the following command in the terminal: *$ git clone <your project url>*
* Now you should have your project in VS code and you can look at the files.

### Install the project dependencies
The project uses libraries (like Vue.js) that have to downloaded and installed.
* Change into the project folder: *$ cd <project folder name>*
* Run the following command: *$ npm install*

## Looking at the project in the browser
* To start the development server run> *$ npm run serve*
* This will output a URL in the form of *http://localhost:8080/*
* Open the  URL in a browser.
* **TADA!**

## Getting to know VS Code and Project
We will look at VS Code and project together in the class. You can also have a look at this [introduction to VS Code](https://code.visualstudio.com/docs/getstarted/userinterface).
* Install the Vue.js plugin.

## Changing the style
* In the project open the file *App.vue*
* In this file, you can change CSS that will be applied to the whole application.
* Make some changes to the CSS, for example, change the background-color
* Have a look at the application in the browser.

## Sharing my changes with the my team
Git tracks your changes and VS code displays this information. Now that you have changed the project, you should see a blue icon with a number on the right.

![Git changes](/public/changes.PNG)

* Go the source control view (by clicking on the icon)
* Here you can see all the files that have changed or have been added/removed.
* Select the file that you have changed and review the changes.
* If you are happy with all your changes, hover with over the *Changes* line, where a *+* should appear. Press the *+*.
* Your changes are now staged. That means ready to be commited.
* Add a message. This helps your team mates (and yourself in the future) understand why you made changes. 
* Commit your changes by pressing the checkmark button. Or changes are now commited to your local Git repository, which is on your computer.
* To share the changes with your team and to pull in new changes from your team, press the Synchronize button at the bottom of the screen 
![Git synchronize](/public/sync.PNG)
* Remember to regularly pull in changes from your team.
* If you and your team mate change the same piece of code, there can be conflicts that need to be merged. VS Code also helps us with that. You will have to decide, which changes you want to take from which user. 

