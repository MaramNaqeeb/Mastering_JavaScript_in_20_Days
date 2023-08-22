# Introduction
In this file, I will make a general introduction of JavaScript starting with the data types and some of the operators used in JS. The most important thing I would like to insist on is that We should not blame JS language when we get surprised by the results of some operations using js, because we have to be aware of js specifications first such as the specification for ++ operator. 

## Examples on one of JS specification
```javascript
var x="5"
x=x+1		//The output: “51” it converts it to a string

//While

var y="5";
++y;     //5
y;	//6
//The output: 6   it converts it to a number
```
```javascript
var x=5
x++;       5
x;	6

//While
var x=5
++x;	6
x;	6
```
Note1: the divergence between what your mind thinks is happening and what the computer does, that’s where the bugs enter.

Note2: In js everything is an object because most of the values in js can behave as an object. For example, the value “false” can behave as an object, but that does not make it an object.

## Data Types:
- Primitive data types: string, number, big integer, Boolean, null, undefined, and symbol.(not objects).
- Objects: objects, functions, arrays.

Note: Unlike Java and C++,  in js and other dynamically typed languages, the values themselves have types not the variable(values types).

## Undefined vs. Undeclared vs. uninitialized 
- Undefined is the default value, and there is a value that has the type undefined. Undefined data type does not mean that the variable does not have a value, but it means it currently does not have a value. Undefined means that the variable is declared that has no value at the moment, but in js it is not a big deal in which it does not throw an error.
- Undeclared means that the variable is has never been created in any scope that we have access to.
- Unintialized refers to the TDZ (temporal dead zone) in the block scope while lead to an error because that value cannot be access from anywhere.

### JS operator ``` typeof ```
``` typeof ```: The typeof operator to distinguish the primitive values with their types.
##### Example
```javascript
var x;
typeof x	//the output: undefined

var y=null;
typeof y	//the output: object but the value is actually null

y =function(){}
typeof y; 	//the output: function

v=[1,2,3]
typeof v; 	//the output: object
```
Note: there is a function called isArray to find out if the value is array or not to be more specific.
```javascript
v=[1,2,3]
console.log(Array.isArray(v));  //the output: true;
```
### bigint
```javascript
v=42n
typeof v; 	//the output: bigint
```
In the above example, it is not just the number 42, but it is 42 within this space where it can grow infinitely large, up to the memory space on the system. It is not IEEE number like other numbers in JS.

## Special values
Special values are used to avoid bugs or to get more power out of our js language.
- ### Nan : it is an acronym of not a number. This do not mean that the value is not a number, but rather it indicates an invalid number.
  ##### Example
  ```javascript
  var myCatAge=Number("n/a") 	//the output: NaN
  
  var myAge= Number("34");
  var x =myAge-"my son’s age";	 //the output: NaN
  
  myCatAge === myCatAge 	//the output: false  because NaNs are not equal to each other because NAN  is the only value
                          // in js that does not have an identity property, which means that it is not equal to itself.
  ```
#### There is a utility in js called isNaN, which checks if the value is NaN or not in which ut returns either true or false. This utility coerces values to numbers before it checks for them to be NaN. 
##### Example
```javascript
isNaN(myAge) 	// the output: false
isNaN(myCatAge) 	// the output: true
OR we can use Number.isNaN to not doing any coercion to definitely assure us whether it is NaN or not.
Number.isNaN(myAge) 		// the output: false
Number.isNaN(myCatAge) 	// the output: true

isNaN(“ my son’s age”)		// the output: true
Number.isNaN(“ my son’s age”)		// the output: false
```
- ### Negative zero
  ```javascript
  var trendRate= -0
  trendRate === -0 	//the output: true;
  
  trendRate.toString(); 	//the output: “0”
  trendRate === 0 	// the output: true;
  trendRate < 0		// the output: false;
  trendRate > 0		// the output: false;
  ```

object.is( , ), which we can call it as quadruple equals which determines exactly if the value is -0 or not. Thus, if it is -0, it is true, otherwise, it is false.
##### Example
```javascript
Object.is(trendRate, -0) 		//the output:true
Object.is(trendRate, 0) 		//the output:false
```
Negative zero is useful in determining the direction of a car on a map. Thus, it shows us the direction of the car when before it stops, because when it stops, it becomes at zero, so by -0, we do not lose the sign when it becomes 0 when it stops.

Math.sign utility tells us if we have a negative zero or not.
##### Example
```javascript
Math.sign(-3)		//the output:-1
Math.sign(3)		//the output:1
Math.sign(-0)		//the output:-0
Math.sign(0)		//the output:0
Math.abs()     //returns the absolute value of a number(positive value).
```
So, knowing the type of values helps us avoid bugs and make better usage of our tool, and enables us to make our code more readable and understandable. 

## Type check exercise 
```javascript
if(!Object.is || true){
Object.is =function ObjectIs(x,y){
var xNegZero= isItNegZero (x);
var yNegZero=isItNegZero(y);
if(xNegZero || yNegZero){
return xNegZero && yNegZero;
}
else if(isItNaN && isItNaN(y)){
return true;
}else {
return x===y;
}
function isItNegZero(v){
return v==0 &&(1/0)== -infinity;
}
function isItNaN(v){
return v!==v;
};
}
}
console.log(Object.is(4,-4)==true)      //the output:false

console.log(Object.is(“foo”,”foo”)==true)	//the output:true
```
## fundamental objects
include:
- Built in objects
- Native functions

### How to use them:
- we can use some of these with the new keyword to construct an object:
Object()
Array()
Function()
Date()
RegExp()
Error()

- We cannot use some other fundamental objects with the new keyword in which we can only use them as functions not as constructors of objects:
String()
Number()
Boolean()
##### Example
```javascript
var yesterday=new new Date (“May 6, 2019”);
yesterday.toUTCSting(); 	//the output: “Wed,06 2019  06:00:00  GMT”

var myGPA= String(transcript.gpa);	//the output:”3.54”
```
# Learning sprint (1), week (3), day (1) delieverables

## Question 1:

Write a function called `convertStringToNumber` that converts a string to a
number using the unary plus operator. 

If the input is not a string, return an object of the input's value and type.

```javascript
function convertStringToNumber(input) {
 if(typeof input ==="string"){
  return +input;

}else{
    return {input:typeof input}
}
}
console.log(convertStringToNumber("34"))
```
-------------------------------------------------------------------

## Question 2:

Write a function called `checkNaN` that takes a single argument and returns
`true` if the argument is `NaN` and `false` otherwise. 

```javascript
// var value="4r5"
const checkNaN=(value)=>{

  if(isNaN(value)){
    return true;
  }else{
      return false
  }
}
console.log(checkNaN("4r5"))
```
------------------------------------------------------------------
-------------------------------------------------------------------

## Question 3: 

Write a function called `isEmptyValue` that checks if a given input is an empty value (undefined,
null, or empty string). 

```javascript
function isEmptyValue(value) {
 if(value.length===0){
   return "This is an empty string" 
 }else if(value===null){
     return null;
 }else{
     return undefined
 }
}
console.log(isEmptyValue(""))
```
-------------------------------------------------------------------

