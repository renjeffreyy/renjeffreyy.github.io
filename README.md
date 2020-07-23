# Jeff's Declassified Code Survival Guide

## Table of Contents

- [Git](#Git)
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

# React.js

# Node.js

---

### **Nodemon**

nodemon is a usefull library that allows your server to start up whenever you save your code. On default you would have to restart your server in the terminal every time you make changes to the server code. With nodemon it restarts automatically. I believe you can use this with other programming languages not just javascript

### **Installation**

I have nodemon globally installed. the below is how you do it

> npm install -g nodemon

If you want it to just to be a development dependency you can run the below in your terminal

> nom install --save-dev nodemon

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
