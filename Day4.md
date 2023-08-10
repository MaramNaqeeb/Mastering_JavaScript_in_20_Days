# Functions, Events & Handlers
This file gives an idea about functions in javascript showing its syntax. Also, It explians scopes in javascript and diffrentiate var from let regarding scoping. In addition, this file illustrate event listeners and event objects with some exercises.

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
