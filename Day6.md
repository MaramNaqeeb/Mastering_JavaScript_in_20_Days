# Data Fetching, Promises, Destructuring, Async, & Modules
This file is a bit heavy in which it introduces some important and a bit complicated concepts in javascript. First of all, I will show how to fetch data using API, and how to get the values from that API using promises. Moreover, I will illiustrate what is destracturing and how we can implement it. Then, I will go more deeply in async and finally I will demonstrate how we can organize our code into files using modules.


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
When we put await before fetch it tells js to wait till it get the data form the url.
### The body property in the url(to get the actual values)

#### ``` await response.json() ```

response.json() reads the data and parse it as a json obj. It gives asynchronous functions
We put await in front of response.json() to get the actual values.So, We await the fetch and await the response.json()
##### Example
``` let body=await response.json(); ```

This returns an object of the actual data we need

#### ``` .then ```
``` .then  ``` is another way to work with promises to get the values 

``` .then (value)=>console.log(value) ```

Note: We can pretend that the await function of fetching data as a synchronous / regular function
## Destructuring

Destructuring is a fancy way of declaring multiple variables at once by “extracting” values from an object with their property names.
##### Example
```javascript
const spices =[
{name:”Jane”, nickname:”Baby”},
{name:”Ann”, nickname:”Ginger”},
{name:”John”, nickname:”Scary”},
]

let {name, nickname}=spices[0];
//instead of:
spices[0].name
spices[0].nickname
```

##### We can destructure arrays as well
##### Example
```javascript
const [baby, scary, sporty]=spices;

let [one, two, three]=[1,2,3]
```
Note: Ordering matter when we destructuring arrays.

##### We can ignore any extra values when we destruturing arrays.
##### Example
```javascript
let [ten, twenty]=[10,20,30,40]
let [,,thirty ]=[10,20,30,40] //use commas to skip items
```
##### We can use the spread operator to collect the items of an array to use its value later if we want
##### Example
```javascript
let[uno, …otros]=[1,2,3,4]
console.log(uno) //the output: 1
console.log(Otros) //the output:  [2,3,4] 
```
## Split Method
Split is a sting method that returns an array of substrings by splitting a string at a certain character.
##### Example
```javascript
let [first,middle,last]=” Hello Hey Hi”.split(“ “)
//The output: [“Hello”,”Hey”, “Hi”]
```
So, by destructuring I can pull out each character separately 

## Doggo Game
Lets continue our Doggo game.
#### The command lines:
```javascript
// TODO 2
    let url =
      "https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg";
    // return the breed name string as formatted in the breed list, e.g. "standard poodle"
    function getBreedFromURL(url) {
      // The string method .split(char) may come in handy
      // Try to use destructuring as much as you can

      let unsplitBreed = url.split("/")[4];
      //OR   let urlParts=url.split("/")
      //         let splitter=url[4]

      let joinBreed = unsplitBreed.split("_").join(" ");
      return [subbreed, breed].join(" ").trim();
    }
```
Note: We can reverse an array using destructuring or by using the method ``` reverse() ```.

Note: We can remove the  white space  from both ends of a string by using the method ``` trim() ```.
## Async
#### There are rules about where the await is allowed 
We need to wrap await in an asynchronous function to be able to use it.
##### Example 
```javascript
async function fetchRespose(url){
const response = await fetch(url);
return response;
}
```
## Doggo Game
Back to our game

#### Now we will complete our game by fetching for the message from the url, create buttons, and render the game.

```javascript

    // TODO 3
    // Given a URL, fetch the resource at that URL,
    // then parse the response as a JSON object,
    // finally return the "message" property of its body
    async function fetchMessage(url) {
    const response = await fetch(url);
    const body = await response.json();
    const { message } = body;
    return message;
    }
    // Function to add the multiple-choice buttons to the page
    function renderButtons(choicesArray, correctAnswer) {
      // Event handler function to compare the clicked button's value to correctAnswer
      // and add "correct"/"incorrect" classes to the buttons as appropriate
      function buttonHandler(e) {
        if (e.target.value === correctAnswer) {
          e.target.classList.add("correct");
        } else {
          e.target.classList.add("incorrect");
          document
            .querySelector(`button[value="${correctAnswer}"]`)
            .classList.add("correct");
        }
      }

      const options = document.getElementById("options"); // Container for the multiple-choice buttons

      // TODO 4
      // For each of the choices in choicesArray,
      // Create a button element whose name, value, and textContent properties are the value of that choice,
      // attach a "click" event listener with the buttonHandler function,
      // and append the button as a child of the options element
      for (let choice of choicesArray){
        const button = documnet.createElement("button");
        button.textContent=choice;
        button.name=choice;
        button.addEventListener("click",buttonHandler);
        options.appendChild(button);
      }
    }

    // Function to add the quiz content to the page
    function renderQuiz(imgUrl, correctAnswer, choices) {
      const image = document.createElement("img");
      image.setAttribute("src", imgUrl);
      const frame = document.getElementById("image-frame");

      image.addEventListener("load", () => {
        // Wait until the image has finished loading before trying to add elements to the page
        frame.replaceChildren(image);
        renderButtons(choices, correctAnswer);
      });
    }

    // Function to load the data needed to display the quiz
    async function loadQuizData() {
      document.getElementById("image-frame").textContent = "Fetching doggo...";

      const doggoImgUrl = await fetchMessage(RANDOM_IMG_ENDPOINT);
      const correctBreed = getBreedFromURL(doggoImgUrl);
      const breedChoices = getMultipleChoices(3, correctBreed, BREEDS);

      return [doggoImgUrl, correctBreed, breedChoices];
    }

    // TODO 5
    // Asynchronously call the loadQuizData() function,
    // Then call renderQuiz() with the returned imageUrl, correctAnswer, and choices
    const[imgUrl,correctAnswer,choices]= await loadQuizData();
    renderQuiz(imgUrl,correctAnswer,choices);
```
## Modules
Modules let us split big codebase across multiple files in order to make our code more organized.

##### There are some differences between script and module
- In script, we cannot use ``` await ``` outside a function, while in module we can.
- In script, we can access the variables that are inside the script scope, while in module we cannot access the variables inside the module scope.
#### ```import ``` & ``` export ```
``` import ``` and ``` export ``` are used to use modules for splitting code into files(files talk to each other).
``` export ``` pops some values up to another file, while ``` import ``` takes what the other file exports.
##### The syntax of import 
``` import { type what you want to import here} from "type the path of the file that you want to export from" ```
## Debugging
We can debug our code to know what is going on our code by printing it out in the console using some of the following code:
```javascript
console.log()
//or
console.warn()
//or
console.error()
```




