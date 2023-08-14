# Functions & Callbacks
In this file, I will clarify how functions in JavaScript work and how to make them reusable. Also, I will explain callback functions and how they collaborate with the higher order function. In addition, I will explain a new function format called arrow function.

## Functions
A Function: is  code we save or define that can be run/executed later when we call it.
### Concepts related to functions
- #### Execution context
Execution context is created to  run  a function in which it has two parts;  thread of execution and memory

- #### Thread vs memory
Thread execution is executing the code line by line. We have one thread of execution that runs alongside the code

Memory mean that we store data inside string, arrays or other data types. 
- #### Call stack (a traditional way to store data)
Through call stack, Js keeps track of what function is currently running (where is a thread of execution).

When we wun a function, we add it to  the call stack, when wefFinish running the function,js removes it from the call stack.

Whatever is top of the call stack (that’s the function we are currently running

## How functions in JavaScript work

When we add a function, its global parts go to the global memory, and its local parts go to the local memory, and the function itself goes to the lowest part of the call stack. When we execute the function and become in the execution context, the result of the function will be deleted from the local memory and it goes to the global memory so that we get the result of the function.

##### Example
```javascript
function  copyArrayMultiplyBy2 (array){
output=[]
for(let i=0;i<array.length;i++){
output.push(array*2);
}
return output;
}
const myArray=[1,2,3];
const result= CopyArrayMultiplyBy2(myArray);
```

![table1](https://github.com/MaramNaqeeb/Mastering_JavaScript_in_20_Days/assets/111737471/8b5ae447-41a0-41c7-8c4c-132c02da1e7a)

## Reusable functions
- We can generalize the input values of a function to make it reusable through using parameters in the function parentheses that have arguments in the function call. In other words, we write a code(function) once, and then we can use it many times with different values when we actually run the function.
- We can generalize what the function does as the following example:
```javascript
function  copyArrayMultiplyBy2 (array,instructions){
output=[]
for(let i=0;i<array.length;i++){
output.push(instruction(array[i]));
}
return output;
}
function mutiplyBy2(input) {return input *2;}
const result= CopyArrayMultiplyBy2([1,2,3],multiplyBy2)
```


![table2](https://github.com/MaramNaqeeb/Mastering_JavaScript_in_20_Days/assets/111737471/fbb41f9c-feb5-4fc9-97ed-38eae95735fb)

#### In the example above: 
The higher order function who has everything inside of and takes in and passes another function is CopyArrayMultiplyBy2
The call back function that is inserted in another function is multiplyBy2

Both higher order function and call back functions keep our code far more dry (do not repeat yourself)
So we write the function one time and edit it after we save it because we left something a bit of it blank (we can edit the values and the code as well through the call back function)

#### Functions are first class objects 
Means that they can be treated just like objects
- We pass a function as an argument
- We can assign a function to a variable
- We can return a function as a value from functions


## Arrow Functions
In ES6, arrow functions are used to reduce code, this created legibility (nice and short) but not readability(for understanding the code). We can remove the parentheses of we have one input, and we can remove the word return. For regular functions it is recommended to use arrow functions, but for lexical scoped functions or call back functions we do as it is nice and short.

Developers care about time and the ability to reason about more than being able to automatically garbage collecting when they save some memory. On these marginal cases, readability comes first.

##### Example 

##### Regular function
``` function mutiplyBy2(input) {return input *2;} ```
##### arrow function
``` function mutiplyBy2 = input => return input *2; ```

## Pair Programming
To grow as a software engineer, some engineers avoid blocks by research and read everything can find on a block/bug,  but others use code snippets from stackOverflow to fix a bug without knowing how they work. The effective thing is pair programming in which the engineer track blocks with a partner, stay focused on the problem, refine technical communication (verbalize their code), and collaborate to solve problem

## Learning sprint (1), week (2), day (1) delieverables
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/use-higher-order-functions-map-filter-or-reduce-to-solve-a-complex-problem
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/functional-programming/apply-functional-programming-to-convert-strings-to-url-slugs
  


