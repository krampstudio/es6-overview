# Notes

## Resources

 - [features](https://github.com/lukehoban/es6features)
 - [Scope](http://www.2ality.com/2015/02/es6-scoping.html)
 - [Classes](http://www.2ality.com/2015/02/es6-classes-final.html)
 - [Pattern and linting](https://medium.com/javascript-scene/how-to-use-es6-for-isomorphic-javascript-apps-2a9c3abe5ea2)
 - [compat table](http://kangax.github.io/compat-table/es6/)

## Plan

 1. Past, Present, Future
    1. ES History
    2. ES6 Standard
    3. ES2015
    4. Runtimes, compilers
 2. Overview
 3. Implementation
    1. Babel
    2. Browserify
 4. Patterns
 5. Pro and con

## Features Overview

### Sugar

- enhanced object literals
- destructuring
- template strings

### Object Literrals

```javascript
var tatoo = {
    size : function size(){
        return 'small';
    },
    ink(){
        return 'red';
    }
};

tatoo.ink() === 'red';
```

```javascript
var color = 'red';

var tatoo = {
    size : 'small',
    color
};

tatoo.color === 'red';
```

```javascript
var color = 'Red';
var size  = 'small';
var tatoo = {
    ['has' + color + 'Ink'] : true,
    ['is' + small.toUpperCase()](){
        return true;
    }
};

tatoo.hasRedInk === true;

tatoo.isSMALL() === true;
```


### Functions and scopes

- default + rest + spread
- let + const
- arrows
- proxies

### Async

- promises
- generators

### Collections

- map + set + weakmap + weakset
- iterators + for..of

### Class

- classes
- subclassable built-ins

### Types and core API

- symbols
- math + number + string + array + object APIs
- binary and octal literals
- unicode

### System

- modules
- module loaders
- reflect api
- tail calls
