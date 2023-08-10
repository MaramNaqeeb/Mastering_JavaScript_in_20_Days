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
## Scope
Scope defines where variables are in play(where variable are declared)

## Types of Scopes
### - The global scope
The widest scoope is the global scope in which the variables in that scope are seen and accessed from any place in the programme.
##### Example
```javascript
var sayHi="Hi"
function greeting(){
console.log(sayHi)
}
greeting()
```
### - The narrow scope(function scope)
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
