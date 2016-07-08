# <img src="https://pbs.twimg.com/profile_images/590941374100430848/WlWr2NYD.png" width="50px">  Indiewalls Styleguide <img src="https://pbs.twimg.com/profile_images/590941374100430848/WlWr2NYD.png" width="50px"> 

## Table of contents 
  - [Javascript](#javascript)
    - [ES2015](#es2015)
      - [Arrow Functions](#arrow-functions)
      - [Object Shorthand](#object-shorthand)
      - [Template Strings](#template-strings)
      - [Destructuring](#destructuring)
      - [Const](#const)
      - [Towards the Future](#towards-the-future)
  - [CSS SCSS] (#css-scss)
  - [React] (#react)

## Javascript

### ES2015

We should move towards adopting the newest syntax whenever possible.
  
Not for the sake of keeping up with the "latest and greatest" but because
ES2015 has tools that help write clean code and provide solutions for many problems 
that have existed in the language.
  
These are features that we should be using in our codebase today
  
### Arrow-Functions
  
Not only are arrow functions easier to read but they provide functional benefits as well.

Be aware of these though as they could produce a different result than you intended.

#### How you write one:

```javascript
//this
() => {}
//is the same as this
function() {}
```
Although the difference isn't much, it really helps when you're looking at a more 
complex example.

```javascript
//Map function using regular function:
someArray.map(function(el) {
  return el + 2;
});
//With arrow:
someArray.map(el => el +2);
```

As you can see the first two things arrow functions do for us is:
  
#### Implied return:

When an arrow function is **one** line it automatically returns the function body.

```javascript
var same = x => x;
same(2); //returns 2

//In es5:
var same = function(x) {
  return x
}
```

#### Remove Parens:

If you only have **one** argument you do not need parens.

```javascript
var validFunction = x => x; 👍🏼
var jankFunction = x, y, z => x; 👎🏽
```

#### Lexical This:
The main benefit to arrow functions are their _this_ scope.

Unlike normal functions, the _this_ context is scoped to the surrounding code.
I like to think of it as the "parent context".
> why is this helpful?

When working with a lot of objects (ex. react components) the _this_ context sometimes gets lost inside of methods.
This means instead of using:
```javascript
// Instead of this 👎🏽
var component = {
  x: 2,
  addX: function(array) {
    return array.map(function(el) {
      return el + this.x;
    }.bind(this));
  }
}; 
// We can do this 👍🏼
var component = {
  x: 2,
  addX: function(array) { 
    return array.map(el => el + this.x);
  }
};

// However, you must be aware of "this" when using arrow functions 
// to avoid things like this: (no pun intended)😁

var component = {
  x: 2,
  addX: array => { 👈🏽
    return array.map(el => el + this.x);
                                👆// 'this' returns undefined in this context
                                //becuase we are using an arrow function one level above as well
                                //this means that the "this" context gets lost 😱
  }
};
```
> That stinks. But using object shorthand we can still make our objects nice and concise!

```javascript
var component = {
  x: 2,
  addX(array) { 👍🏼
    return array.map(el => el + this.x);
  }
};
```

*There are more fine grain differences that you probably won't encounter but you can read more
[here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).*

#### Our In House Style <img src="https://pbs.twimg.com/profile_images/590941374100430848/WlWr2NYD.png" width="30px"> 

```javascript
// If there is only one argument, no parens
x => x; 👍
x => {
  return x + 2; 
}; 👍🏼

// If there is multiple arguments, you **must** use parens.
(x,y,z) => x; 👍

// If the arrow function is an argument of another function, 
// and is not the only argument, please use parens. 
// Even if the arrow function only has one argument.
Obj.someFunction(y => y + z); 👍
Obj.someFunction(x, y => y + z); 👎🏽
Obj.someFunction(x, (y) => y + z); 👍
```
> Why?

It's confusing to read, as the argument to the arrow function looks like an argument for the invoked function.
```javascript
Obj.someFunction(x, y => y + z);
                    👆🏽//can't tell if argument for invoked function or callback function....
```

### Object Shorthand

#### Coming Soon

### Template Strings

#### How:

Instead of using regular qutoes, use back ticks.

To interpolate a variable, surround the variable name with: 

> ${varNameHere}

Template strings provide two big conveniences:

#### Interpolating variables in strings
```javascript
var name = 'Nathan';
var greeting = `Hello my name is ${name}!` 👍🏼
// greeting returns "Hello my name is Nathan!"

// No more of this non-sense 👎🏽
var name = 'Evan';
var favoriteDrink = 'coffee';
var greeting = 'Hello my name is ' + name + ' and my favorite drink is ' + favoriteDrink + '!'; 😱
// How bout this instead? 
var greeting = `Hello my name is ${name} and my favorite drink is ${favoriteDrink}!`; 👍🏼
```

#### Multiline strings
```javascript 
// We can now write on multiple lines like a normal human being. 👱🏽
var someHtml = `
  <div>
    <span>
      <h1>Hello ${name}!</h1>
    </span>
  </div>
`;

// Let's look at the old way...

var someHtml = "<div>" + "\n" +
  "<span>" + "\n" +
      "<h1>Hello " + name + "!</h1>" + "\n" +
    "</span>" + "\n" +
  "</div>";
// wat? 👽 
```

> Why?

You can see from the comparison how error prone concating with '+' is. 

Also template strings are much more readable, especially when interpolating multiple values on multiple lines.

#### Our In House Style <img src="https://pbs.twimg.com/profile_images/590941374100430848/WlWr2NYD.png" width="30px"> 

Always use template strings if your string involves multiple lines or variable interpolation.

**Even if it involves only _one_ variable.**

If it is just a regular string (single line, no variables) then just use regular quotes.

### Destructuring

#### Coming Soon

### Const)

#### Coming Soon

### Towards the Future

#### Coming Soon

## CSS-SCSS

#### Coming Soon

## React

#### Coming Soon


