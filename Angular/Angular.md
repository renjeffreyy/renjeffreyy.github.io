# Angular

Table of Contents

- [Getting Started](##Getting-Started)
- [How an angular app gets loaded and started](##How-an-angular-app-gets-loaded-and-started)
- [Components](##Components)

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
- **Provider**: tells angular how to create services. **note**: i dont know if it is limited to services. further research needed

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

- ngSwitch
  - similair to switch n avascript. used when you have a lot of conditions and cases
  - `[ngSwitch]="value_in_ts_to_observe"` put this in the containing element like a div
  - in the child elements add *ngSwitchCase directive `*ngSwitchCase="value"`
  - add a default case to the end of the switch `*ngSwitchDefault`

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

### Services and Dependency Injection

**Services**
Centralized containers to put similiar business logic and data. These allow other components that may need the same data or functions to have access to them through services instead of having to pass them down to parents/child

- allows you to communicate between components
- a service does not need a decorator. it is just a normal typescript class
- We need to inject the service using the constuctor of the component we want to use the service in.
- we import the service into the file and then in the constructor of the component we inject the service
  - example: `constructor(private alias_of_service_in_component: Service_Name){}`
  - we are prividing the type of the service that we want. the type is what follows the colon.
  - we need to tell Angular how to provide the service. We do that by passing the Service into the providers array that we put into the @component decorator
- we can then utilize all the properties of the service by using the this keyword followed by the alias that we gave ourservice.
- putting the service int he provider creates new instances of the service. Instances of services Propogate down to the children but defining new instances within child components overiedes the instance in the parent component. So to use the same instance we need to only put the service in the provider of the top most level of our component that needs the service.
- Highest level of service instance is at the appModule in the providers array.By putting the service in the app module we ensue that all of our components get the sane instance of the service unless we overide it.

**Injecting a service into a service.**

We can inject a service into aservice but in order to do so we need to use the @injectible decorator from angular core. Thi decorator provides Angular with the metadata that would normally come from an angular component.

- example `this.service_alias.method_in_service()`

In order to create a data service it is the same as making a normal service except whehn you inject everything into the component , define a property for your data and assign type then you want to implement ngOnInit and set the data to initalize when the component initializes.

### Routing

Routing Module constrols what content are displayed to the user when a specific route is entered into theURL

- In the app module or in a seperate app.routing module Crete a constant variable containing your routes. `const routes: Routes = []`
  - the variable is type routes that is imported from `@angular/routes`
  - We also import Router Module from `@angular/routes`.
- The route array takes in objects that contain information about your route
- object has to follow a specific strucutre for it to work
  - path:
    - always needs a path. This is the part of the url that gets entdered after your domain
    - Should be a string
    - Do not add the slash in the beginning
  - component
    - informs angular that after a path is entered, show the specified component
- You should set an empty path to render home component
- Add Router Module or module containing yor routes info to imports into appModule.ts
- use forRoot method of RouterModule and pass in your route variable containing all your array of routes `RouterModule.forRoot(routes)`
- Browser Outlet has it's own directive that marks where you want to display your pages on your route `<router-outlet></router-outlet>`

example

```typescript
import { Routes } from '@angular/router';
const routes: Route = [
  { path: 'name_of_path', component: 'name_of_component' },
];
```

**Changing the url and displaying content on router outlet**

If you use a normal anchor tag to cchange the URL your page will refresh every time. This makes it so you lose all state and data on refresh. So it is best to use routerLink directive to change routes and display content
routerLink is a directive that allows us to change the route and thus change the content that is displayed in the router outlet.

- to give your active routes style angular provides a routerLinkActive directive that adds a class to your element if the url for that router link is active.
  - the way router link active works is that it will give the class as long as any of the routes are within the main url. What this means is that the default home url with slash will always be active. To change that we can add `[routerLinkActiveOptions]="{exact: true}"` to make it so the active class only gets applied to exact matches.

naviating routes

- adding a slash (`routerLink='/route'`) in front of your route will change the url to add your route to the root url. example rootUrl.com/route.
- If you add a route name without a slash in the beggining it will try to add the route to the current page. so if you use `routerLink='route'` and you are currently on rootUrl.com/route. The new route will be rootUrl.com/route/route
- we can use dot notation to navigate the routes like we do with directories `routerLink="../../route"`. This takes a look at the current route and sets it accoding to the dot notation. In the example it will go back 2 slashess and look for your route path.
- We can programmically navigate to routes by creating a method that navigates to the desired route. We do this by importing Router from angular code, injecting router dependency, and using `this.router.navigate(['/route'])`. this will not refresh the page. it will behave just like router link
- we can add data to routes dynamically by starting the portion we want to add with a colon. `routerLink='/route/:dynamic_variable'`
  - be careful this will make it so that basically anything can take the place of the dynamic variable and the component will load.

**Child Routes **

- You can add child paths to routes with the same base. just pass children into the pbject as an array with all the child routes inside the array

example:

```typescript
const routes: Routes = [
  {
    path: 'first-component',
    component: FirstComponent, // this is the component with the <router-outlet> in the template
    children: [
      {
        path: 'child-a', // child route path
        component: ChildAComponent, // child route component that the router renders
      },
      {
        path: 'child-b',
        component: ChildBComponent, // another child route component that the router renders
      },
    ],
  },
];
```

- you can add aother router outlet selector inside the component with the child routes and children will be injected to the router outlet selector

Handling Undeefined routes

- One way to handle undefined route is to define a redirect path that takes in all unfamiliar paths and redirects them to a specific page.
- To do this we set path equal to `**` and add redirectTo: to the object
- we can also create a page not found component. whatever the wild car path is be sure to add it to the end so angular can go through all your previous routes first. Routes get parsed from top to bottom
  example

```typescript
const routes: Routes = [
  { path: 'first-component', component: FirstComponent },
  { path: 'second-component', component: SecondComponent },
  { path: '', redirectTo: '/first-component', pathMatch: 'full' }, // redirect to `first-component`
  { path: '**', component: PageNotFoundComponent }, // Wildcard route for a 404 page
];
```

For more complex applications we can outsource the routing of our application to its own app routing file.

Your app routing file will look like this

```typescript
//be sure to import these. import the component
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';

//these are the routes in your app
const routes: Routes = [{ path: 'heroes', component: HeroesComponent }];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

Be sure to import your app routiring module to your app module file. add it to the imports array.

### Route guards

One way to protect against unauthorized access to routes is by using an authguard service. This code runs when users are trying to access the protexted route.

- to run the check when a user tries to access a route we add the canActivate property to the routes object and set it equal to the guard that we have created.
- [Here is an article to help with auth guards in angular](https://medium.com/@ryanchenkie_40935/angular-authentication-using-route-guards-bf7a4ca13ae3)
-

**pipes**

**Streams**

Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. The Angular HTTP client, HttpClient, is a built-in way to fetch data from external APIs and provide them to your app as a stream.
