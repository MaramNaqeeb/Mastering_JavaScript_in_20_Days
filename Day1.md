# Day1: Introduction & DOM
This file gives an overview of what JavaScript is, and how to write codes on the browser's JS console to interact with the DOM using CSS selectors in order to retrieve some info from the DOM and make some changes to the DOM.

## What is JavaScript
JavaScript is a programming language that interact with HTML to do some stuffs on web pages.
JavaScript is a dynamic language in which it is not directly associated with a specific data type, so that we can declare variables without specifying a certain data type to them, and we can re-assign variables to values of different data types. Also, JavaScript is a just-in-time language in that it compiles the code and meanwhile it optimizes and interprets the code.   Moreover, JavaScript is a weakly-typed language as it makes a type conversion when a mismatch happens between operations without running an error. For example, if we add a string to a number, JS converts the number to a string without running an error.

## BFFs (HTML, CSS, JS)
HTML is about the content and the structure of the web elements. 

CSS is about the positioning and designing the web elements.

JS is about the actions of the web element. 

## Where to write and run JS code:
We can write JS code on the browser’s JS console, the local text file such as TextEdit or VS code, or online playground such as CodePen or CodeSandBox.

## What is DOM 
DOM is a shortcut of Document Object Model in which JS creates an object model or entity that represents the HTML Document with its content and elements.

Note1: If we type document in the console, we get all the values and stuffs that represents HTML document to JS.
Note2: We use the dot notation to access a specific object in the document.

### Here are some examples that show how we can work with the document object from the console:
```javascript
document.title // This shows the title of the document on the browser tab.
document.body // This shows the body of the document that contains all of the document content.
document.getElementById(“board”) // This shows the element which has the id “board”
document.querySelector(“#board”) // This is another way to show the element which has the id “board”.
document.getElementByClassName(“player”) // This shows the element that have the class name “player”.
document.querySelectorAll(“.player”) //This is another way to show the element that have the class name “player”.
```
## .length & .textContent
```javascript
.length // Gives us the number of elements that a specific query selector returns

.textContent  //It types the text inside a specific element with a specific query selector.
```
Note: Instead or remembering all stuffs about HTML, CSS, or JS, you can simply use is a free resource for in-depth documentation on web standards such as HTML, CSS, JavaScript, and much more.

## Exercises in the console from Tic Tac Toe app:
#### Retrieve the p elements.
  ```javascript
 document.getElementsByTagName("p")
//the output: HTMLCollection(2) [p#p1.player, p#p2.player, p1: p#p1.player, p2: p#p2.player]
  ```
#### Retrieve the text “X”.
   ```javascript
   document.getElementById("p1-symbol").textContent
//the output: 'X'
   // OR
  document.querySelector("#p1-symbol").textContent
//the output: 'X'
   ```
#### Find the numbers of the squares in the board.
   ```javascript
   document.getElementsByClassName("square").length
//the output: 9
   // OR 
 document.querySelector("square").length
//the output: 9
   ```
#### Retrieve the text “A game you know”.
```javascript
document.querySelector("h2").textContent
//the output:'A game you know'
```
## Editing the DOM in the JS console:
What we did above is retrieving some info from the Dom in the console, but we can edit the DOM in the console as well, and here are some examples:

We can change the title of the page from “TicTacToe” to “A game to play” through the following command line:
```javascript
document.title=“A game to play”
```
We can add the name”Sofia” ,for example, to the name “Anjina” of the player “x” through the following command line:

```javascript
document.getElementById(“p1-name”).append(“ & Sofia”)
```
We can swap the symbols X and O from the app through the following command lines: 
```javascript
document.getElementById("p1-symbol").textContent="O"
document.getElementById("p2-symbol").textContent="x"
```
## JavaScript Challenges
#### 1st: Compound Assignment With Augmented Multiplication
Instead of assigning the variable to itself and multiply it to a number, we can simply use the Compound Assignment With Augmented Multiplication which can be represented by *=

##### Here is some examples:
```javascript
let a = 5;
let b = 12;
let c = 4.6;

a *= 5; //instead of a = a * 5
b *= 3; //instead of b = 3 * 3
c *= 10; //instead of c = c * 10
```
#### 2nd: Concatenating Strings with the Plus Equals Operator
We can concatinating strings using += operator at the end of an existing string variable.
##### Example:
```javascript
let myString;
myString="This is my first sentence."
myString+="This is my second sentence"
//The output: This is my first sentence. This is my second sentence.
```
### 3rd: Use Bracket Notation to Find the Nth-to-Last Character in a String
We can use bracket notation including the length of the string minus the number of the last character assigned.
##### Example:
###### Use bracket notation to find the second-to-last character in the lastName string.
```javascript
const lastName = "Lovelace";

const secondToLastLetterOfLastName = lastName[lastName.length-2];
//The output: c


