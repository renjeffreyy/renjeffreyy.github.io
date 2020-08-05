# Angular

## Getting Started

- make sure you have node and npm installed
- install the angular cli using the below
  - `npm install -g @angular/cli`
- in the directory that you want to put your project run the command to create a new project. replace my-app with the name of your app
  - `ng new my-app`
- to launch the server for your application go to the directory of your project(in the terminal) and run ng serve
  - `cd my-app`
  - `ng serve --open`
    - --open just opens a browser with the server to the local host of you app .if you already have a browser open you can just run ng serve

## How an angular app gets loaded and started

- Angular is a framework that allows us to serve single page applications
  - the file that is being served is the index.html
- Angular uses the selector to replace a piece of html with our componenet. in inital creation it is the app root. it replaces the html with the tempalte from that component.
- When our application is first strating up
  - angular injects a script to the html for our main.ts file.
  - in our main.ts file the file calls a function that bootstraps the app module. when our application starts it passes the app module
  - in the appmodule there is a bootstrap array that shows all the components that should be known to angular upon the time it analyzes our index.html
  - upon first strting the app we only have app componenet in the array
  - int he app.componenet.ts file the app takes that selector and replaces with with our template html

## In-app navigation

## Components

- components are a key feature of angular. you build you entire application by composing it from a couple of components
- allows us to split up our web page into reusable parts
- each componenet has its own html code, styling, business logic
- we add our components to the app component. the app componenet is our root component.

## How to create component Manually

- in our app folder create another folder with the name of your component.
- basics of the component are the main type script file, html, and style file(css,scss)

example of what our component will look like

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html',
})
export class ServerComponent {}
```

**pipes**

**Streams**

Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. The Angular HTTP client, HttpClient, is a built-in way to fetch data from external APIs and provide them to your app as a stream.
