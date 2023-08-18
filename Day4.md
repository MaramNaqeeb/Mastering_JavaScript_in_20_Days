# Functions, Events & Handlers
This file gives an idea about functions in javascript showing its syntax, differentiating between parameters and argument and demonstrating arrow function. Also, It explians scopes in javascript and diffrentiate var from let regarding scoping. In addition, this file illustrate event listeners and event objects with some exercises.

## Functions
while values are things, and variables point to things, Functions do things. Thus, functions are a block of code that returns something.

## The Syntax of Functions
### Declaring a function 
We declare functions as following:
```javascript
function half(x){
return x/2    //some kind of expression 
}
```
We call functions as following:
### Calling a function 
``` const one=half(2)  //2 is the value of x ```

## Parameters .vs Arguments
Parameters behave and are named like variables, While arguments behave and look like values.

##### Example
```javascript
function(x,y){ //the parameters of the function (as pseudo variables)
return x+y; 
}
add(2,3)
```
In the above example x and y are parameters of the function (as pseudo variables), while 2 and 3 are the arguments 
passed to the function(the actual values of the function) that are get assigned to the parameters x and y that we described when created the function.

Note: Some functions do not need any parameters 
##### Example
```javascript
function getRandomNumber(){
return Math.random();
}
getRandomNumber();
```
## JS is loosey about missing/extra arguments
If we use miss an arguments of a parameter in a function, js does not through an error but rather returns NAN because the missing argument will have the value of undefined in which adding some values to undefined values returns NAN because js is loosey about the arguments of functions.

##### Example
```javascript
function add3(x,y,z){
    return x+y+z;
}
add3(1,2)
//the output: NaN
```
However, if we pass an additional argument, js does not care and the output will stay the same because js loosey about the arguments of functions.
##### Example
```javascript
function getRandomNumber(){
return Math.random();
}
getRandomNumber(“Hi”); // the output will be a random number between 0 and 1

```
## Arrow Function
Arrow function is named arrow because of its symbol ``` => ```  which is as an arrow.

Arrow function is defined as snonymus /unnamed function that does not have much code.

##### Example
```javascript
cost add=(x,y)=>x+y;
//Which is the same as:
function add(x,y){
return x+y;
}
```
## "Quiz Project"
This project is a quiz of true or false questions with an explanation of the answers whether they are true or false.
#### The command lines to continue the project (declaring functions to disable and enable a button)
```javascript
const disable = (disabledButton) => {
disabledButton.setAttribute("disabled", " ");
};
const enable = (button) => disabledButton.removeAttribute("disabled");
```
#### The command lines to to declare isCorrect (guess) functions to compare a guess string to your fact's answer string
```javascript
function isCorrect(myGuess){
return myGuess=fact.answer.toString(); 
}
```

## Scope
Scope defines where variables are in play(where variable are declared)

## Types of Scopes
- ### The global scope
The widest scoope is the global scope in which the variables in that scope are seen and accessed from any place in the programme.
##### Example
```javascript
var sayHi="Hi"
function greeting(){
console.log(sayHi)
}
greeting()
```
- ### The narrow scope(function scope)
The varibles are declared inside the function in which the variables are not seen or accessed from outside their function
##### Example
```javascript
let globalVar="I am a global variable"
function narrowScope(){
console.log(globalVar)
let localVar="I am a local variable"
}

narrowScope() // the output: "I am a global variable"
console.log(localVar) //js will through an error as js cannot access the local variable "localVar" from outside the function
```
## Reassigning the variable of ``` let ```
We can declare variables with let in the global scope and then modify them in the narrow scope, through reassigning it in the narrow scope, but this is dangerous. 
#### Examlple
```javascript
let sayingHi=”hi”;
function greeting(){
sayingHi=”Hello”;
}
greeting()
console.log(sayingHi)
```
the output : “Hello”  //because of reassining, so the variable will point to “Hello” instead of “Hi” 

## ``` var ``` .vs ``` let ```
- Var is declared in the function scope or global scope, so they are accessed from outside the block scope
- Let is declared in the block scope such as for statement, if statement, and the code inside {}.
## Events and Handlers
### addEventListener
AddEventListener is a method that lets us listen for events on a DOM 

##### Example
```javascript
document.addEventListener(“click”,function (){
Console.log(“clicked”)
});
```
"click" is the event while the function is a call back function or what we call an event handler


### Events’ examples:
- “click”
- “dblclick”
- “mouseover”
- “mouseout”

## Learning sprint (1), week (3), day (4) delieverables
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/global-scope-and-functions
```javascript

let myGlobal=10;
function fun1() {
  // Assign 5 to oopsGlobal here
oopsGlobal=5;
}

function fun2() {
  let output = "";
  if (typeof myGlobal != "undefined") {
    output += "myGlobal: " + myGlobal;
  }
  if (typeof oopsGlobal != "undefined") {
    output += " oopsGlobal: " + oopsGlobal;
  }
  console.log(output);
}
```

- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/local-scope-and-functions
```javascript
function myLocalScope() {
const myVar="a variable"
  console.log('inside myLocalScope', myVar);
}
myLocalScope();

// myVar is not defined outside of myLocalScope
console.log('outside myLocalScope', myVar);
```

- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/global-vs--local-scope-in-functions
```javascript
// Setup
const outerWear = "T-Shirt";

function myOutfit() {
const outerWear="sweater"
  return outerWear;
}
myOutfit();
```

- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/stand-in-line
```javascript
function nextInLine(arr, item) {
  // Only change code below this line
   arr.push(item);
  const removed = arr.shift();
  return removed;
  // Only change code above this line
}

// Setup
let testArr = [1, 2, 3, 4, 5];

// Display code
console.log("Before: " + JSON.stringify(testArr));
console.log(nextInLine(testArr, 6));
console.log("After: " + JSON.stringify(testArr));
```
