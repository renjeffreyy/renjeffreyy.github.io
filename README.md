# Jeff's Declassified Code Survival Guide

## Table of Contents

- [React](#React.js)
- [Redux](#Redux)
- [Node](#Node.js)
- [CSS](#CSS)
- [SCSS or SASS](#SCSS-or-SASS)
- [Deploying Your Website](#Deploying-your-website)


---

# React.js

# Redux
[React Redux Documentation](https://react-redux.js.org/introduction/quick-start)

**Getting started**

install redux into your project directory
> npm install react-redux

add the provider `<Provider />` into your app. this makes the redux store available to your entire app

Into the file containing your root element(usually index.js).  import provider from react-redux
 the file should look something like the below
 ``` javascript
 import React from 'react'
import ReactDOM from 'react-dom'

import { Provider } from 'react-redux'
import store from './store'

import App from './App'

const rootElement = document.getElementById('root')
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  rootElement
)
 ```
**Note** the provider doesnt have to be in the root element. it just has to wrap around all the react componenets that you want to have access to the store. 

I prefer to put the provider in my app.js.

the below also works
``` javascript
const App = () => {
  return (
    <Provider store={store}>
      <Router>
        <Fragment>
          <Navbar />
        </Fragment>
      </Router>
    </Provider>
  );
};
```

**create your store**

- import create store and apply middleware. create store creates the store and applymiddleware lets you use middleware in your store. 

- if you want to use redux devtools in your browser you can install redux-devtools-extenstion as a dependency

- thunk makes it so you can easily pass yiur actions in the connect method that will be wrapping each of our componenets

- set your initial state
- create a middleware variable to hold all the middleware that you are going to use in your project

The Below is an example of what your store should look like


``` javascript
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevtools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};

const middleware = [thunk];

const store = createStore(
  rootReducer,
  initialState,
  composeWithDevtools(applyMiddleware(...middleware))
);

export default store;
```

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

# CSS

# SCSS or SASS

**CSS on steroids**

if you are using vs code a lot of people recomend that we add the scss compliter extension. this is becaus ebrowsers can not read scss. they can only read regular css

What can we do in SASS
- we can create variables
  - we use the $ to create a variable. put the $ in front of your variable name
  - ex: ```$primaryButtonColor :red;```
  - this works like any other variable in javascript/programming language
- maps
- nesting
  - instead of creating new blocks for css elements within other css elements we can next them into the parent

example: 

```scss 
header {
    background:red;
    button{
        background:blue;
    }
}
  ```
  to add hover, before, after, etc we add the & symbol before the keyword within the element we want to style
  
example:

```scss
button {
    background:red;
    &::after {
        content: "hello";
    }
}
```



- mixins
  - similiar to functions in a programming language we can put several styles into a mixin and use them like puzzle pieces and put those styles where we need them. this helps us not repeat code.
example of mixin:
``` scss
@mixin flexCenter {
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}
```
then in the element we are styling we call `@inclide flexCenter();`
if we want to use the mixin but change something we can define a variable within the parenthesis of the mixin and use it within the mixin 

example 

``` scss
@mixin flexCenter($direction) {
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:$direction;
}

@include flexCenter(center)
```


- extensions
  - we can have elements inherit the styles of another by using extensions
  - `.contact{ @extends header;}` and if we want to change the styles of the extensions we can just write them following the extensions
- operations
  - we can do operations in scss + - / *
- imports
  - we can import our our scss from different files. this can help us organize our code



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

