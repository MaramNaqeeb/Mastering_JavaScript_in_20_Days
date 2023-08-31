# Scope & Function Expression & Advanced Scope
In this file, I will introduce a very useful topic in JS, I will explain the execution process in JS, static mode, and nested scope. Moreover, I will illustrate special types of functions which are function expressions and arrow functions.

## Scope
Scope: is where we look for things(identifiers). When JS engine processing the code, it asks What is the position of a certain variable and what scope does it belong to.
JS is not an interpreted language(executing the code line by line), but rather a compiled language(parsed).

Explanation: if there is an error in line 10 of the code, JS will throw an error before executing lines 1 through 9. Thus, it processes the code before execution. So, JS is a two-pass system not a single-pass in which we have a scope manager and a compiler to process the code first and then execute it.

Note: JS organizes scopes with functions and blocks (the units of scope).

##### Example
```javascript
var teacher =”Kyle”;		//red bucket(global scope)
function otherClass(){	//red bucket(global scope)
var teacher =”Suzy”;	//blue bucket(functional scope)
console.log(“Welcome”)
}
function ask(){		//red bucket(global scope)
var question =”Why”;	//green bucket(functional scope)
console.log(question;
}
otherClass();		//red bucket(global scope)
ask();			//red bucket(global scope)
```
Note1: having two variables with the same name is called shadowing.

Note2: all the scopes are determined at the compiled time not at the run time.

Note3: even if the var teacher =”Kyle” looks like one statement, it is actually two parts, the declaration of the variable that what the compiler handles, and the value “Kyle” that what the execution engine handles(when using the variables in the run time).

The variable teacher that is just declared and have a value assigned to, is in a target position/reference (receiving position) while question in console is in a source position/reference. Also, otherClass(); is in a source position because we are not assigning to it, but what  we must  be doing.

Note: if we pull out a variable with a value of null or undefined, then a TypeError will throw.

Thus, in JS there is two stages of processing the code, the first one, when we figure out all the scopes, and the second one when we use all that information to execute the code.

Note: JS is a two pass processing: First pass compilation second pass execution.


When we assign a variable that does not have a formal declaration using an identifier to belong to a scope, the global scope will say to it, I will create a marble with your name. It creates a declaration for it at compile time and creating it dynamically during the run time (auto global)(non-strict mode).

In the following example the global scope will create a marble for topic:
```javascript
var teacher = "Kyle";
function otherClass() {
  teacher = "Suzy";
  topic = "React";
  console.log("welcome");
}
otherClass();
teacher; 
topic;
```
### Strict Mode “use strict”
##### Example
```javascript
"use strict"
var teacher ="Kyle";
function otherClass(){
teacher ="Suzy";
topic="React";
console.log("welcome");
}
otherClass();
// JS will through a reference error, because with the strict mode, the global scope will not create a marble
// for undeclared variable as in the case of topic because it is not defined.
```
### Nested scope
##### Example
```javascript
var teacher ="Kyle";
function otherClass(){
var teacher ="Suzy";
function ask(question){
console.log(teacher, question);
}
ask("why");
}
otherClass();
ask()  
 //JS will through a reference error as there is a source referenced to a variable that is undeclared which is ask()
```
So, we have to understand the difference between the target mode and source mode in non-strict mode, but in the strict mode, there is no difference between the two references.

## Undefined vs. Undeclared 
Undefined means that the variable exists/declared but does not have a value currently.

Undeclared means never formally declared in any scope that we have accessed to (we do not have a marble for it or does not exist) in which the strict mode, it always results in those reference areas.

Nested scope is similar to a building with a big tall elevator in it in which if we go to a building searching for something, we go to the first floor, if we do not find it, we go to the next floor, and if we do not find it, we go to the next floor and so on. Thus, the first scope is the current scope where the reference is, and the top floor is the global scope.

## Function expressions
```javascript
function teacher(){}
var myTeacher = function anotherTeacher(){
console.log(anotherTeacher);
};
console.log(teacher);
console.log(myTeacher);
console.log(anotherTeacher);	//we get a reference error because it has no reference in the global scope.
```
The difference between the function declaration and function expression is that the function declaration and its name attach its marble to the enclosing scope, so we make a red marble on the line it is in whereas function expression adds its marble to its own scope, so we make a blue marble on the line it is in. Also, function expression is read only, we cannot reassign it to some other values.

#### Name function expressions
##### Example
```javascript
var clcikHandler= function(){	//anonymous function expression (more common)
};
var keyHandler=function keyHandler(){	a named function expression (it is better)
};
```
#### Why should we prefer the named function expression
-	The name produces a reliable function self-reference (recursion, etc). Any time we need a self reference to a function to access it values, we need to use a named function expression. We prefer to name the function expression over a variable in the outer scope.
-	More debuggable stack traces.(it shows up in the stack trace)
-	More self-documenting code(unambiguous and shows the purpose of the function without reading the body of the code).

We prefer the function declaration if we have more than three lines of code, but if it is less, we use function expression, unless that thing needs to be called multiple times, we use function declaration even if it is one line.

## Arrow functions
It is a feature in ES6, they are shorter.
##### Example
```javascript
//Normal function
var ids= people.map(function getId(person){
return person.id;

//Arrow function
var ids=people.map(person => person.id);

});
```
#### It is not recommended to use arrow functions as a replacement for functions, why:
-	The shorter syntax will come up with more corner cases.
-	In arrow function, to know what is the purpose of a function, we need to read its body(it is inference, we have to infer its purpose instead of being listed out).

#### Some times function declaration is more concise than arrow functions as in the following example:
```javascript
var getId=>person=>person.if;
var ids=people.map(getId);

var getDataFrom= person => getData(person.id);
getPerson();
.then(getDataFrom);
.then(renderData);
```
When we use map, we spend more characters than using the function declaration.

Note1: A function declaration has some benefits over a named function expression, but named function expressions have huge benefits over anonymous function declarations.

Note2: We only do anonymous function expression in the arrow expression form because I was getting lexical clicks.

# Learning sprint (1), week (3), day (3) delieverables

### QUESTION #2

Build a function called `preserveThis` that takes a function as input and
returns a new arrow function that behaves the same way as the input function but
preserves the original this context when used as a method of an object.

```javascript

// Example object
const obj = {
  name: 'John',
  greet: function (greeting) {
    console.log(`${greeting}, ${this.name}!`);
  }
};

const preserveThis = (func) => {
 return () =>  obj.name + func; 
}

const preservedGreet = preserveThis(obj.greet);

preservedGreet(preserveThis(obj.greet('Hello'))); // Output: "Hello, John!"

```
### QUESTION #3

Consider the 2 following examples and distinguish the different output in each
one with them with a reasoning.

**Example 1:**

```javascript
function outer1() {
  var x = 10;

  var inner1 = function() {
    console.log(x);
  };

  inner1();
}

outer1(); // Output: 10
```

> **Reasoning for example 1's output:**
When JS executes console.log(x), it looks for the value of the var x in the inner function called inner1() first, if it does not find it there, JS looks for it in the outer function called outer1(), if it finds it in outer1, JS prints the value of x which is in this case 10.

**Example 2:**

```javascript
function outer2() {
  var x = 10;

  var inner2 = function() {
    var x = 20;
    console.log(x);
  };

  inner2();
}

outer2(); // Output: 20
```

> **Reasoning for example 2's output:**  
When JS executes console.log(x), it looks for the value of the var x in the inner function called inner2() first, if it finds it there, JS prints the value of x that is in the function inner2() which is in this case 20, otherwise, it looks for the value of x in the outer function called outer2().
-------------------------------------------------------------------
