# Closure
In this file, I will explain the meaning of closure and when it is used. Also, I will illustrate what backPack is and what its benefit. 

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



