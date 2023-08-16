# Asynchronous & Promises
In this file, I will continue talking about asynchronous in js especially the callback queue and event loop. Furthermore, I will deeply explain promises in js, which is one of the most important concept in js in which I will focus on fetch method. Also, I will introduce the problems and the benefits of promises.

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
## Promises
Promise in js is a placeholder object that is returned as a result of the consequence between the js and the web browser in an asynchronous operation.

Making consistency or map between what is going happening on the web browser and the js. I will explain that through an example. If we send A network request to fetch a data from the internet, so the network in the web browser will send a request to the internet to get data, and therefore, it is going to have a consequence immediately in js as well in that the fetch label in js is going to trigger speaking to the internet sending a request of data and simultaneously in js land is going to return out a special kind of object or a placeholder object called a promise object that is going to sit in memory, and when the background work (web browser action) is done, it is going to fill in and update that object’s data in js land with the data from the background. Thus, when the background work finishes, we will have a result back in js because we have a two pronged façade function which has a consequence in the web browser and in js as well. So, we can know what is happening in the web browser because we have it in the js land because of that mapping.

##### Example
```javascript
function display(data) {
  console.log(data);
}
const futureData = fetch("https://twitter.com//will/tweets/1");
futureData.then(display);
console.log("Me first");
```
### Explanation of the above example: 
At zero millisecond,  in the global memory, we put the function display and declare the const of futureData, so the first prong is in js as futureData=fetch(“https://twitter.com//will/tweets/1”) in which it will return out a promise object that has two properties; an initial empty value and an empty array called on fulfilled, and those two properties are also in the fetchData that is in the global memory. The other consequence or prong is in the web browser as XML or as HTTP request or generally a network request. The domain name(Twitter.com) and the path(/will/tweets/1) in the url will go to the network and ask for data from the internet. When it is complete after some milliseconds of time, instead of having a function that receives the data from the web browser, it goes and set up in js placeholder object that is called promise object, so we can get the response data in the value property that is stored into fetchData object, so the futureData.value will be updated with the response data because it is immediately linked to the background. 

However, we need to make js runs a code automatically to use it after get the data into the value property. This happens when we put any function or code in the empty array property that is called fulfilled in which we can store functions in a list, for example. So, any function in that array will be triggered to run when the value property gets updated(has a value from the url). Thus, the value property will be auto inserted as an input or argument to fill in the parameter of any function that is stored in the array.

#### How to get the display function into the fulfilled array in the above example? 
We cannot use fulfilled.push(display(data)), because that array is hidden, but there is in js a method that allows us to do so which is ``` .then ```, so we can use the following command line:

``` futureDta.then(display) ``` . This line will take the data in the display method and push it into the fulfilled array.
#### How to delay the function display data from the fetched data from futureData

##### Example
```javascript
function display(data) {
  console.log(data);
}
function greeting() {
  console.log("hi");
}
function blockForSec() {}
setTimeout(greeting, 0);
const futureData = fetch("https://twitter.com//will/tweets/1");
futureData.then(display);
blockForSec();
console.log("Me first");
```
### Explanation of the above example:
At 3002ms, "Me first" will get consoled after calling the blockFor300ms, at 3003ms, the data fetched will will be displayed, and finally, at 3004ms, the function greeting will be executed and "hi" will get consoled. 

Note: Any function is attached to a promise object by one of the two prongs for store functions which gives a promise object will go to the micro-task queue. Also, any function that is passed in directly to a façade function that triggers a web browser feature such as setTimeout will go to the callback queue when they are complete in the background web browser.

### Promises problems: 
99% of the developers have no idea about how they are working under the hood
Debugging becomes super hard as a result
Developers fail technical interviews 

### Promises Benefits
Cleaner readable style with pseudo-synchronous style code
Nice error handling process by the method .catch()




