# Functions, Callbacks & Closure
In this file, I will clarify how functions in JavaScript work and introduce the first class object. Alos, I will explain callback functions and how they collaborate with the higher order function. In addition, I will explain a new function format called arrow function. Finally, I will deeply illustrate closure in JavaScript.

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

## How functions in JavaScriot work

When we add a function, its global parts go to the global memory, and its local parts go to the local memory, and the function itself goes to the lowest part of the call stack. When we execute the function and become in the execution context, the result of the function will be deleted from the local memory and it goes to the global memory so that we get the result of the function.

##### Example
```javascript
Function  copyArrayMultiplyBy2 (array){
Output=[]
For(let i=0;i<array.length;i++){
output.push(array*2);
}
Return output;
}
const myArray=[1,2,3];
const result= CopyArrayMultiplyBy2(myArray);
```

![table1](https://github.com/MaramNaqeeb/Mastering_JavaScript_in_20_Days/assets/111737471/8b5ae447-41a0-41c7-8c4c-132c02da1e7a)



