# Jeff's Declassified Code Survival Guide

## Table of Contents

- [Git](#Git)
- [Javascript Concepts](#Javascript-Concepts)
- [React](#React.js)
- [Angular]()
- [Redux](#Redux)
- [Node](#Node.js)
- [CSS](#CSS)
- [SCSS or SASS](#SCSS-or-SASS)
- [Deploying Your Website](#Deploying-your-website)

---

# Git

[helpful link to git commands](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)

**Delete a branch locally**

in Terminal type `git branch -d <branch name>`

if you want to force the branch to delete use a capital D `git branch -D <branch name>`

**Create new branch when working on master**

- make sure all the changes from master have been pulled into your project use `git pull`
- create the branch on your local machine and switch in this branch
  - `git checkout -b <name of your branch>`
- push your branch to github
  - `git push origin <name of your branch>`


# Javascript Concepts

### Intersection Observer
Helps determine the visibility of elements in the DOM. When you have an element inside of a parent element or viewport, the observer observes changes in the intersection of the element relative to the parent element. 

Used for
- infinite scroll
- lazy loading images
- animations


### Import Export

Import
- when importing a module that has an export default, the name that you import it as can be your choosing because it will reference the default export of the module
- when using {name} to import, Only the specified part of the module will be imported. Names must match
- You can use * to import everything from the module
- You can change the name of an import by specifying the changed name of your import
  ```javascript
  import {name as Nammmmee} from './someFile.js'
  ```

Exports
- Use export default to set a default export for your module
- 
#### Event Loops



# React.js

### JSX
JSX is similiar to HTML but it is javascript that gets compiled into HTML with React.createElement(). A react function that takes in the JSX and creates those html elements
- to add styling classes to your JSX use className instead of class. class is a reserved word in JS so we need to use className to create classes.

### Javascript within JSX
you are able to write javascript code within your jsx by wrapping your javascript code with single curly brackets within your jsx. 

For Example
```javascript
const name = "Jeffrey"

const Component = ()=>{
  return (
    <div>
    <h1>hello my name is {name}</h1>
    </div>
  )
}
```

### App / root component
The Root component is the component that contains the other react components within your applicaion. If you used **create-react-app** to create your application. App.js will be your root component. 

The index.js file is the file that takes your app.Js component and injects it into your index.html.


### file/ folder naming in react
Start the folder names of your react componenet swith a captital letter.

### Creating functional components

- Import React from the react package
- Using Es6 conventions, create a const variable that holds your arrow function. The component is a function that returns JSX. 
- export the function as a default
- import the functionl component into the file that you want to use it in using a relative path.

The below is an example of a basic functional component

```Javascript

Import React from 'react'

const Person = ()=>{

}

export default Person

```


# Node.js

---

### **Nodemon**

nodemon is a usefull library that allows your server to start up whenever you save your code. On default you would have to restart your server in the terminal every time you make changes to the server code. With nodemon it restarts automatically. I believe you can use this with other programming languages not just javascript

### **Installation**

I have nodemon globally installed. the below is how you do it

> npm install -g nodemon

If you want it to just to be a development dependency you can run the below in your terminal

> npm install --save-dev nodemon

---

### **Create package.json file**

The package.json file holds some basic information about your application as well as metadata about your app. It will also manage all the dependencies of your application. Any additional package you install using NPM (Node Package Manager) will be managed here as well.

Use the below command to created the file

> npm init

you can add -y to answer yes to all the questions it asks you about your project

> npm init -y

## Express.js

install express

> npm install express

bring express into your app by requiring it in the index.js file. The below is a basic express server

```javascript
const express = require('express');

const app = express();

const PORT = process.env.PORT || 4000;

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

**Sending things in express**
express response object lets us send responses back to the client. some things we can send are

- strings
- json
- files
- headers
- status codes
- the body

Response methods

- res.send(body)
  - we can use the `res.send` method to send an HTTP response
  - the body can be a buffer object, string, plain object, or an array
- res.sendStatus(statusCode)
  - we can send http response status codes. we just have to pass in a number

# CSS

# Common Libraries

- **express** : framework for backend node.js development
- **express validator**: Express Validator is an Express middleware library that you can incorporate in your apps for server-side data validation.
- **bcrypt** : used to encrypt passwords
- **config** : It lets you define a set of default parameters, and extend them for different deployment environments (development, qa, staging, production, etc.).
- **gravatar**:
- **json web token** : creates a token for validation to authenticate users
- **mongoose** : Mongoose provides a straight-forward, schema-based solution to model your application data. It includes built-in type casting, validation, query building, business logic hooks and more, out of the box. used to create models and interact with mongodb Database
- **request**
- **concurrently** : allows you to ren dev server and front end dev server at the same time

# Databases

## ** MongoDB**

## **Mongoose**

[Link to medium article that talks more about mongoose and react](https://medium.com/@KLMcGrath2/mongoose-schemas-in-react-f5c0afa5a47d)

Mongoose helps you interact with Mongodb databases. Models are the rock band — it is how your API creates, queries, updates, and deletes from your database. Anything goes in the Model, there is no structure to the data.

A mongoose Schema is the drummer in the band — it defines the structure of the document, the default values, its validators and other things. The Schema makes using the data more usable.

The Schema is applied to the Model, and mongoose applies this to the MongoDB database.

### **Schemas**

# Deploying your website

## Heroku
Heroku is a good hosting service that has a free tier that allows you to host projects either for free or for a very low cost

### Heroku Dynos
Heroku hosts your code in what they call **Dynos**.  
- Dynos are containers for your code within their machines. 
- If you do not pay for their more premium plans then your dynos will be on shared machines. The performance of your project may be impacted by the other projects that are also hosted on that machine

### Heroku Routing
When a lot of requests come to your site Heroku Routing directs the traffic to your dynos. **Heroku has a random routing algorith.** Meaning that if you have multiple dynos and many request coming in at once Heroku will randomly assign one of your dynos to handle your request. Since it doesnt balance the workload, this could potentially lead to bottlenecks for bigger appliations. If you only have 1 dyno then this doesnt really matter.

## Performance testing
Software performance testing is a means of quality assurance. It involves testing software applications to ensure they will performa well under their expected workload

**Performance testing checks**
- speed - determines whether the application responds quickly
- scalability - determines the maximum user load the software applicaton can handle
- stability - Determines if the application is stable under varying loads

**API Performance Metrics**
- response time
- throughput - requests per second, request payloads, maximum operating capacity
- traffic composition - average and peak concurrent users
- database - number of concurrent connections, cpu utilization, read and write iops (input output operations per second), memory consumption, disk storage requirements
- errors - handling, failing rates

### Load Testing
Load tests allow you to see how your application performs under real-world traffic. Use load testing to test a new feature at scale before it launches, or to prepare your app for traffic growth.

-  Add seed data
    -  create seeds that reflect the variety of data in production
    -  avoid using production data for load testing as it may be sensative or impact real users

### Stress testing

Stress testing involves testing an application under **extreme** workloads to see how it handles high traffic or data processingl The objective is to identify the breaking point of an application.

### Volume testing
With volume testing a large amount of data is populated into a database to observe how the application handles large amounts of data. 

### Scalability testing
helps determine the projects effictiveness in growing to  support an increase in crease in userload. This helps with planning capacity additions to your software system.


## Scalability 

 Scalability of an application can be measured by the number of requests the application support simultaneously.

 ### Horizontal vs vertical scaling
 
 ---
 # Security
 
 ## DOS
 **Denial of service attack** is when someone denies a user from interacting with a network ressource by sending a lot of requests to the server in an attempt to over load the server. comes from a single source (IP address)
 
## DDOS
**Distributed Denial of service attack** is when the denial of service attack comes from multpile sources  making it so you cant stop the attack from just blocking a single source. 

## Validating User Inputs
