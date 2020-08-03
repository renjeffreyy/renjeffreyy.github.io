# Typescript

Typescript is a super set of javascript. TLDR it is javascript with a bunch of healthful features for the developer. it compiles down to javascript.

## Assigning types to a variable

Assigning variables in typescript is the same as assigning them in javascript except we can define the type of the variable.

example

```typescript
let myString: string;
```

with this you create an instance of the variable but when you assign it a value the value must be type string. if not you are going to get an error in your editor

if we do not define the type typescript can infer the type of the variable if you assign it a value upon defining it

example

```typescript
let myString = 'myString';
```

in this example type script will infer that the type of the variable mystring is of type string. If you later try to reassign the variable to a non string value, typescript will throw an error.

if we just define the variable like below. Typescript will just assign the type any to the variable.

```typescript
let mystring;
```

Type any is not best practice, it is good to define the type of your variables, classes, etc because it will help catch errors and help you write better code.

## Classes in Typescript

classes in typescript compiles to old javscript which is useable by even older browsers.

private classes are only accessible from inside the class. They are not available outside the class.

We can add static keyword in front of class properties to make them accessible by default without defininf them.
