# Techstack Setup for Studio Web/Mobile 2019 <!-- omit in toc --> 
- [About this guide](#about-this-guide)
- [Install Node.js or check your version](#install-nodejs-or-check-your-version)
- [Install Git](#install-git)
- [Creating a Vue.js project](#creating-a-vuejs-project)
- [Using the Vue CLI service](#using-the-vue-cli-service)
- [Setting up your development environment](#setting-up-your-development-environment)
- [Creating a simple HTTP-Server for the deployment](#creating-a-simple-http-server-for-the-deployment)
- [Adding Google maps](#adding-google-maps)
  - [Getting an API key](#getting-an-api-key)
  - [Adding a map to your Vue application](#adding-a-map-to-your-vue-application)
- [Integrating the Contentful CMS](#integrating-the-contentful-cms)
  - [Creating an account and a project](#creating-an-account-and-a-project)
  - [Integrating Contentful in your Vue application](#integrating-contentful-in-your-vue-application)
- [Push your project to Github](#push-your-project-to-github)
- [Setup Heroku](#setup-heroku)

## About this guide
These setup instructions are for students of [Digital Ideation](https://www.hslu.ch/en/lucerne-school-of-information-technology/degree-programs/bachelor/digital-ideation/) taking the Studio Web/Mobile 2019 course. The following figure illustrates our stack.
![Techstack](/public/techstack.png "Techstack")

You need to do the setup once per group. The following instructions assume that you have a technical background. To see the instructions on how to use the projects that your team mate has created go the [Getting started guide](getting_started.md).

Instructions starting with *$* should be typed into a command line. 
You can open a command window on Windows by pressing the windows key and typing *cmd*.

## Install Node.js or check your version

* Install Node.js from [https://nodejs.org/en/](https://nodejs.org/en/)
* If you have it installed already, check the version in the command line: $ node -v 
* Make sure you have at least version 10, if not update.

## Install Git
Git helps your collaborte with your team mates and provides version control.

* https://git-scm.com/downloads


## Creating a Vue.js project

We are going to use the [Vue Command Line Interface (CLI)](https://cli.vuejs.org/guide/creating-a-project.html#vue-create).
Run the following commands in the command line.
* $ npm install -g @vue/cli
* $ vue ui
* In the UI choose a name and a location for the project.
* Choose manual presets.
* In addition to the defaults, also add the Router and CSS Preprocessors
* Pick Sass and ESlint + Prettier options

## Using the Vue CLI service

Dev server with Hot-Module-Replacement (HMR)
* $ npm run serve

Build production ready bundle
* $ npm run build


## Setting up your development environment
The goal of this step is to have an IDE setup so that you can work productively.

* Install [Visual Studio Code](https://code.visualstudio.com/) or use your favourite IDE
* Open your project folder
* Open the file *App.vue*
* Install a Vue.js Plugin
* Start the dev server from a terminal within VS Code
* Look at the folders *components* and *views*
* Update the message in the file home.vue and look at the change in the browser.

## Creating a simple HTTP-Server for the deployment
The goal of this step is to have a simple HTTP server for static files that we can use when we deploy the app.
We are going to use Node.js with the [Express framework](http://expressjs.com/).

* $ npm install express -save
* In the top level of your project folder create a file named *server.js*
* Add the following code to the file

```javascript
let express = require('express');
let app = express();
let http = require('http').Server(app);
let path = require('path');
let serveStatic = require('serve-static');
let fs = require('fs');

// serve the index.html as starting page
app.get('/', function (req, res) {
    res.sendFile(path.join(__dirname, "dist", "index.html"))
});

// serve all files in dist
app.use(express.static('dist'));

http.listen(process.env.PORT || 8090, function(){
    console.log(`listening on *: ${http.address().port}`);
});
```

* $ node server.js
* Check in the browser that the website is served

## Adding Google maps
The goal of this step is to add Google Maps to your project.

### Getting an API key
* We have received a Google Cloud Platform Education Grant. Follow the instructions in the Email received from me to get your credit.
* Go to the [Google Cloud platform console](https://console.cloud.google.com/)
* Create a new project
* Enable the Maps Javascript API
* Go to *Credentials* and create an API Key
* Restrict the API to *localhost* (later you will also need to add Heroku here). Only websites that are listed here can access Google Maps with your key. This step is needed to make sure that no one else can use your key and your free quota on their website.
* In the file *index.html* add the following line inside the `head`: `<script src="https://maps.googleapis.com/maps/api/js?key=API-Key"></script>` 
* Replace `API-Key` with your API key from Google.

### Adding a map to your Vue application
* In the file *home.vue* add a `<div id="map"></div>`. This is where the map will be displayed.
* Give the map a height and a width using CSS 
```html
<style scoped lang="scss">
#map {
  height: 80vh;
  width: 80vw;
}
</style>
```
* Initialize the map and set it to a location
```javascript
export default {
  name: "home",
  components: {
    HelloWorld
  },
  mounted: function(){
    const element = document.getElementById("map")
    const options = {
        zoom: 14,
        center: new google.maps.LatLng(47.071467, 8.277621)
    }
    this.map = new google.maps.Map(element, options);
  }
};
```
* Check in the browser, if the map is showing up

## Integrating the Contentful CMS
The goal of this step is to have the Contentful CMS integrated in your project. With a CMS, content (images, texts) can be created independent from the code. This way, you don't have to re-deploy the project whenever the content changes. We are going to use [Contentful](https://www.contentful.com/) as a cloud-based, headless CMS. In headless CMS, no templates are used in the CMS, instead the data is sent over a Rest-API to our Vue.js client.

### Creating an account and a project
* Go to the [Contentful website](https://www.contentful.com/) 
* Create an account
* Create an organization
* A sample project is created for you


### Integrating Contentful in your Vue application
* $ npm install contentful-management --save
* Import the contenful library in *main.js*
```javascript
import {createClient} from 'contentful-management'
```

* Create a content managment access token from the *API Keys* settings menu
* Configure the client with your access key. We add the contentfulClient to the window Object to make it available globally in our application.
```javascript
window.contentfulClient = createClient({
    accessToken: '64d6a750c7ae5a7c93603911e56166b198ce5ab94be05261848e8a280ba8972c'
});
```
* Get data from your Contenful space and print it to the console.
```javascript
window.contentfulClient.getSpace('7la5sjify8om')
.then((space) => space.getEnvironment('master'))
.then((environment) => environment.getEntries()) 
.then((response) => console.log(response.items))
.catch(console.error)
```
* Open the console in the browser and look at the ouptut.

## Push your project to Github
* Create an account at 
* Optionally (but recommended) get the [Student pack](https://education.github.com/pack). This gives you free private repos and a free plan with Heroku
* Make sure that your HSLU email address is set in your account to get the student pack.
* Create and add an SSH key for your machine (so you don't have to enter your password on every commit or update) using [these instructions](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
* Create a new repository
* Add your project to the repo using [these instructions](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/). Vue-CLI has already initialized the project so you can start with step 5. You can also do these steps through the UI of VS code except for step 8.

## Setup Heroku
The goal of this step is to have your project run in the cloud so that it can be accessed anywhere from the internet. We are going to use [Heroku](https://www.heroku.com/) as a service provider.

* Create a Heroku account. Check if you can use the student pack to get more free service.
* Create a new App.
* In your *package.json* set the Node.js engine
```javascript
  "engines": {
    "node": "10.x"
  },
```
* Add a start script to  your *package.json*
```javascript
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "start": "node server.js",
    "lint": "vue-cli-service lint"
  },
```

* Commit and push your changes
* As a deployment method choose Github
* Look for your user name and project
* Enable automatic deploys
* Open the app in the browser and make sure that your website is displayed.
* Add your Heroku app as a referrer for Google Maps



