# Asynchronous & Promises
In this file, I will continue talking about asynchronous in js especially the callback function. Furthermore, I will deeply explain promises in js, which is one of the most important concept in js. I will focus on callback queue and event loop, and fetch method.

## Callback queue & Event Loop

For loop for an array that has a large number of elements, which can block the thread for one second and sit on the call stack after running.
##### Example 
```javascript
var x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18];
function greeting() {
  console.log("hi");
}
function blockForSec() {
  for (i = 0; i < x.length; i++) {
    console.log(x[i]);
  }
}
setTimeout(greeting, 0);
blockForSec();
console.log("first");
//the output: 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18, (after a second) first, (after a second) hi
```
### Explanation:
In the global memory, there will be the function greeting and the function blockForSec. The setTimeout that has nothing to do with js, triggers the web browser and switch on the timer there using the time set and the called back function in the setTimeout. So, at 0 millisecond, the timer is complete. Therefore, the function greeting will go to the call back queue, because it is a call back function. Then, at 1 millisecond, the function blockForSec will go to the call stack and it will take 1000ms there and console log what is inside it, and then at 1001ms, the blockForSec will go out of the call stack, the console.log(“first”) will be executed and printed in the console, and then at 1002ms, the function greeting will go to the call stack and “hi” will be printed in the console. Thus, when the global execution context is done, i.e., all the synchronous or all regular execution is done even if it is a million of concole.log. In other words, when the blockForSec is excuted and got out of the call stack, the function greeting goes to the call stack.
#### Call back hell
The problem of call back hell is that the response data is only in the callback function and maybe it feels a little odd to think of passing a function into another function only for it to run much later. Also, the error handling in this approach is not clean unlike promises. However, it is super benefit once we understand how it works under the hood. 
##### Example
```javascript
var x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18];
function greeting() {
  console.log("hi");
  function blcoCode() {
    for (i = 0; i < x.length; i++) {
      console.log(x[i]);
    }
  }
  blcoCode();
}
setTimeout(greeting, 1000);

console.log("first");
```
