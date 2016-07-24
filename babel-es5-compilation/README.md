##Introduction
The way Babel JS compilation works is by adding polyfills for some the features (like Map, Set) or convert it to to ES5 during build time. 
Here I am trying to to see how some of the static compilation features work. 
Babel version is 6.9.1, and the approach my change in future babel versions.

# Table of Contents  
[Let](#let)  
[Const](#const)  
[Rest Parameters](#rest-parameters)  
[Spread operator](#spread-operator)  
[Default Parameters](#default-parameters)  
[Object Literal Enhancements](#object-literal-enhancements)  
[Template Literals](#template-literals)    
[Destructuring](#destructuring)

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

##Const
**const** works the same way as that is by creating a new variable where required.

```javascript
const a = 4;
if(a === 3) {
  const a = 5;
}
```
Gets converted to
```javascript
var a = 4;
if (a === 3) {
  var _a = 5;
}
```
One additional check is does is that it throws an error during build time if the variable is reassigned a new value.
```javascript
const a = 4;
a =5;
```
This throws error ***"a" is read-only***. This way babel ensures that your constant variables are not reassigned by mistake.
Note that this check happens during build time only.

## Rest parameters
The rest operator (...) can be used in front of the last formal parameter and ensures that it will receive all remaining actual parameters in an Array.

If only we are using specfic items from the ***rest array***, babel will just use the arguments object
```javascript
function test(main, sub, ...others) {
  console.log(others[2] + others[0])
}
```
Gets transformed to
```javascript
function test(main, sub) {
  console.log((arguments.length <= 4 ? undefined : arguments[4]) + (arguments.length <= 2 ? undefined : arguments[2]));
}
```
Here babel just checks if parameter being passed is valid or not and returning undefined otherwise.

If we are using the whole array babel will create a new array object.
```javascript
function test(main, sub, ...others) {
  console.log(others)
}
```
Gets transformed to
```javascript
function test(main, sub) {
  for (var _len = arguments.length, others = Array(_len > 2 ? _len - 2 : 0), _key = 2; _key < _len; _key++) {
    others[_key - 2] = arguments[_key];
  }

  console.log(others);
}
```
What's happening above is that babel is looping over the arguments object starting from 2 parameter, create a array object of the required length and then assiging the values from arguments object to the ***others*** array.

###Spread operator
The spread operator turns the elements of an array into the arguments of a function call or into elements of another array.
It can be used wherever we want to convert array of parameters into individual parameters, like adding elements to an array fro manother array.
```javascript
var params = [ 5, 6, 7 ]
var newArr = [ 1, 2, ...params, 8, 9 ] // [ 1, 2, 5, 6,7, 8, 9 ]
```
This gets converted to
```javascript
var params = [ "hello", true, 7 ]
var newArr = [1, 2].concat(params, [5, 6]); // [ 1, 2, "hello", true, 7, 5, 6 ]
```
Pretty straightfoward - it just uses concat to add elements to the array.

Spread can also be used where we have an array, using which we want to call functions or constructor accepting individual parameters.
```javascript
Math.max(...[-1, 5, 11, 3])
new Date(...[1912, 11, 24]) 
```
Gets converted to
```javascript
Math.max.apply(Math, [-1, 5, 11, 3]);
new (Function.prototype.bind.apply(Date, [null].concat([1912, 11, 24])))();
```
The ES5 version just uses ***apply*** along with the array to make the call.

Also, it can be used to convert any arraylike object to array
```javascript
function test() {
  const allArgs = [...arguments]
}
```
gets converted to
```javascript
function test() {
  var allArgs = [].concat(Array.prototype.slice.call(arguments));
}
```
Pretty similiar to what we used to do in ES5 manually.

##Default Parameters
Default parameters in ES6 are implemented in a straighfoward manner, the variables are extracted from function arguments and assigned default if they are undefined.
```javascript
function append(value = -1, array = []) {
  console.log(value, array)
}
```
Gets converted to:
```javascript
function append() {
  var value = arguments.length <= 0 || arguments[0] === undefined ? -1 : arguments[0];
  var array = arguments.length <= 1 || arguments[1] === undefined ? [] : arguments[1];
  console.log(value, array);
}
```

##Object literal enhancements

#### Method definition shorthand
The short method defintions simply converts to the longer format.
```javascript
var data = {
  do() {
    return "do"
  },
   done: function() {
    return "done"
  }
}
```
Gets converted to
```javascript
var data = {
  do: function _do() {
    return "do";
  },

  done: function done() {
    return "done";
  }
};
```
Main thing to note is that babel adds names to the function expression - ***_do*** and ***done*** in the above example.

#### Shorthand notation
ES6 allows us to use shorthand notations in object literals instead of repeating something like ***var1: var1*** everywhere.
```javascript
var myField = "test";
var a = {
  some: "some",
  myField,
  last: "last"
}
```
Gets converted to
```javascript
var myField = "test";
var a = {
  some: "some",
  myField: myField,
  last: "last"
};
```

####Computated Keys
ES6 enables us to use variables as object keys in object literal format. Earlier, we had to manually assign the properties on the object instance.
```javascript
var data = {
  field: "hello",
  [variableFile]: "Some Value",
  lastfield: "bye"
}
```
Gets converted to:
```javascript
var _data;
var data = (_data = {
  field: "hello"
}, _data[variableFile] = "Some Value", _data.lastfield = "bye", _data);
```
Note that we are creating a new field to initialize ***_data*** to attach the key and then using the [comma operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Comma_Operator) to assing ***_data*** to ***data***.
Also, even though the ***lastfield*** property hash static key, we are still assiging it dynamically to preserve the order in the keys are present in the object literal.

## Template literals

#### String literals
String Tempaltes literals enhances the create of string objects by enabling us to use variables or create multiple line strings.

```javascript
var url = "test.com"
var title ="Test";
var fullLink = `<a href="${"http://" + url}">${title}</a>`
```
Gets converted to
```javascript
var url = "test.com";
var title = "Test";
var fullLink = "<a href=\"" + ("http://" + url) + "\">" + title + "</a>";
```
This is pretty much what we would do, template literals just save us the hassle of concatenating and escaping.

Simililarly for multiline strings:-
```javascript
var longString = `
  Address line 1,
  Address line 2,
  City,
  Country
`;
```
Gets converted to
```javascript
var longString = "\n  Address line 1,\n  Address line 2,\n  City,\n  Country\n";
```
Note that all extra spaces and new lines are present in the converted string, enabling us to write multline strings in a more readable manner. 

#### Tagged templates
With tagged templates were are able to modify the output of template literals using a function applied to the template as a tag.

```javascript
var a = 5;
var b = 10;
tag`Hi   \n.Hello ${ a + b } world ${ a * b }`;
```
Gets converted to
```javascript
var _templateObject = _taggedTemplateLiteralLoose(["Hi   \n.Hello ", " world ", ""], ["Hi   \\n.Hello ", " world ", ""]);
function _taggedTemplateLiteralLoose(strings, raw) { strings.raw = raw; return strings; }
var a = 5;
var b = 10;
tag(_templateObject, a + b, a * b);
```
Here, Babel creates a field ***_templateObject*** which is an array of all the String components of the template broken down. The ***tag*** function is called the  ***_templateObject*** string array and the passed template variables. Now the ***tag*** function can process and return the final string.

## Destructuring
Destructuring is a convenient way to extract values from data stored in (possibly nested) objects and arrays. 

#### Arrays
Simples form of array destructuring just assigns variable1 through variableN value of corresponding item in the array, including any nested items.
```javascript
let [a, , b] = [2,3,4, 5]
```
Gets converted to
```javascript
var _ref = [2, 3, 4, 5];
var a = _ref[0];
var b = _ref[2];
```
It just assigns the array to a temp variable (if the array is not assigned to any variable) and then uses that variable to assign the values.

It can also be used for nested structures
```javascript
let data = [[2]];
let [[a]] = data;
```
Gets converted to (slightly formatted)
```javascript
var _slicedToArray = function () { 
  function sliceIterator(arr, i) {
  var _arr = []; var _n = true; var _d = false; var _e = undefined;
  try {
    for (var _i = arr[Symbol.iterator](), _s; !(_n = (_s = _i.next()).done); _n = true) {
      _arr.push(_s.value); if (i && _arr.length === i) break;
    }
  } catch (err) { _d = true; _e = err; } finally { try { if (!_n && _i["return"]) _i["return"](); } finally { if (_d) throw _e; } }
    return _arr; 
  }
  return function (arr, i) {
    if (Array.isArray(arr)) { return arr; }
    else if (Symbol.iterator in Object(arr)) { return sliceIterator(arr, i); }
    else { throw new TypeError("Invalid attempt to destructure non-iterable instance"); }
  };
}();

var data = [[2]];
var _data$ = _slicedToArray(data[0], 1);
var a = _data$[0];
```
This is a bit more complicated. _slicedToArray is used when there are any iterator needs to be destructured. It creates a temp array, pushes values into that array and uses that for destructuring.

#### Objects
Object destrucutring works in the same way
```javascript
var {a, b} = {a: 3, b: 5}
```
Gets converted to
```javascript
var _a$b = { a: 3, b: 5 };
var a = _a$b.a; // a = 3
var b = _a$b.b; // b = 3
```
Babel here is just assigning the fields from the object to be destructured based on the variable names.

We can also provide other the name of property being bound to
```javascript
var {a: myA, b} = {a: 3, b: 5}
```
Gets converted to
```javascript
var _a$b = { a: 3, b: 5 };
var myA = _a$b.a; // 3
var b = _a$b.b; // 5
```
Pretty straightfoward.
