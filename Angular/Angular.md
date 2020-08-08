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
  styleUrls:['./server.component.css]
})
export class ServerComponent {}
```

**@Component decorator**

- with the decorator @component we tell type script that it is not a normal class. it is a component. the decorator enhances our class.
- The decorator is not something that typescript knows so you have to import it. we import the decorated component from angular core
- We pass an object into the comonent decorator with information about our component.
- **selector** : inside the selector we pass on the name of the placeholder in our html that we want to inject our html template into. we can either use attributes or classes. can not uses Ids. but we will mostly use the html looking selector
- **templateUrl** this is the location of the template of the file that you want to inject into the selector
- **template:** instead of having a seperate file four our html tempalte we can rwite in directly within the template preperty. this is more for if you dont have a lot of code to write.
- **styleUrls** : this is where we put the file path to our styles. this takes in an array and you can add multiple files of css
- **styles:** this also takes in an array also and you can write your styles in directly as strings

### How to use Cli to generate component

- We can use the command `ng generate component name_of_component`. The Short hand for it is `ng g c name_of_component`

### What is the app module and ngModule

it is a bundle of functionality of our app. it gives angular the information of what features your app has and use. normally it is an empty type script class but we use the @ngModule decorator imported form @angular/core

**what do each of these object keys in ngModule do**

- **Bootstrap**: tells angular what components angular needs to be aware of when starting up
- **Declarations**: Here we register new componenets and let Angular know that the components that we want it to use exist. Angular won't look for your components so you will have to declare them here. You would also need to import the components into the file
- **Imports**: since Angular is made up of a bunch of modules this is where we import other modules that we want to use in the app module. int he example below we import the forms,http, and browser module. this gives us functionality of usng forms, http, and browser
- **provider**:

The below is an example of appmodule for your reference

```typescript
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule, HttpModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

### Databinding

Databinding is how we can communicate data to our html.
ways we can databind

- **String Interpolation**: {{data}}
  - the expression in the curly braces can only return a string value so we can only put in things that will return a string value. we can even use a method that returns a string but we cant use block expressions life if else. we can use ternery
  - we can use numbers because numbers can be easily converted to strings
  - we can use methods that return strings also in the curly braces
- **property binding:** [property]='data'
  - allows you to bind html properties and set their value to whatever data yu want to set it to.
  - we can bind to directives and the properties of your own components
- **event binding** (event)= 'expression'
  - we put the name of the event that we are going to listen for in the parenthesis and once that event occurs on the element it runs the defined function
  - passing \$event into theevent binding function gives us access to the event data emitted with the event
- **two way data binding:** [(ngModel)]="data"

  - FormsModule is required for two way data binding
  - you need to make sure it is in the imports of the app module and that you import it from @angular/forms

### Directives

Directives are instructions in the dom
we can add attribute like keybords into our html to manipulate the dom
**built in directives**

- NGIF. performs conditional rendering. we add \*ngIf to the element we want to manipulate
  - `*` is required when directives change the structure of the DOM
  - for ngIF the element will not display if we pass in something false
  - to use the else feature we can add an else attrivute followed by the name of the replacing componenent. You will need to use an ng-tempalte with a marker with `#name_of_else`
- ngStyle
  - allows us to change the style of the element. we put ngStyle in Brackets to bind to the ngStyle property and set it equal to a value/function in javascript
  - allows us to dynamically update the styles
  - unlike strucural directives that add or remove elements, attribute directives only change the elements they were placed on.
- ngClass
  - allows us to dynamically add or remote css classes
  - only adds the class if a met condition is true
- ngFor

  - structural directive so we need to include the star in the syntax
  - `*ngFor="let logItem of log; let i = index"`
  - we are looping through log and each item is called log item
  - i is equal to the index of each logitem in log

  **pipes**

**Streams**

Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. The Angular HTTP client, HttpClient, is a built-in way to fetch data from external APIs and provide them to your app as a stream.
