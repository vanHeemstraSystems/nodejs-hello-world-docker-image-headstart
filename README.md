nodejs-hello-world-docker-image-headstart
# NodeJS "Hello World" Docker Image  - Headstart

- Based on "A simple docker setup for hello world nodejs application" at https://medium.com/@sssanjaya/a-simple-docker-setup-for-simple-hello-world-nodejs-application-bcf79bb608a0

- Based on "Dockerizing a Node.js web app" at https://nodejs.org/fr/docs/guides/nodejs-docker-webapp/

## STEP 1: Creating simple nodejs hello world app

Assuming that nodejs installed on your system.
See https://github.com/vanHeemstraSystems/how-to-install-nodejs-npm-on-centos-7

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

### Creating index.js with simple http server that will serve on port 8080

````javascript
//now it loads express module with `require` directive
var express = require('express')
var app = express()
//Define request response in root URL (/) and response with text Hello World!
app.get('/', function (req, res) {
  res.send('Hello World!')
})
//Launch listening server on port 8080 and consoles the log.
app.listen(8080, function () {
  console.log('app listening on port 8080!')
})
````

### Running this app

````javascript
node index.js
````

This will show the log as that app is listening on port 8080. You can stop it with CTRL + C. And check out http://localhost:8080/ in your browser, it will respond with Hello World!. Alternatively if you live in a terminal, you can do:

````javascript
curl http://localhost:8080/
````

which will return the same Hello World! in the terminal.

## STEP 2: dockerize our app

Lets assume docker is installed. See also https://github.com/vanHeemstraSystems/docker-headstart

### Create Dockerfile to root directory

Create an empty file called Dockerfile in the root directory of the (local) repository:

````javascript
touch Dockerfile
````

Open the Dockerfile in your favorite text editor (e.g. vim)

````
vi Dockerfile
````

The first thing we need to do is define from what image we want to build from. Here we will use the latest LTS (long term support) version 10 of node available from the Docker Hub:

````
## it uses node js image alpine version from image registries.
FROM node:10
````

more ...

Ultimately your Dockerfile should look like below:

````javascript
## it uses node js image alpine version from image registries.
FROM node:8.16.1-alpine
## it sets directory in the container to /app to store files and launch our app.
WORKDIR /app
## it copies the app to /app directory with dependencies.
COPY package.json /app
RUN npm install
COPY . /app
## it commands to run our app which is index.js.
CMD node index.js
##  it exposes the port where our app is running that is port 8080.
EXPOSE 8080
````

### To build this image

````javascript
docker build -t web .
````

## STEP 3: using docker compose

NOTE: Requires Python 3 or later version, see also https://github.com/vanHeemstraSystems/python-headstart

````
version: ‘3’ # version of docker-compose
services: # defining service/s
  web: # name of the service
    image: nodejs/hello # image named given
    build: . # directory what to build, here it is root directory
    ports:
      – “8080:8080” # defining port for our app
````

### how to run docker compose

````
docker-compose up ## {-d for detached mode or background}
````

or for new fresh build use this

````
docker-compose up --build ## {--detach for running in background}
````

to remove the container

````
docker-compose rm
````
