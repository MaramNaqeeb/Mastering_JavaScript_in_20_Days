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