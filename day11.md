# Introduction
In this file, I will make a general introduction of JavaScript starting with the data types and some of the operators used in JS. The most important thing I would like to insist on is that We should not blame JS language when we get surprised by the results of some operations using js, because we have to be aware of js specifications first such as the specification for ++ operator. Moreover, I will introduce an important concept in JS which is coercion.

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
- ### Nan : it is an acronym. This do not mean that the value is not a number, but rather it indicates an invalid number.
  ##### Example
  ```javascript
  var myCatAge=Number("n/a") 	//the output: NaN
  
  var myAge= Number("34");
  var x =myAge-"my son’s age";	 //the output: NaN
  
  myCatAge === myCatAge 	//the output: false  because NaNs are not equal to each other because NAN  is the only value
                          // in js that does not have an identity property, which means that it is not equal to itself.
  ```
#### There is a utility in js called isNaN, which checks if the value is NaN or not in which it returns either true or false. This utility coerces values to numbers before it checks for them to be NaN. 
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
var yesterday= new Date (“May 6, 2019”);
yesterday.toUTCSting(); 	//the output: “Wed,06 2019  06:00:00  GMT”

var myGPA= String(transcript.gpa);	//the output:”3.54”
```
## Coercion
Coercion can be defined as an implicit conversion from one data type to another.
Explicit Coercion: In order to make explicit coercion we use abstract opeartions, such as toPrimitive, toString, Number, and Boolean.

-	ToPrimitive(hint) takes an optional type hint

  If the hint is a “number”
  valueOf()
  toString()
  
  While
  
  If the hint is a “string”
  toString()
  valueOf()
  
  If we applied both without getting a primitive value, so an error will thro
  ##### Example
  ```javascript
  var x=[1,2,3]
  console.log(x.toString().valueOf())
  ```
-	ToString()
Is an abstract operation that takes a value and gives the representation of that value in string form.
##### Example
```javascript
  null   	// "null"
  false  	// "false"
  3		    //  "3"
  0		    //  "0"
  -0	   	//  "0"
```

  If we call toString(object), that will invoke the toPrimitive(string), which ends up calling toString() and then valueOf().
  ##### Example
  ```javascript
  []		                       // ""
  [null,undefined]		         // ","
  [[],[],[]],[]]	  	         // ",,,"
  [,,,,]		        	         // ",,,"
    {}                         // "[object Object]"  //this is the default toString on the object prototype
    {a:2}                      // "[object Object]"
   {toString(){return “X”;}}   //  “X"
  ```
-	Number () is an abstract operation that converts the value into a number.
  ##### Example
  ```javascript
  ""		          //0	//an empty string represents that there is no value there.
  "0"		          //0
  "-0"	          //-0
  " 009 "	        //9	//it removes the white spaces
  "3.14159"     	//3.14159
  "0."		        //0
  ".0"		        //0
  "."	            //NaN
  "Oxaf"	        //175
  false 	        //0
  true	          //1
  null	        	//0
  undefined	      //NaN
```
More examples on Number:
```javascript
[""]       	       //0
["0"]	             //0
["-0"]	           //-0
[null]	           // 0	//because it first becomes an empty string
[undefined]	       //0	//because it first becomes an empty string

[1,2,3]		         //NaN
[[[[]]]]		       //0
{}	               //NaN
{valueOf(){return 3;}}	 //3 	//here we override the value of an object
```
Note: The empty string is the root of all coercion evil.
- Boolean:

Boolean is an abstract operation that converts the value into a boolean.It is less algorithmic and straight lookup. We have to check if the value isFalsy() or is Truthy() in which values in JS can be categorized into falsy or truthy.

```javascript
//Falsy values:			

""				          
0				               
-0				            
Null
NaN			            
False			         
Undefined
	      	
//Truthy values:
"foo"                
23
{a:1}
[1.3]
true
function(){}
[]
{}   
```
## Cases of coercion
Do not avoid coercion for the reason that it is evil.
##### Example
```javascript
var msg1="There are";
var numStudents=16;
var msg2=" students.";
Console.log(msg1+numStudents+msg2);
//the output: "There are 16 students."
```
   - In the above example, we use a template lateral strings in which we add a sting to a number.
   - When we use the + operator and one of the values is a string, js prefers the string, so js turn the value into a string.
   - The number inside ${} will convert to a sting implicitly.
  ##### Example
  ```javascript
  var num=16;
  console.log(`There are ${num+””} students`)
  We can throw the value into an array and use join with it
  var num=16;
  console.log(`There are ${[num].join(" ")} students`)
  //Or
  console.log(`There are ${num.toString()} students`)
```
But the weird thing here is that we called a method on a primitive value, so that means that there is an implicit coercion there. However, if we do not want to do any coercion to be explicit, we can use the fundamental object String, for example, without the new keyword string.
``` console.log(`There are ${String(num)} students`) ```

if we use + operator with a string and a number, js will give us a string concatenation. To avoid that, and to make js prefer the number over the string we use + operator before the operation as the following example:
```javascript
var num=16;
var numString="5"
console.log(+numString +num)
//OR by using Number()
var num=16;
var msg="5"
console.log(Number(msg)+num)
```
  - If we use a minus operator, js prefer numbers over strings.
  - If we write an if statement that uses non-Boolean in the if class, such as checking the string is empty or not, that is called coercion.
  ##### Example1
  ```javascript
  if(studentsInputElem.value){
  numStudents=Number(studentsInputElem.value);
  }
  while (newStudents.length){
  enrollStudent(newStudents.pop());
  }
  //that is falsy
  ```
  ##### Example2
 ```javascript
  if(!!studentsInputElem.value){   		//that turns it to a Boolean, we can use Boolean(), these are useful with strings
  numStudents=Number(studentsInputElem.value);
  }
  while (newStudents.length>0){		//this converts it to a Boolean, this is useful with numbers
  enrollStudent(newStudents.pop());
  }
```
## Boxing
To access the  .length of a string value we use boxing, which is a form of implicit coercion. To access the property of a primitive value JS coerces the primitive value into an object counterpart so that we can access the properties and methods on them, so the code will become clear.


Note1:It is useful to use the implicit Boolean coercion with undefined, null, or objects, but not as much with strings, or numbers because we have some corner cases.

Note2: All programming language have conversion, and have type conversion corner cases.
```javascript
Number( “” );		//0
Number(“ \t\n”)	//0
Number(null)		//0
Number(undefined)	//NaN
Number( [] )		//0
Number( [1,2,3] )	//NaN
Number( [null] )		//0
Number([undefined])	//0
Number( {} )		//NaN

String( -0 )		//“0”
String( null )		//“null”
String( undefined )	//“undefined”
String( [null] )		//“”
String( [undefined] )	//“”
Boolean( new Boolean(false) )	//true

Note: a lot of falsy values become numbers such as null and empty string.

The root of all (coercion) evil:
StudentsTnput.value=””;	//0

Number(studentsInput.value);
StudentsInput.value=”  \t\n”;	//0 because it is full of white space because js strips off all the white spaces before doing coercion 
Number(studentsInput.value);

More corner cases:
Number(true)		//1
Number(false)		//0
1<2			//true
2<3			//true
1<2<3			//true
(1<2)<3			//false
(true)<3		//true
1<3			//true
3>2			//true
3>2>1			//false
(3>2)>1			//false
(true)>1		//false
1>1         //false
```
# Learning sprint (1), week (3), day (1) delieverables
If we call Number(object), that will invoke the toPrimitive(number), which ends up calling valueOf() and then toString().
```javascript
(for [] and {} by default);
valueOf(){return this;}	      //if value of that method  is an array or object that have not overridden,
                                //it just returns itself. Thus, it will convert the value into string.
```

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

## Question 4: 

Write a function called `compareObjects` that takes 2 arguments of type
`"object"` and compares them. If both arguments are equal, return `true`. If
not, return `false`.

If either argument is not of type `"object"`, the function should return an
array of the arguments. 

```javascript
function compareObjects(input1, input2) {
 if(Object.is(input1,input1)===Object.is(input2,input2)){
     return true;
 }else{
     return [input1,input2];
 }
}
console.log(compareObjects({name:"Jane",age:16},{name:"Ann",age:13}))
```
------------------------------------------------------------------
## Question 5: 

Write a function called `complexCoercion` that takes a single argument and
checks if its type is primitive, and if so returns a coerced value according to
the rules below.

coercion rules: 
- if input is primive and:
  - if input is a number, convert to string and then return a boolean. 
  - if input is a string, return a boolean.
  - if input is `null` or `undefined`, return `false`.

If input is not a primitive type, return the argument.

```javascript
function numberToString(x) {
  if (typeof x !== "object") {
    if (typeof x === "number") {
      x = x.toString();
      return Boolean(x);
    } else if (typeof x === "string") {
      return Boolean(x);
    } else if (x === null || x === undefined) {
      return false;
    }
  } else {
    return x;
  }
}
console.log(numberToString(5));
```
