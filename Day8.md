# Closure
In this file, I will explain the meaning of closure, its benefits, and when it is used. Also, I will illustrate what backPack is and what its benefit. Moreover, I will give an introduction of asynchronous in JavaScript. 

## What closure is
closures are an important concept that allows functions to access variables from their outer lexical environment even after the outer function has finished executing. 

In usual functions, if we run a function for the second time, it does not remember the data from the first previous execution of the function. However, functions can hold data even after execution( a persistent memory) through passing a function from another function.

##### Example
```javascript
function createFunction(){
function multiplyBy2(num){
return num*2;
}
return multiplyBy2;
}
const generatedFun= createFunction ();
const result=generatedFun(3);
```
In the above example, we have a local label multiplyBy2 inside the execution context which will be deleted,  but their functions will be returned out by the generatedFun which  is a new label  for the function that was born as function multiplyBy2 in that its runs the function mutiplyBy2 in which generatedFun has no connection the function creatFunction(it is like taking a function in another function by creating a new label for it). Therefore, we can use the function that is returned from the running with other function that is stored in the global label, and use what in the function by its new global label.

## Calling a function in the same function call as it was defined
function. Thus, when we run and save a function (inner function) inside another function (outer function), if the inner function did not find the variable that it needs, it will look for it in the outer function, because it is already running and saved inside the outer function.
##### Example
```javascript
function outer(){
let counter=0;
function inner(){
console.log(counter++)}
inner()
}
outer()
```
## Calling a function outside of the function call in which it was defined
There is a hidden scope [[scope]] that attaches the local function to its global call. Thus, when we return a local function without calling it in the same function and the function ends there after returning it and  deleting it from the call stack, we can call that function through storing it in another function global call, so that it will get back to the call stack and get run. Therefore, the data inside the function is private in that it is not accessible without running the function, and also it has a permanent memory in which the function remembers the previous running via its permanent memory.
##### Example
```javascript
function outer(){
let counter=0;
function inner(){
console.log(counter++)}
return inner;
}
const myNewFun=outer()
myNewFun()
myNewFun()
```

Note: If there is no reference to the inner function which means that there is no point in the backpack (global memory) which causes memory leaks.
memory leak: is using a space of the computer memory with a label that cannot be accessible or used anymore. As it is literally wasting space in the computer’s memory.

## Backpack & Scoping
Scope in JavaScript refers to the accessibility or visibility of variables and expressions. That means the space where an item, such as a variable or a function, is visible and accessible in your code.

Scope: is the rule in any programming language for at a given line of code, and what data do I have available to me. In other words, so those rules protect data inside functions or block of code. Those rules called lexical or static scoping, Where I save in a function determines for the rest of that life, for the life of that function whenever it gets run under whatever new label it gets, what data it will have access to when that function runs.

#### js is a  lexical statically  or scoped language

That means that if I run the function out, the data the is grabbed inside the lexical scope will stay without getting deleted after running the function. Thus, in js closure, when you save a function inside another function, when it exits, the inner function does not get deleted, but rather it brings that data to the backpack(global memory), so when we run that function, it still has access to that persistent data from its backpack.
Note: If I want to return more than one function from the outer execution, I can attach them with the backpack in an array format or object for methods.

##### Therefore we can call data in js as: Persistent lexical static scoped referenced data (PLSRD)


## Multiple closure instances
I will explain Multiple closure instances through the following example:

```javascript
function outer(){
let counter=0;
function inner(){
console.log(counter+=1)}
return inner;
}
const myNewFun=outer()
myNewFun()
myNewFun()

const anotherFun=outer()
anotherFun ()
anotherFun ()
```
##### the output: 1,2,1,2   because the backpack of myNewFun is different from the backback of anotherFun
Explanation: Individual backpacks: if we run “outer” again the returned “inner” function definition in “anotherFun”, this new “inner” function was created in a new execution context and therefore has a brand new independent backpack.

Note1: if there is no backpack of the outer execution, the output will be 1,1,1,1  because the value will be deleted in each call.
Note2: If we declare the counter in the global scope outside the outer function as following:
```javascript
let counter=0;
function outer(){

function inner(){
console.log(counter+=1)}
return inner;
}
const myNewFun=outer()
myNewFun()
myNewFun()


const myNewFun2=outer()
myNewFun2()
myNewFun2()
```
the output: 1,2,3,4 

## The benefits of using closure in js
- Closure gives our functions persistent memories of their previous input output combinations
- Iterators and generators use closure and lexical scoping to achieve the most contemporary patterns for handling data in js.
- Node Module pattern protects data inside the backpack.(use closure in the backpack)
- Asynchronous js (callback and promises) relies on closure


# Learning sprint (1), week (2), day (2) delieverables

## Question 1:

Write a closure named createCounter that takes an initial value start and returns a function. 
The returned function, when invoked, should increment the counter by 1 and return the updated value.

```javascript
function createCounter() {
  let counter = 0;
  function incrementCounter() {
    console.log(counter++);
  }
  return incrementCounter;
}
const myNewFun = createCounter();
myNewFun();

```
## Question 2:

Write a closure named calculateAverage that takes an array of numbers, nums, and returns a function. 
The returned function, when invoked, should calculate and return the average of the numbers in the array.

```javascript
function createCounter() {
  let arr = [1, 2, 3, 4, 5];
  let average = 0;
  function incrementCounter() {
    for (let i = 0; i < arr.length; i++) {
      average += arr[i] / arr.length;
    }
    console.log(average);
  }
  return incrementCounter;
}
const myNewFun = createCounter();
myNewFun();
//the output:3
```
## Question 4: 

Write a closure named compose that takes multiple functions as arguments and returns a new function. 
The returned function should apply the provided functions in reverse order, passing the result of each function as an argument to the next function.
```javascript
function subtract(x) {
  return x - 3;
}
function sum(x) {
  return x + x;
}
function composeFun(subtract, sum) {
  function incrementCounter() {
    console.log(sum(subtract(8)));
  }
  return incrementCounter;
}
const myNewFun = composeFun(subtract, sum);
myNewFun();
//the output:10
```
## Asynchronous in JavaScript
Promises is the most significant feature in ES6 in which asynchronicity makes dynamic web applications possible, and creates event loop, callback queue and web browser features(APIs).

In general, js is a single threaded language in which one command runs at a time. Also, js is a synchronous language, which means that it runs a line and finish it, then it runs the next line.

##### Example
```javascript
const num=3;
function mutiplyBy2(){
const result=inputNumber*2;
return result;
}
const output=mutiplyBy2(num);
const newOutput= multiplyBy2(10)
```
In the above example, js will run the outout function first, then the newOutout.

#### What if the program needs a long time to execute a certain command of code like fetching data from the server.
##### Example
```javascript
function greeting(){
    console.log("hi")
}
setTimeout(greeting, 1000)
 console.log("first")
//the out put: first  hi
```
In this case, js is not enough, so we need to use promises, API features, event loop, and callback in order to delay a function.
Js is run in the browser,  so beside the js features such as console and dev tools, there are some features that are not js features which include,sockets, Network requests(which is called fetch that talks to the internet), rendering Document(HTML DOM) and Timer ( like setTimeOut). Therefore, we need js to use these features. In js, we have functions that are called facade functions, which look like js, but are actually fronts or facades for browser features.  Thus, a big part of what we are doing with js is not even js.



