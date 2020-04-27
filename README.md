nodejs-hello-world-docker-image-headstart
# NodeJS "Hello World" Docker Image  - Headstart

Based on "A simple docker setup for hello world nodejs application" at https://medium.com/@sssanjaya/a-simple-docker-setup-for-simple-hello-world-nodejs-application-bcf79bb608a0

## STEP 1: Creating simple nodejs hello world app

Assuming that nodejs installed on your system.

### Installation
create new directory and initialize npm:

````javascript
mkdir nodejs-hello
cd nodejs-hello
npm init
````

confirm default values with enter.

npm will create a package.json which holds the dependencies of our app and following code will add express framework as a dependency.

````javascript
npm install express --save
````
