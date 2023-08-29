# Values and Data Types
This chapter gives an overview of data types of values and focuses more on strings by introducing many functions do deal with strings. Moreover, it explains the diffrent operators used in JavaScript with some exercises. Also, it gives an introduces the variables, expressions, and statements in JavaScript.

### What is Value
Value is a unit of info that have certain characteristics (data).

## Types of Values
 #### Primitive Data Types
 #### Objects

 ### Primitive data type
 It includes strings, numbers, boolean, undefined, and null.
We can use ``` typeof ``` to return a string that indicates the type of values in js. 

#### String: is a textual data type that can be represented using back text, single quote, or double quotes such as "Hello".
#### Number: is an integer or long integer such as 23.
#### Boolean: it returns true or false values
#### Undefined: it happens when the user does not assign the variable to a value mistakely.
#### Null: it happens when the user assign the variable to null value intendedly.


## Exercise  
#### Define the type of the value: 
``` false ```   Boolean 

``` “true” ```  string

``` document.title ```   string 

``` “some string”.length ```    number 

``` Null ```    null despite of the fact that in the console it returns its type as an object  

## Strings 
Strings are made up of smaller units of text called characters that spin together to form a word ,a sentence or emoji etc.

#### Some features with strings
#### 1st: ``` indexOf() ``` 
```indexOf()``` is used to return the index of the first appearance of a specific character in a string 
Example:
``` “Hello”.indexOf(“e”) ```  //the output: 1
``` “Hello”.indexOf(“l”) ```  //the output: 2

#### Case sensitive
if I ask for a lower case while I have uppercase it returns -1

If I ask to get the index of an inexistent character in a string eg “Hello”.indexOf(“c”) the result is -1

#### 2nd: ``` includes() ``` 

```includes()```  returns a Boolean of true or false of the existen characters.
#### Example:
 ``` “Hello”.includes(“lo”) ``` //the output: true 
``` “Hello”.includes(“lol”) ```  //the output: false

#### 3rd: ``` startWith() ```

```startWith()``` returns a Boolean of true or false of the first characters in a string.
#### Example:
 ```“Hello”.startWith(”He”) ``` //the output: true
```“Hello”.startWith(”lo”)```  //the output: false

#### 4th: ``` toLowerCase() ``` or ``` toUpperCase ```
``` toLowerCase() ```  it gives the lowercase version of the given string

``` toUpperCase ``` it gives the uppercase version of the given string

#### Note1:
We can ask for the index of substrings that have multiple characters 
Using indexOf with multiple characters:
``` “Hello”.indexOf(“lo”) ```  returns 3 it represents the position of those character 
``` “Hello”.indexOf(“lol”) ```   returns -1

#### Note2: we can concatenate strings using + operator

## Exercises on the Tic Tac Toe website:
#### 	Add your last name in the player listing
```javascript
document.getElementById(“p1-name”).append(”Naqib”)
//or
document.getElementById(“p1-name”).textContent+=”Naqib”
//or
document.getElementById(“p1-name”).textContent=”Maram”+” ”+”Naqib”
```

#### Retrieving the first “T” in the page title
```javascript
document.title.indexOf(“T”)  9
//so
document.title[9] //th eoutput: "T"
```
#### 	Answer whether the page title contains the string “JavaScript”

```document.title.includes(“JavaScript”)``` the output:  false  
While

```document.title.includes("JavascripT")``` the output: true  because of the capital T 
#### 	Capitalize the heading “Tic Tac Toe” 
``` document.querySelector("header h1").style.textTransform="upperCase" ```
OR

```var upperHeader= document.querySelector("header h1").textContent.toUpperCase()
document.querySelector("header h1").textContent.toUpperCase()
```

## Operators

``` + ```for add

``` - ``` for aubtract

``` * ``` for multiply 

``` / ``` for divide

## Comparison Operators
``` > ``` greater than

``` < ``` less than 

``` >= ``` greater than or equal to

``` <= ``` less than or equal to

## Equality Operators

``` === ``` strict equal operator

``` == ``` loosey-goosey equal operator

``` !== ``` strict unequal operator

``` != ``` loosey-goosey unequal operator

## OR, AND and ++ operators:
 The logical OR is represented by ``` || ```

The logical AND operator is represented by ``` && ```

To increment the counter by 1, we use the operator ``` ++ ```

## Variables

#### Variables are not boxes that contain values but rather pointers to values.

### ``` let ``` Keyword
``` Let ```: is a keyword that let us declare variables in a block scope in which we can reassign its value. 
The sign ``` = ```: is used to assign the variable to a value to the right
``` ; ```: it is used at the end of the value to indicate the end of it.

### Declaring Variables
Declaring variables means that we just declare a name for a variable without giving it a value.

#### Example: 
``` let remember; ```

So, the value of the variable remember is undefined in which it has no value in an undeliberate way. Unlike the null value, in which the value is null deliberately as in ``` let remember= null ```

### ``` const ``` keyword

Const is a keyword to declare a variable and assign a value for it in a block 

scope but without being able to reassign or change the value assigned to the const variable.

#### Example:
``` const greeting=”Hello” ```

Note1: We can write the variable names in different forms such as:
- Camel case such as validVariable(the convention way)

- Pascal case  such as ValidVariable

- Use underscore such as valid_variable

But  we cannot start the name of the variable with numbers or emoji.

Note2: We can use variables to hold some lines of code such as 
Let title=document.querySelector(“h1”)

### Statements vs expressions 

Expressions are questions that ask js for a specific value while Statements   tell js to do something or assigning a value to an already declared variable.
#### Example:
#### expression:
1+2
#### statement:
let sum=1+2;

#### There are many statements in js which include:

- Function statements
- Conditional statements
- For statements

## Learning sprint (1), week (3), day (2) delieverables
#### QUESTION #1
Consider the following JavaScript code:

What will be the output of each console.log statement? WHY?

```javascript
let a = 0;
let b = "0";
let c = false;
let d = "false";

console.log(a == b);   // the output: true  because here there is a loosey equal operator 
console.log(b === c);  // the output: false  because here there is a strict equal operator 
console.log(!!d);      // the output: true    because !!truthy returns true
```
#### QUESTION #2:
Consider the following JavaScript expression:

What will be the output of this expression? What are the steps of evaluation taken by JS?
```javascript
console.log(4 + 5 * "7");
// the output: 9
/* explanation: JS will multiply 5 by 7 without first as the multiplication is the strongest operation and
then it adds 4 to the result of the multiplication and it does not care about the quotes around number 7
*/
```
#### QUESTION #3:
Evaluate the following expression:

What will be the output of this expression? What are the steps of evaluation taken by JS?
```javascript
let result = 5 + 2 * 3 - 1;
// the output: 10
/* explanation: JS will multiply 2 by 3 first as multiplication is the strongest oparation and then it adds 5 to the
 result and then subtract 1 from the result as we the operators of the same level such as + and - work from left to right
*/
```


#### QUESTION #4:
Consider the following code:

What will be the output of each console.log statement? WHY?
```javascript 
let x = 10;
let y = '10';
console.log(x == y);     // the output: true  because here there is a loosey equal operator 
console.log(x === y);    // the output: false  because here there is a strict equal operator 
```

#### QUESTION #5:
Given the code below:

What is the value of result? What are the steps of evaluation taken by JS?
```javascript 
let num = "15";
let isPositive = true;
let result = (num > 10 && isPositive) || num < 0;
console.log(result);
//  the output: true
// explanation: beacuse of the use of the logical OR operator "||" in which if one of the options is met, the output is true
```

