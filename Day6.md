# Data Fetching, Promises, Destructuring, Asynch, & Modules
This file is a bit heavy in which it introduces some important and a bit complicated concepts in javascript. First of all, I will show how to fetch data using API, and how to get the values from that API using promises. Moreover, I will illiustrate what is destracturing and how we can implement it. Then, I will go more deeply in asynch and finally I will demonstrate how we can organize our code into files using modules.


## Data Fetching (APIs)
APIs provide URLs that point at data. 
##### Example
```javascript
{
“message”:[
“orange”,
“banana”,
“apple”
],
“status”:”success”
}
```
#### To get the data from APIs we use a built in function called fetch(url) lets us load data from somewhere in the internet using js (from APIs)
##### Example
``` fetch(“https://dog.ceo/api/breed/hound/list”); ```
#### to get the values of the fetch data we use promises

Promises are used when we are doing of looking for something that needs a long time in which it has to do with event loop and asynchronous code.
As fetching for data takes a long of time, we need to use promises to get the data from the url.

### 3 Possible States of promises 
- Pending  : it is still waiting for the value hang tight
- Fulfilled : it finally got the value 
- Rejected : it could not get the value

#### Sometime we want our program to wait for data to be fulfilled  before keep running the code, so we use ``` await ```
``` await ``` lets us tell js to stop and wait for an asynchronous operation to finish.
In the case of a promise, it waits for it to resolve before continuing with the code.
##### Example
```javascript
let response=await fetch(“https://dog.ceo/api/breed/hound/list”)
console.log(response);
```

