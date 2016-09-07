# This document is living
If you'd like to make a change to it, then propose it to the group and lets make the change

# JavaScript Reference
- [The fundementals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators)
- [JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [Memory managment / Garbage collector](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)

Read and memorize this.
# JavaScript Style Rules
Familiarize yourself with the [Google JavaScript style rules](https://google.github.io/styleguide/javascriptguide.xml#JavaScript_Style_Rules). Once you get it, use the following style rules at Augur:
## spacing
  - Always use 4 indent spacing
  - Use tabs, not spaces
  - Always use a space (nbsp) between characters to make code easily digestable at a glance, for example:
```javascript
let x = 'variable';
  ```
## declaration
### values
```javascript
// always end declarations in semi-colons => ;
// always 'use strict' on top of scripts, it improves performance
'use strict';
let a = 1; // always use let when working with variables. let is bracket scoped
const SOME_CONST = true; // use const when declaring and reusing a value. const is bracket scoped
var c = 'string'; // use var when you cannot use let or const
```
### functions
```javascript
function name( arg1 = 'default arg value', arg2 = {}, arg3 = false, ...restOfTheArgs ) {
    return [ arg1, arg2, arg3, restOfTheArgs ];
}
name( undefined, undefined, null, 1, 2, 3, 4, 5, 'abc' );
```
### arrow functions
```javascript
function tellMeTheDifference( someArg ) {
    this.property = 'correct context';
    
    let arrowFunc = ()=> {
        console.log({ 
            details: 'by default, arrow functions inherit context', 
            argumentVector: arguments, 
            context: this 
        });
    };
    let normalFunc = function() {
        console.log({ 
            details: 'by default, normal functions do not inherit context', 
            argumentVector: arguments, 
            context: this
        });
    }
    
    normalFunc();
    arrowFunc();
}
new tellMeTheDifference( 'this is an argument value' );
```
### arrow expressions
```javascript
const sum = ( a, b )=> a + b;
console.log( sum( 1 + 9 ) ); // returns 10
```
### arrow vs function usage
Always use function. Only use arrow functions if you intend to make the function inherit context.
## boolean
  - Always use ===
  - never use ==

## if statements
```javascript
let a = false;
let b = 0;
let c = [];
let d = {
        key: 'value'
    };
let e;
    
if ( a === true ) {
    console.log( true );
} else if ( b === 1 ) {
    console.log( 'also', true );
} else if ( e !== undefined || d.constructor === Object && d.key === undefined  ) {
    // do something
} else if ( c.constructor === Array ) {
    console.log( d );
} else {
    console.log('this never gets called');
}
```
## loops
### Array
#### when iteration order matters
```javascript
/*
    the for loop is fast and easy to read.
    use it when ordered iteration matters.
*/
let array = [ 1, 2, 3 ];

for ( let i = 0, j = array.length; i < j; i++ ) {
    // do something with array[i]
}
```
#### when iteration order does not matter
```javascript
/*
    This is the fastest loop in JavaScript, b/c it requires 
    the least amount of computation to continue iterating. 
    Use always. When not possible to use, then use the for loop.
*/
let array = [ 1, 2, 3 ];
let i = array.length;

while ( i-- !== 0 ) {
    //do something with array[i]
}
```
#### Objects
```javascript
let obj = {
        a: 1, 
        b: 2, 
        c: 3
    };

for ( let property in obj ) {
    //do something with obj[ property ];
}
```
#### Sets
```javascript
let set = new Set([ 1, 2, 3 ]);
/*
    Get each element in the set
*/
for ( let element of set ) {
    //do something with each element;
}
```
#### Maps
```javascript
let map = new Map([ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ]);
/*
    Get each element in the set
*/
for ( let [ key, value ] of map ) {
    //do something with each key, value
}
```
# JavaScript Best Practice
Best practice for optimal performance.

## Pointers vs new values
Always answer the question:
> Am I creating new object at run-time? Or am I creating a pointer that's getting re-used?

##### Be careful! Don't use a pointer when you actually mean to assign a clone of the value!
This causes weird bugs if you screw it up.

## Cloning
### Object
```let clone = Object.assign( {}, obj );```
### Array
```let clone = array.slice();```
### Primitives
```javascript
let primitive = 1;
let clone = primitive;
primitive = 0;
console.log( clone === 1, primitive === 0 ); // returns true, true
```
## Casting
### String to Number
```javascript
let string = '1'; // string.constructor is String
let number = +string; // number.constructor is Number
let oops = +'this is not a number!'; // oops now equals NaN, since this was a bad cast
```
### Number to String
Use Int + '' 
```javascript
let number = 1; // number.constructor is Number
let string = number + ''; // string.constructor is String
```

## JSON
### Stringify
Remember, JSON.stringify randomly creates a string from an object. Do not expect the same string to be created through the serialization process. You'll need a plugin for that, such as json-stable-stringify on npm.
