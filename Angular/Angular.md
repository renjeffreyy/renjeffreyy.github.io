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

## In-app navigation

**pipes**

**Streams**

Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. The Angular HTTP client, HttpClient, is a built-in way to fetch data from external APIs and provide them to your app as a stream.
