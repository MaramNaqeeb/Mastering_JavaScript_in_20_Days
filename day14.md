# Advanced Scope
In this scope, I will talk about the different types of scope in JS. Also, I will differentiate between the different types of variables. In addition, I will introduce an important topic in JS which is hoisting.

## Lexical scope
Scopes nested in each other, we have to think of it as related to compiler, related to, in essence, the author time decision to put a function inside another function. Thus it is decided at the compiler time not at run time. In general. JS is a lexical scoped language.

##### Example
```javascript
var teacher = "Kyle";
function otherClass() {
  var teacher = "Suzy";
  function ask(question) {
    console.log(teacher, question);
  }
  ask("why");
}
otherClass();
```
In the above example, the variable teacher is going to point at the variable teacher in the outer scope.

There is a tool called ES levels, which is a tool that analyzes the scope levels of where basically all your buckets and marbles are. 

## Dynamic scope
It exists in some languages, but it does not exist in JavaScript.

If it exists in JS it will work as in the following example:
```javascript
var teacher = "Kyle";
function ask(question) {
  console.log(teacher, question);
}
function otherClass() {
  var teacher = "Suzy";
  ask("why");
}
otherClass();
```
In the above example, from the lexical point of view, the teacher argument in the function ask() points to the variable teacher that does not exist in its own scope. However, in dynamic scope, the teacher argument will point to the variable teacher from the scope of the function otherClass() because dynamic scope asks where was the function ask() called from. Thus, the function’s reference to its variables are dependent upon where that function was called from.

To sum up, the dynamic scope is determined based upon the conditions at runtime, while lexical scope is determined at author/compile time. Also, the lexical scope is fixed and predictable, while the dynamic scope is flexible.

## Function scope
##### Example
```javascript
var teacher=”Kyle”

var teacher=”Suzy”;
console.log(teacher);	//Suzy

console.log(teacher);	//Suzy
```
In the above example, there is a name collision as we named the second variable the same as in the same scope. To fix that problem, we can wrap a function around the second variable as following:
```javascript
var teacher=”Kyle”
function anotherTeacher(){
var teacher=”Suzy”;
console.log(teacher);	//Suzy
}
anotherTeacher();

console.log(teacher);	//Kyle
```
The name collision problem is not solved that way, however, there is a core principle called least exposure or least privilege which says “you should default to keeping everything private, and exposing the minimal necessary”. There are three main problems that are solved by using this principle:
-	If we have a name collision and we used a sort of hiding, then we reduce the surface area for name collision.
-	If we hide something, it means that, no one can accidentally of intentionally misuse that thing.
-	If we hide something, like a variable or implementation details, we protect ourselves for future refactoring (we become able to refactor our code in the future without breaking the code).

##### Example
```javascript
var teacher=”Kyle”
function anotherTeacher(){
var teacher=”Suzy”;
console.log(teacher);	//Suzy
}
( anotherTeacher ) ();

console.log(teacher);	//Kyle
```
So, We need a better way to solve the name collision.

```javascript
var teacher=”Kyle”
(function anotherTeacher(){
var teacher=”Suzy”;
console.log(teacher);	//Suzy
})()				//the parentheses are to execute the function 
console.log(teacher);	//Kyle
```
In the above example, we replace the variable with the function expression to create a scope. Thus, we immediately invoke the function expression (IIFE pattern ) that runs once and then it goes away, instead of using a regular function that we might need to call many times.

Note: We can use IIFE as anonymous.

```javascript
var teacher=”Kyle”;
(function(teacher){
console.log(teacher);
})(“Suzy”);		//Suzy
console.log(teacher)	//Kyle
```
##### Another Example
```javascript
var teacher;
try{
teacher = fetchTeacher(1);
}
catch (err) {
teacher =”Kyle”;
```
So, to prevent the function  fetchTeacher() from throwing an exception, we wrap it inside try and catch. However, teacher is assigned many time, so to make it clear for the reader that the teacher only gets assigned once by using function expression in addition to try and catch as in the following example:

##### Example
```javascript
var teacher = (function getTeacher(){
try{
return  fetchTeacher(1);
}
catch (err) {
return “Kyle”;
}
})();
```
## Block scoping 
It is scoping that is done with blocks (curly braces) instead of with functions. Thus, we apply the same principle in which we put something inside of a block instead of inside of the enclosing scope because we want to hide it, so that it has fewer chances of name collision, and protect a detail, or protect future refactoring.

##### Example
```javascript
var teacher= “Kyle”;
{
let teacher = “Suzy”;	//Suzy
console.log(teacher);
}
console.log(teacher);	//Kyle
```
The above example is similar to IIFE, but here we just use curly braces block and let statement like a block scope decoration. Also, block scope has less side effects in the sense it doesn’t redefined anything about returns or breaks, so it is a lighter weight form. Moreover, blocks are not scopes until they have a let or const inside of them

#### Block scope variable:

```javascript
function diff(x,y){
if(x>y){

let temp = x;
x=y;
y=temp;
}
return y-x;
}
```
If we need an if statement or for loop in out code temporarily, we can use a temporal variable inside the if statement or for loop to tell the reader that we will use it once and we do not need it anymore by using a block scope variables let like the variable temp in the above example. However, sometimes we still need to use the variable var as in the following cases:

1. The idea is that in block scope, we need to use let variable, but the things that are not naturally a block scoped, we do not use let variable as in the following example.
  ```javascript
   function repeat(fn,n){
    var result;
    for(var i=0; i<n;i++){
    result -= fn(result,i);
    }
    return result;
    }
  ```
2. If we need to re declare a variable many times inside of the scope, we need to use var variable as in the following example:
```javascript
function lookupRecord(searchStr){
 try{
var id= getRecord (searchStr);
}
catch(err){
var id =-1;
}
return  id;
}
```
3. If we want to use let variable at the top level of our function, we can create a block scope for it.
   
### Const 
Const is better than let.

Const is not unique to JS, it is found in many language in which that is confusing. Const  means in programming languages a variable that cannot be reassigned, but we can mutate values such as:
```javascript
const teachers=[“Kyle”,”Suzy”]
teachers[1]=”Brian”  //allowed
```
So, there is a difference between mutable assignment and mutable values.
We use const only with primitive immutable values.

## Hoisting
It is just a metaphor, it is not actually exist. According to hoisting, we move the variable declaration or function calls first and then make execution.

If JS finds the variable declaration before execution that is hoisting. 
##### Example
```javascript
var student;
student;	//undefined
student=”You”;
```
This differentiates a function declaration from a function expression in which to avoid errors we need to have all the function defined before calling it. (no hoisting with function expression).
##### Example on var hoisting 
```javascript
var teacher =”Kyle”;
otherTeacher()function otherTeacher(){
console.log(teacher);	//undefined
var teacher =”Suzy”;
}
```
##### Example on function hoisting
```javascript
teacher =”Kyle”;
var teacher;

getTeacher();
function  getTeacher(){
return teacher;
}
```
Note1: It is not a good idea to assign a variable earlier in the scope before its declaration.

Note2: people feel more comfortable with function hoisting than with variable hoisting.

Let does not hoist because it throws an TDZ error because let and const hoist to a block while var hoist to a function. Also, when var says that there is a variable, it says when the scope starts, initialize it to  undefined whereas when let  hoists its variables into its block scope, it says create a location called teacher, but do not initialize it(uninitialized state, that means you cannot touch it yet until we find const or let declaration (TDZ)). 

The TDZ happens because of const not because of let in which const initializes itself to undefined and then we console that variable, you saw it undefined and then later you saw it with the value 42, this violates the concept of a const. So TDZ is mainly for const but they assign it to let as well.

# Learning sprint (1), week (3), day (4) delieverables

## ADVANCED SCOPE:

### QUESTION #1

Given the following code snippet and **explain what's happening**.

```javascript
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log("value of [i] is: ", i);
    }, 100);
}
```

The current output is: "value of [i] is: 5" five times.

The output should be: 

"value of [i] is: ", 0 "value of [i] is: ", 1 "value of [i] is: ", 2 "value of
[i] is: ", 3 "value of [i] is: ", 4

Without changing anything in the for loop's code itself, provide a solution to
fix it.
#### Solution
```javascript
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log("value of [i] is: ",(i-=1));
    }, 100);
}
```
-------------------------------------------------------------------


