# Asynchronous & Promises
In this file, I will continue talking about asynchronous in js especially the callback queue and event loop. Furthermore, I will deeply explain promises in js, which is one of the most important concept in js in which I will focus on fetch method. Also, I will introduce the problems and the benefits of promises. Moreover, I will demonstrate the rules for the execution of asynchronous delayed code, and also the objective of Promises, web APIs, the callback and micro-task queues and event loop.

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
function blockFor300ms() {}
setTimeout(greeting, 0);
const futureData = fetch("https://twitter.com//will/tweets/1");
futureData.then(display);
blockFor300ms();
console.log("Me first");
```
### Explanation of the above example:
 After calling the blockFor300ms, and at 3002ms, "Me first" will get consoled, at 3003ms, the data fetched will be displayed, and finally, at 3004ms, the function greeting will be executed and "hi" will get consoled. 

Note: After all the global functions finished running, any function is attached to a promise object by one of the two prongs for store functions which gives a promise object will go to the micro-task queue. Also, any function that is passed in directly to a façade function that triggers a web browser feature such as setTimeout will go to the callback queue when they are complete in the background web browser.

## Promises problems: 
- 99% of the developers have no idea about how they are working under the hood
- Debugging becomes super hard as a result
- Developers fail technical interviews 

## Promises Benefits
- Cleaner readable style with pseudo-synchronous style code
- Nice error handling process by the method ``` .catch() ```


## Some rules for the execution of asynchronous delayed code:
- Hold promise-deferred functions in a micro-task queue and callback function in a task queue (callback queue) when the web browser feature(API) finishes.
- Add the function to the call stack or run the function when the call stack is empty and all global code run according to the event loop.
Note: prioritize functions in the micro-task queue over the functions in the callback queue.


## The objective of Promises, web APIs, the callback and micro-task queues and event loop
- Non-blocking applications: this means we do not have to wait in the single thread and do not block further code from running.
- However long it takes: we cannot predict when our browser feature’s work will finish so we let js handle automatically running the function on its completion.
- Web applications: Asynchronous js is the backbone of the modern web in which it lets us build fast non-blocking  dynamic applications in which we can handle a ton of staff in the background while we race on in the foreground running our code being responsive to user’s interactions.

# Learning sprint (1), week (2), day (3) delieverables

## Question 1:

You are given a function `executeInSequenceWithCBs` and some code. The task is to
modify the `executeInSequenceWithCBs` function so that it runs and executes all
the tasks inside the asyncTasks array. 

The function should return an array of messages obtained from each task's
execution.

You are only allowed to change the `executeInSequenceWithCBs` function or add new
functions/code. You cannot modify the tasks' functions.

```javascript

const task1 = (cb) => setTimeout(() => {
  const message = "Task 1 has executed successfully!";
  cb(message);
}, 3000)

const task2 = (cb) => setTimeout(() => {
  const message = "Task 2 has executed successfully!";
  cb(message);
}, 0)

const task3 = (cb) => setTimeout(() => {
  const message = "Task 3 has executed successfully!";
  cb(message);
}, 1000)

const task4 = (cb) => setTimeout(() => {
  const message = "Task 4 has executed successfully!";
  cb(message);
}, 2000)

const task5 = (cb) => setTimeout(() => {
  const message = "Task 5 has executed successfully!";
  cb(message);
}, 4000)

const asyncTasks = [task1, task2, task3, task4, task5];

const executeInSequenceWithCBs = (tasks, callback) => {}

```
-------------------------------------------------------------------
### Solution:
```javascript
let asyncTasks = [task1, task2, task3, task4, task5];
let arr = [];

var executeInSequenceWithCBs = function (cb) {
  for (i = 0; i < asyncTasks.length; i++) {
    var messagesOfTasks = asyncTasks[i];

    messagesOfTasks(cb);

    arr.push(x);
  }
};

executeInSequenceWithCBs(function (tasks) {
  console.log(tasks);
});
```

## Question 2:

You are given a function called `executeInParallelWithPromises`, which takes an
array of APIs (represented by objects). 

Your task is to write code that fetches the data of each API in parallel using
promises. In Parallel means that the api which resolves first, returns its value
first, regardless of the execution order. 

The output of the `executeInParallelWithPromises` function should be an array
containing the results of each API's execution.

Each result should be an object with three keys: `apiName`, `apiUrl`, and
`apiData`..

```javascript
const apis = [
  {
    apiName: "products", 
    apiUrl: "https://dummyjson.com/products",
  }, 
  {
    apiName: "users", 
    apiUrl: "https://dummyjson.com/users",
  }, 
  {
    apiName: "posts", 
    apiUrl: "https://dummyjson.com/posts",
  }, 
  {
    apiName: "comments", 
    apiUrl: "https://dummyjson.com/comments",
  }
]

const executeInParallelWithPromises = (apis) => {}

```
-------------------------------------------------------------------
### Solution
```javascript

const executeInParallelWithPromises = (apis) => {
  var array = [];
  function createObj(name, url, data) {
    const newObj = {};
    newObj.apiName = name;
    newObj.apiUrl = url;
    newObj.apiData = data;
  
    return newObj;
  }
  for (let i = 0; i < apis.length; i++) {
    var fetchPromise = fetch(apis[i].apiUrl);
    fetchPromise
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        //console.log(data);
        return data;
      });

    let name = `${apis[i].apiName}`;
    let url = `${apis[i].apiUrl} `;
    let data = fetchPromise;

    let x = createObj(name, url, data);

    array.push(x);
  }
  console.log(array);
};

console.log("Welcome to API");

executeInParallelWithPromises(apis);
```
## Question 3: 

You are given a function called `executeInSequenceWithPromises`, which takes an
array of APIs (represented by objects). 

Your task is to write code that fetches the data of each API sequentially (one
after the other) using promises. 

In Sequence means that the api which executes first, returns its value
first.

The output of the `executeInSequenceWithPromises` function should be an array
containing the results of each API's execution.

Each result should be an object with three keys: `apiName`, `apiUrl`, and
`apiData`.

```javascript

const apis = [
  {
    apiName: "products", 
    apiUrl: "https://dummyjson.com/products",
  }, 
  {
    apiName: "users", 
    apiUrl: "https://dummyjson.com/users",
  }, 
  {
    apiName: "posts", 
    apiUrl: "https://dummyjson.com/posts",
  }, 
  {
    apiName: "comments", 
    apiUrl: "https://dummyjson.com/comments",
  }
]

//modify and write your code here
const executeInSequenceWithPromises = (apis) => {}

```
### Solution
```javascript
const executeInSequenceWithPromises = (apis) => {
  var array = [];
  function createObj(name, url, data) {
    const newObj = {};
    newObj.apiName = name;
    newObj.apiUrl = url;
    newObj.apiData = data;

    return newObj;
  }
  for (let i = 0; i < apis.length; i++) {
    async function getData() {
      const response = await fetch(apis[i].apiUrl);

      if (!response.ok) {
        const message = `An error has occured: ${response.status}`;
        throw new Error(message);
      }

      const data = await response.json();
      //console.log(data);
      return data;
    }

    getData().catch((error) => {
      error.message; // 'An error has occurred: 404'
    });

    let name = `${apis[i].apiName}`;
    let url = `${apis[i].apiUrl} `;
    let data = getData();

    let x = createObj(name, url, data);

    array.push(x);
  }
  console.log(array);
};

console.log("Welcome to API");

executeInSequenceWithPromises(apis);
```



