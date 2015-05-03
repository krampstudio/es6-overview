# Notes

## Resources

 - [features](https://github.com/lukehoban/es6features)
 - [Scope](http://www.2ality.com/2015/02/es6-scoping.html)
 - [Classes](http://www.2ality.com/2015/02/es6-classes-final.html)
 - [Pattern and linting](https://medium.com/javascript-scene/how-to-use-es6-for-isomorphic-javascript-apps-2a9c3abe5ea2)
 - [compat table](http://kangax.github.io/compat-table/es6/)
 - [iterators](https://hacks.mozilla.org/2015/04/es6-in-depth-iterators-and-the-for-of-loop/)
 - [generator async](http://davidwalsh.name/async-generators)
 - [Terms](http://www.2ality.com/2011/06/ecmascript.html)

## Plan

 1. Past, Present, Future
    1. ES History
    2. ES6 Standard
    3. ES2015
 2. Overview
 3. Implementation
    1. Runtimes, compilers
    2. Babel
    3. Browserify
 4. Patterns
 5. Pro and con

## Past, Present and Future

### What's what

- ECMAScript : "Java" is a trademark of Sun so "JavaScript" is also (why microsoft named it JScript, etc.). The name of the language and the standard. Hosted by ECMA international
- ECMA-262 : the standard
- ES 5 : 5th edition of ECMA-262
- TC39 : The Technical Committee that maintain the standard

###  How all began

 - 1995 : Eich developped Mocha/LiveScript
 - 1996 : Netscape (with Sun) include JavaScript in the browser (in order to complete Java) 
 - 1996 : Netscape submit JavaScript to ECMA for standardization
 - 1997 : ECMA-262 1st Edition
 - 1998 : ECMA-262 2nd Edition
 - 1999 : **ECMA-262 3rd Edition **  This is the version we all know. 

### The dark years

 - 1999 - 2008 : JavaScript is a toy. T39 start an amibitius new version : static typing, classes, generators, annotations, generics, etc. But they even never been agreed what features to include. 
 

### The resurection
 
 - ~2005 web2.0 is rising  
 - 2008 : v8
 -  2008 : TC39 finally abandonned ES4. Agreement on starting 2 projects :   ES5 as a lighter version and Harmony for the future of the language. 
 - 2009 : ECMAScript 5th Edition
 - 2009 : 1st version of node.js
 - 2011 : ECMAScript 5.1th Edition (The current implementation)

### And now 

 - ES6 is feature complete
 - planned for end of May 2015
 - Some Harmony features have been moved to ES7 
 - Now called ES 2015 (really?)



## Features Overview

### Backward compatible

 ALL ES5 features :

 - strict mode (change langage semantic but enable backward compat)
 - API Enhancement : 
 -- `Object.create`, `Object.keys`,  `Object.defineProperty`, etc.
 -- `Array.indexOf`, `Array.forEach`, `Array.map`, `Array.reduce`, `Array.filter`, `Array.some`, etc.
 -- `Date.now`, `Date.toISOString`
 -- `Function.bind`
 -- `String.trim`
 -- `JSON`
 - Getter/Setter 
 - Property access on string and on object using reserved keyword
 
[Features and compat table](http://kangax.github.io/compat-table/es5/)

### Sugar

- enhanced object literals
- destructuring
- template strings

### Object Literrals

#### Methods

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

#### Properties

```javascript
var color = 'red';

var tatoo = {
    size : 'small',
    color
};

tatoo.color === 'red';```

#### expressions for property name

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

### Destructuring

#### Destructuring Array

```javascript
var tattoo = ['small', 'red', '$80'];
var [size, color, price] = tattoo;

size === 'small';
color === 'red';
price === '$80';
```

#### Destructuring Objects

```javascript
var tattoo = {
    s : 'small',
    c :'red',
    p : '$80'
};

var { s : sizer, c : color, p : price };

size === 'small';
color === 'red';
price === '$80';
```

#### Soft failing

```javascript
var [size] = [];

size === undefined;
```

### Template Strings

#### Substitution

```javascript
var tattoo = 'pin-up';
var desc   = `My mother has a ${tatoo} tattooed on her arm`;
```

#### Multiline

```javascript
var tattoo = 'pin-up';
var desc   = `<div>
    <span>My mother has a <strong>${tatoo}</strong> tattooed on her arm</span>
</div>`;
```

#### Expressions

```javascript
var tattoos = ['pin-up', 'anchor', 'dragon'];
var desc   = `My mother has a ${tatoos.length} tattoos`;
```

#### Tagged templates

```javascript
function tattoo(tpl, ...values){
  return tpl.reduce(function(acc, chunk, index){
    return acc + chunk + (values[index] || '');
  }, '');
}

var size = 'SMALL';
var motif = 'flower';
var color = 'red';

var res = tattoo`A ${size.toLowerCase()}, ${color} ${motif} tattoo`;
res === "A small, red flower tattoo";
```

### Functions and scopes

- function parameters
- variable declaration
- arrows
- proxies

###  function parameters

#### Default value

```javascript
function countTattoo(tattoos = [] ) {
	return tattoos.length;
}

countTattoo(['arms', 'neck']) === 2;
countTattoo() === 0;
```

#### Rest parameter

```javascript
function countTattoo(...tattoos) {
	return tattoos.length;
}

countTattoo('arms', 'neck') === 2;
countTattoo() === 0;
```

#### Spread

```javascript
function drawTattoo(size, color, location){
	return 'Drawing a ' + size + ', ' + color + ' tattoo on the ' + location;
}

var tattoos = ['small', 'green', 'back'];
drawTattoo(...tattoos) === 'Drawing a small, green tattoo on the back';
```

### variable declaration

#### let

```javascript
if (true){
	let size = 'small';
	size === 'small';
}
typeof size === 'undefined';
```

#### const

```javascript
if (true){
	const size = 'small';
	size === 'small';

	//size = ''; throws a SyntaxError 
}
typeof size === 'undefined';
```

#### Arrow functions

#### => expression as body

```javascript
var tattoos =  ['pin-up', 'anchor', 'dragon'].map( t => t[0].toUpperCase() + t.substring(1).toLowerCase());
```

#### => block as body

```javascript
var tattoos =  ['pin-up', 'anchor', 'dragon'].map( t => {
	return t[0].toUpperCase() + t.substring(1).toLowerCase()
});
```

#### => scope

```javascript
var tattoo = {
	color  : 'blue',
	draw  : function (locations){
		var result = [];
		locations.forEach( (l, i) => {
			result[i] = 'Drawing a ' + this.color + ' tattoo on the ' + l;
		});
		return result;
	}
};

var drawing = tattoo.draw(['arm', 'leg']);
drawing[0] === 'Drawing a blue tattoo on the arm';
drawing[1] === 'Drawing a blue tattoo on the leg';
```

#### Proxies

**!!! todo !!!**

```javascript
var handler = {
	get : function(target, property){
		//trap
		return target[property];
	},
	set : function(target, property, value){
		target[property] = value;
	}
};
var target  = {};
var p = new Proxy(target, handler);
p.foo = 'bar';
p.foo;
```
**!!! todo !!!**

### Async

- promises
- generators

#### Promises

#### Generators

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

## Implementation

## New Patterns

 - spread instead of [].slice
 - default parameter (see isomorphic es6)
 - for [k,v] of Map
 - for k of Object.keys(array)
 - arrow fn in forEach, map/reduce
 - generators ???
 - spread to replace arguments (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)  
