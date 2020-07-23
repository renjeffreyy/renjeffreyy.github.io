# SCSS or SASS

**CSS on steroids**

if you are using vs code a lot of people recomend that we add the scss compliter extension. this is becaus ebrowsers can not read scss. they can only read regular css

What can we do in SASS

- we can create variables
  - we use the $ to create a variable. put the $ in front of your variable name
  - ex: `$primaryButtonColor :red;`
  - this works like any other variable in javascript/programming language
- maps
- nesting
  - instead of creating new blocks for css elements within other css elements we can next them into the parent

example:

```scss
header {
  background: red;
  button {
    background: blue;
  }
}
```

to add hover, before, after, etc we add the & symbol before the keyword within the element we want to style

example:

```scss
button {
  background: red;
  &::after {
    content: 'hello';
  }
}
```

- mixins
  - similiar to functions in a programming language we can put several styles into a mixin and use them like puzzle pieces and put those styles where we need them. this helps us not repeat code.
    example of mixin:

```scss
@mixin flexCenter {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

then in the element we are styling we call `@inclide flexCenter();`
if we want to use the mixin but change something we can define a variable within the parenthesis of the mixin and use it within the mixin

example

```scss
@mixin flexCenter($direction) {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: $direction;
}

@include flexCenter(center);
```

- extensions
  - we can have elements inherit the styles of another by using extensions
  - `.contact{ @extends header;}` and if we want to change the styles of the extensions we can just write them following the extensions
- operations
  - we can do operations in scss + - / \*
- imports
  - we can import our our scss from different files. this can help us organize our code

**Extensions**

If we have styles that we want to transfer to other elements we can extend them using `%` to start of the style. for example `%message-shared` to define the shared styles and inside of the elements that we want to put those styles into we can use `@extend %message-shared` inside the curly brackets of scss and also add out own styles

**Example of extension**

```scss
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
}

.message {
  @extend %message-shared;
}
```
