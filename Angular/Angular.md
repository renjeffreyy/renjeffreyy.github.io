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
- **Encapsulation**: Normally Css is applied globaly with Angular, it is not because of view encapsulation. Instead of giving your html elements their classes and styles Angular gives it a unique property with all that info so your styles stay withon your component. To change this you would set this to none. Emulated is default.

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
  - We can bind properties to even our own components that we created.
    - define the property in our child to recieve them and in the parent component is where the data lives.
    - in order to allow the parent component to read the type of the child we import the `@imput decorator` from angular core and execute it next to the property `@Input() property_name`. this exposes our property to outside parent elements
    - If we want to change the name of the property we can pass the name that we want as an argument into the input decorator and change the name in the selector to match the name that you pass into the decorator. Original name will not work after passing the alias into Input decorator
- **event binding** (event)= 'expression'

  - we put the name of the event that we are going to listen for in the parenthesis and once that event occurs on the element it runs the defined function
  - passing \$event into theevent binding function gives us access to the event data emitted with the event
  - We can also bind to custom events

    - we create the events in the child component using `{EventEmitter}` from `@angular/core`. We input the Output decorator from angular core. This makes the event emitter available to the parent.
    - we create methods that will emit the event we created
    - in the selector of the element we event bind the name of the event and set it equal to a method in the parent component that does something with the event. you can have the method take data from the event and have it do sometihng with that event data. for example we take the event data and add it to a property in the parent component.
    - We can assign an alias to our event by passing in the name that we want as a string to the Output decorator
    - Example of binding to own events

```html
Events in the selector html. we click a button that will emit the events
<app-cockpit
  (serverCreated)="onServerAdded($event)"
  (blueprintCreated)="onBlueprintAdded($event)"
></app-cockpit>
```

import EventEmitter and output from angular core

create the event emitters

create a method that will emit the event

```typescript
import { Component, OnInit, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-cockpit',
  templateUrl: './cockpit.component.html',
  styleUrls: ['./cockpit.component.css'],
})
export class CockpitComponent implements OnInit {
  @Output() serverCreated = new EventEmitter<{
    serverName: string;
    serverContent: string;
  }>();
  @Output() blueprintCreated = new EventEmitter<{
    serverName: string;
    serverContent: string;
  }>();
  newServerName = '';
  newServerContent = '';
  constructor() {}

  ngOnInit(): void {}

  onAddServer() {
    this.serverCreated.emit({
      serverName: this.newServerName,
      serverContent: this.newServerContent,
    });
  }

  onAddBlueprint() {
    this.blueprintCreated.emit({
      serverName: this.newServerName,
      serverContent: this.newServerContent,
    });
  }
}
```

this is what the parent component should look like

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  serverElements = [
    { type: 'server', name: 'TestServer', content: 'just a test' },
  ];

  onServerAdded(serverData: { serverName: string; serverContent: string }) {
    this.serverElements.push({
      type: 'server',
      name: serverData.serverName,
      content: serverData.serverContent,
    });
  }

  onBlueprintAdded(serverData: { serverName: string; serverContent: string }) {
    this.serverElements.push({
      type: 'blueprint',
      name: serverData.serverName,
      content: serverData.serverContent,
    });
  }
}
```

- **two way data binding:** [(ngModel)]="data"

  - FormsModule is required for two way data binding
  - you need to make sure it is in the imports of the app module and that you import it from @angular/forms

### local references in templates

- we can place a local reference anywhere in our tempalte html file. We add local reference by adding a `#reference_name` to the html that we want to reference.
- this local reference allows us to reference that html anywhere in our tempalte code. Not in our typescript code.
- An example of how we can use this reference is by putting the reference on an input field and passing the value of that input field into one of our methods in the template by accessing the value property of the html element
- `console.log(name_of_reference)`

If you want to access tempalte and DOM Values you can use the @ViewChild

- we would give the template html a local reference.
- then we would import the `@viewChild` decorator
- we pass the local reference into the view child decorator as a string.
- `@ViewChild('Local_reference_name`) name of property in typescript: type_of_property;`
- from there we can reference the property in typescript. If we want to access the value this was we can use the nativeElement.value property to get the value of the Dom/tempalte element.
- `this.name_of_property.nativeElement.value`

### Projecting Content into components with ng-content directive

Just like how we put text in between html elements and have the inside value display we can put HTML/content in between selector tags and have that content be injected into our component template

1. put the html elements in between the opening and closing of the selector tags
2. inside of the template file of your component add the `<ng-content></ng-content>` directive where you want the content to be injected.

### Directives

Directives are instructions in the dom
we can add attribute like keybords into our html to manipulate the dom

**Structural Directives vs Attribute directives**

**Attribute:** sit in template elements just like attributes. Only affect the element they sit on.

**Structural Directives:** also sits in tempalte but changes the DOM. Affect a whole area of the DOM. We can not have more than 1 structural directive in an element

**built in directives**

- NGIF. performs conditional rendering. we add \*ngIf to the element we want to manipulate
  - `*` is required when directives change the structure of the DOM
  - for ngIF the element will not display if we pass in something false
  - to use the else feature we can add an else attrivute followed by the name of the replacing componenent. You will need to use an ng-tempalte with a marker with `#name_of_else`
- ngStyle
  - allows us to change the style of the element. we put ngStyle in Brackets to bind to the ngStyle property and set it equal to a value/function in javascript
  - allows us to dynamically update the styles
  - unlike strucural directives that add or remove elements, attribute directives only change the elements they were placed on.
  - example" `[ngStyle]="{attribute:condition}"`
    - condition can be ternery
- ngClass
  - allows us to dynamically add or remote css classes
  - only adds the class if a met condition is true
  - example: `[ngClass]="{class_name: condition}"`
- ngFor

  - structural directive so we need to include the star in the syntax
  - `*ngFor="let logItem of log; let i = index"`
  - we are looping through log and each item is called log item
  - i is equal to the index of each logitem in log

**How to make your own directive**

1. create a class that will hold your directive logic
2. import Directive and ElementRef, and others you may need from angular core
3. Use the @Directive decorator to give it directive behavior and pass in an object with properties of your directive
   1. main property you need is selector. this creates the selector for the directive. we can put the selector in square brackets to make it so all we have to do is add the property name to the element
4. inject ElementRef
5. implement onInit
6. set ngOnInit to the logic you want the directive to perform.
7. you need to add the directive to the appmodule.
   1. import the directive from its location and add the import name to the declarations array

you can use the cli to generate directives
`ng generate directive directive_name`

if you want to access the DOM the best way to do it is using renderer.

[Read more about Angular Renderer](https://angular.io/api/core/Renderer2)

### Component Life cycle

**types of lifecycle hooks**
Whenever angular creates a component for us it goes through life cycle hooks and gives us a chance to hook into these phases and execute some code.

- ngOnChanges: called at the start of the component life cycle and ran whenever properties with the @input decorator is changed
- ngOnInit: called once the component has been initialized. We may not be able to see it yet but it is when it is first initialized. the properties can be accessed. will run after constructor.
- ngDoCheck: called during every change detection run. will run on every check. angular does this in a very efficient way. This is mainly for if you want to run something on every change.
- ngAfterContentInit: called after content from ng-content has been projected into view
- ngAfterContentChecked: called everytime the project content has been checked
- ngAfterViewInit: runs when our view has been rendered
- ngAfterViewChecked: called everytime the view and child views has been checked
- ngOnDestroy: called once the component is about to be destroyed

Constructor and nginit run on each new instance of the class

`ngOnInit(){}`
**pipes**

**Streams**

Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. The Angular HTTP client, HttpClient, is a built-in way to fetch data from external APIs and provide them to your app as a stream.
