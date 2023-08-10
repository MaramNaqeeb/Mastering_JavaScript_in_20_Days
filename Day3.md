# Arrays, Objects, and Variables
In this file, I will define what array is and what methods we can use to deal with arrays. Also, I will demonstrate the differences between arrays and strings, let and const, push and concat ragarding mutation. Moreover, I will explain what object is and how to access its values and mutate it in addition to illustrating ``` this ``` keyword, the nested objects, and the built in objects.

## Arrays  
An array can be defined as keep multiple values together in a single collection(list).
#### Example:
``` let fruits=[“orange”,”apple”, “strawberry”] ```

``` .length ``` is used  get the number of the element in an array.

``` .indexOf() ``` is used to get the index number of the first occurance of a specific element in an array.

``` [index] ``` To access a particular value in an array we use the index of the value in querly brackets 

## Methods with Arrays

- ``` .includes() ``` to search for a value in the array 
  #### Example 
  ``` fruits.includes(“orange”) ```   the output: true

- ``` .pop() ``` to remove the last item in an array
  ##### Example
  An array can be defined as keep multiple values together in a single collection(list).
  ##### Example:
  ``` let fruits=[“orange”,”apple”, “strawberry”] ```
  ``` let lastItem=fruits.pop() ``` "strawberry" will be removed

 - ``` .push() ``` to add an item to the end of an array
    ##### Example:
   ``` let fruits=[“orange”,”apple”, “strawberry”] ```
   ``` let lastItem=fruits.pop("banana") ``` "banana" will be added

 - ``` .sort() ``` to sort the strings alphabetically
    ##### Example
    ``` [“c”,”a”,”d”,”b”].sort() ```
    It sorts the strings alphabetically 
    The output: ``` [“a”,”b”,”c”,”d”] ```

    Note: ``` .sort() ``` function should be written in a different way when we deal with numbers.

- ``` .join() ``` It joins the values in an array using a string joiner that we pass in.
    ##### Example
    ``` let animals=[“lion”,”tiger”,”bear”].join(“ & “) ```
    The output: “lions & tigers & bears”
    Instead of:
    ``` Animals[0]+” & “ +animals[1]+” & “ + animals[2] ```
    The output: “lions & tigers & bears”

- ``` .concat() ``` It squishes/concatenates/ joins/merges two arrays together into a single array.
    ##### Example
    ``` [1,2,3].concat([4,5,6]) ```
    The output: [1,2,3,4,5,6]

## Mutation

- #### Let .vs const
``` let ``` can be reassigned while ``` const ``` cannot 
##### Example 
 ```javascript
 let x=”let”
 x=”new”
```
It will point to the new one and the value of x will become "new"

while in the case of ``` const ``` an error will be thrown 

- Assigning a mutable value to the const variable
  When we assign a mutable value to a const varible, we can make changes to that value such as an array.

##### Example:
```javascript
const x=[4,6]
X[0]=5
console.log(x)  // the output: [5,6]
const newSum=x[0]+x[1]
console.log(newSum) //the output:11 
```
- assigning an array to another array results in making them point to the same array reference and if any change happens in one of them the other will be changed; they are dependent on each other.
##### Example
``` javascript
let array1=[1,2,3]
let array2=array1
array1[0]=4
array1   // the output: [4,2,3]
array2   // the output:  [4,2,3]
```
- Arrays are mutable while strings are not
  ##### Example
  ``` javascript
  let letters=[“a”,”b”,”c”]
  letters[1]=”d”
  d replaces b
  we reassigned the value in the index 1 with “d”
  [“a”,”d”,”c”]
  ```
  While
  ```javascript 
  Let abcString=”abc”
  abcString[1]=”d”
  ```
  Will still “abc” with no errors because js in loosey 

## ``` .concat() ``` .vs ``` .push() ```
``` .concat() ```  does not change the original array but rather it returns a new array keeping the original one as it is. Thus, it returns to a new array. In other words, it creates a new copy of the array that gives a new thing.
##### Example
```javascript
let number2=[1,2,3];
let result2=number2.concat([4])
```
the output:

result2=[1,2,3,4]

//While

number2=[1,2,3]

``` .push() ``` changes the original array. Thus, it still points to the original array in which it returns the same array (manipulate that original array to be something else) it mutate the array or change the array in place.
##### Example
```javascript
let number1=[1,2,3];
let result1=number1.concat([4])
```
the output:

result1=[1,2,3,4]

//And 

number1=[1,2,3,4]

## Objects
An object is a collection of properties that point to values of diffrent data types.
##### Example:
```javascript
const js={
name=”javascript,
isAwesume: true,
birthYear:1995,
creator: “Brendan Eich”
}
```

##### Note: do not forget the comma between one property and its value and the other in the obj to separate them.

### To access the javascript value we write the following line:
``` js.name```    the output: “javascript”

OR

``` js["name"] ```   the output: “javascript” //do not forget the " " inside the []

Note: We name the properties of object using string while in arrays we name properties numerically.Therefore, as we cam access a value of an object using [“property”], In arrays we can use [“index”] because arrays are objects indeed.


#### Objects are mutable like Arrays:

- We can reassign the properties point to a diff value in the obj new value
##### Example
```javascript
const indecisive={
lunch:”sandwishes”
}

let lunch=”tacos” 

indecisive.lunch  //the output: "tacos"
```
- We can also assign/add a new property to the object.

##### Example:
``` javascript
const indecisive={
lunch:”sandwishes”
}
indecisive.snack=”chips”
```
The output:
{ lunch:”sandwishes”, snack:”chips”}

## Function Property in Objects(methods)
Properties in objects can be functions that do something by using () after the name of the function.
##### Example
```javascript
const dog={
name:”Ein”,
speak:function (){
console.log(“Hi”)
     }
}
Dog.speak()
//The output: Hi Ein
```
## ``` this ``` keyword
``` this ``` keyword refers to the current object.  
##### Example
```javascript
const dog={
name:”Ein”,
speak:function (){
console.log(“Hi”,this.name)
}
}
dog.speak()
//The output: Hi Ein
```
## Nested Objects
Nested object: is an object inside another object that behaves as a value of the other object.
##### Example
```javascript
var obj1={
  obj2:  {
   name:"John",
   age:12
  }
}
//To access the name we say:
obj1.obj2.name
```
#### We can have objs inside an array and an array inside an obj 
##### Example
```javascript
const spices=[
{name:”Ema”,nickname:”Baby”},
{name:”John”,nickname:”Sporty”},
{name:”Jimy”,nickname:”Scary”},
]

Const spiceGirl={
Albums:[“spices”,”spiceworld”,”forever”],
Motto:”Girl Power”,
Members:spices  //it indicates to the previous array
}
```
## Built in objects
- ### ``` document ```
``` document.title=”tic tac toe” ```
To find out the built in values nested in document we simply can write document in our console, or use the reference MDN 

- ### ``` .push() ``` in arrays
To find out the built in methods in arrays we  simply can write Array.prototype in our console, or use the reference MDN 

- ### ``` console ``` and ``` clear()```
```javascript
console.log() is a built in js
console.warn()
console.error()
clear()
```
- ### ``` Math  ``` to get some math related functions and constants
##### Examlpe
```javascript
Math.PI  
//the output: 3.141592653589793
Math.random() // that gives a random value between 0 and 1 
```

## Learning sprint (1), week (3), day (3) delieverables
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-data-structures/copy-array-items-using-slice
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-data-structures/combine-arrays-with-the-spread-operator
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/write-reusable-javascript-with-functions
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/understanding-undefined-value-returned-from-a-function
- https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/return-a-value-from-a-function-with-return

