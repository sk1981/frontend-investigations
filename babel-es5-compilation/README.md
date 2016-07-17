##Introduction
The way Babel JS compilation works is by adding polyfills for some the features (like Map, Set) or convert it to to ES5 during build time. 
Here I am trying to to see how some of the static compilation features work. 

## Let

'let' allows block scope usage, the way babel works is by creating a a differently named variable if the variable is used again.

The below code declares a number 's', which is aleady re-declared with for blocks 
```javascript
let a = 4;
let s = 0;
let c = ''
if(a > 4) {
  let s = 6;
  c = 'a';
}

if(a <= 4) {
  let s = 4;
  c = 'b';
}
```
Which is converted to:-
```javascript
var a = 4;
var s = 0;
var c = '';
if (a > 4) {
  var _s = 6;
  c = 'a';
}

if (a <= 4) {
  var _s2 = 4;
  c = 'b';
}
```
So, babel, just creates a new variable (_s, _s2) if it's declared again.

Babel is smart enough to avoid conflicts with your existing code.
```javascript
let a = 4;
let _a = 6;
if(a > 4) {
  let a = 5;
}
```
Get converted to:
```javascript
var a = 4;
var _a = 6;
if (a > 4) {
  var _a2 = 5;
}
```
And, it does not creates a new variable if the variable is redeclared inside a function.
```javascript
let a = 4;
function test() {
  let a = 5;
}
```
Gets converted to
```javascript
var a = 4;
function test() {
  var a = 5;
}
```
