
# The philpshphy of coercion & Equality & Static typing
In this file, I will continue talking about coercion. After that, I will differentiate between the double equal and the triple equal deeply depending on the data types. Then, I will explain the static typing which is TypeScript and its pros and cons.

## The philosophy of coercion
- Nothing should be type rigidly, static types, or type soundness. Thus, JS is a dynamic typing, which is not a weakness, but rather it is a strength point in which it is able to survive multi-paradigm because of its type system.

- If a function receive argument of either string or number, this means that there is an implicit coercion there.

- Comments are useful if we want to tell the reader why we did so in the code not how because that’s what the code’s for.
  
  Note: We should think of implicitness as abstraction not as a magic or a bad thing. Implicitness hides unnecessary details because that re-focuses the reader on the important stuff and increases the clarity of the code such as boxing.

  ##### Example
  ```javascript
    //Instead of saying
  var numStudents=16;
  console.log(`There are ${String(numStudents)} students.`);
  //we can simply say
  var numStudents=16;
  console.log(`There are ${numStudents} students.`);
  ```
  ##### Another Example:
  ```javascript
  var workshopEnrollment1=16;
  var workshopEnrollment2=workshop2Elem.value;
  //Instead of saying
  if(Number(workshopEnrollment1) < Number(workshopEnrollment2)){
  }
  //We can simply say
  if(workshopEnrollment1 < workshopEnrollment2){
  }
  ```
## Useful v.  Dangerous vs. Better
- The useful thing happens when the reader is focused on what is important.
- The dangerous thing happens when the reader cannot tell what will happen
- The better thing when the reader understands the code.

 # Working With Coercion

In this exercise, you will define some validation functions that check user inputs (such as from DOM elements). You'll need to properly handle the coercions of the various value types.

## Instructions
1. Define an `isValidName(..)` validator that takes one parameter, `name`. The validator returns `true` if all the following match the parameter (`false` otherwise):

    - must be a string
    - must be non-empty
    - must contain non-whitespace of at least 3 characters

2. Define an `hoursAttended(..)` validator that takes two parameters, `attended` and `length`. The validator returns `true` if all the following match the two parameters (`false` otherwise):

    - either parameter may only be a string or number
    - both parameters should be treated as numbers
    - both numbers must be 0 or higher
    - both numbers must be whole numbers
    - `attended` must be less than or equal to `length`

```javascript
function isValidName(name) {
  if (typeof name == "string" && name.trim().length >= 3) {
    return true;
  }
  return false;
}
function hoursAttended(attended, length) {
  if (typeof attended == "string" && attended.trim() != "") {
    attended = Number(attended); //to convert its type
  }
  if (typeof length == "string" && length.trim() != "") {
    length = Number(length); //to convert its type
  }
  if (
    typeof attended == "number" &&
    typeof length == "number" &&
    attended >= 0 &&
    length >= 0 &&
    Number.isInteger(attended) &&
    Number.isInteger(length) &&
    attended <= length
  ) {
    return true;
  }
  return false;
}

console.log(isValidName("Frank") === true);
console.log(isValidName(false) === false);
console.log(isValidName(null) === false);
console.log(hoursAttended(6, 10) === true);
console.log(hoursAttended(6, "10") === true);
console.log(hoursAttended("6", 10) === true);
console.log(hoursAttended("6", "10") === true);
```
## Equality 

When the types match do the triple equal. In the case of the type already match triple and double are the same. Triple equals checks the type and if it does not match it returns false, without caring about the value. So, the real difference between double and strict equality is whether any coercion is allowed to occur or not. If the types of the values match but their values are NaN, triple equals return false but it returns true if the values are negative zero. If there are two objects with the same content, neither double nor triple equals returns true because they are different objects with different reference. Therefore, double equals allows type coercion when the types are different while triple equals does not allow coercion when the types are the same.
##### Example
```javascript
var x=9
var s=8
x==s	//true
x===s 	//true
```
### Some notes on equality:
- If one of the values is null and the other is undefined, so a coercion occurs and the double equals returns true, while the triple equals returns false.
- If the type of a value is number and the other is string, we can call Number() with string (coercive equality(==) prefers the numeric comparison).
- If the double equals compare non primitive values, so we use ToPrimitive(), so double equals only compares primitives. The only time it does something with non primitives is when they are the exact same type and then it just does the same value triple equals comparison.
- When we compare a number with an array, the double equals, the array stringifies itself, so we get a number and a string, and coercion prefers numbers, so it makes numeric coercion and then the double equals returns true.

#### Coercion with primitives is not sensible. 
##### Example
```javascript
var x=4;
var y=[4]
Behind the scene:
4==”4”
4==4
x==y 	     //true
```
## Corner Cases
- ### Double equals corner cases
##### Example
```javascript
[]==![]
How this work?
[]==false  
“”==false		//convert the array into a primitive type which is a string
0==false		//convert the string into a number
0==0			//convert the Boolean into a number
```
- ### Corner cases: boolean
##### Example
```javascript
var x=[]
var y=true
x==y		//false

//How:
[]==true
"" == true
0 == 1		//false

//While
var x=[]
var y=false
x==y		//true
How:
[]==false
""==false
0 == 0		//true
```
Note1: There is no scenario in which we use double equals with true or false.
### How to avoid the corner cases with the double equals:
-	Avoid using  == with 0 or "" or even " "
-	Avoid using == with non-primitive
-	Avoid using ==true or ==false: allow Boolean or use ===
  
## The case for preferring double equals( == )
The stronger argument that you should prefer == in all possible places.
Knowing types is always better than not knowing them.
Static types in not the only (or even necessarily best) way to know your types.

-	== in not about comparison with unknown types.(we need to know the types when we use double equals)

-	== is about comparisons with knows type(s), optionally where comparisons are helpful

-	If you know the type(s) in a comparison, and both the types are the same
== is identical to ===
-	Therefore, using === would be unnecessary, so prefer the shorter and the faster ==

However, if we know the types and they are different, using === would be broken and would distract the reader.
So, if the types are different, we either do not do the comparison or we can use double equals. Thus, whether you know the type(s) or not, double equals is the more sensible choice.

Note1: Not knowing the types means not fully understanding the code, but we should be obvious to the reader that there is some uncertainty in the code by using comments.

Note2: Not knowing the types is equivalent to assuming type conversion. So, because of corner case, the only safe choice is triple equals.

Therefore, if you do not know the types, triple equals is the only reasonable choice.

## Typescript
#### Benefits:
-	Catch type-related mistakes.
-	Communicate type intend because the typing is in the code.
-	Provide IDE feedback through the tooling ecosystem that can show up live directly in your ID.

#### Caveats:
-	Inferencing is best-guess, not a guarantee. 
-	Annotations are optional in which if we do not put an annotation on a variable, typescript will default to the any type unless you have that turned off, then you are not getting any benefit out of it.
-	Any part pf the application that isn’t types introduces uncertainty.
##### Example
```javascript
var teacher =”Kyle”;
teacher ={name: “Kyle”};	//this will throw an error: can’t assign an object to a string.

//This is the same as:

var teacher: string =”Kyle”;
teacher ={name: “Kyle”};	//this will throw an error: can’t assign an object to a string.
```
The above example shows that if I do not do any typing at all, both TypeScript and Flow by default will do some static types inferencing.

#### Custom types: We can define an object of a type as in the following example:(TypeScript is helpful in this case)
##### Example
```javascript
type student={name:string{;
function getName(studentRec:student):string{
return studentRec.name;
}
var firstStudent:student={name:”Frank”}
var firstStudentName:string=getName(firstStudent);
```
#### Validating operand types :(TypeScript is helpful in this case)
##### Example
```javascript
var studenName: string=”Frank”;
var studentCount :number =16 studentName;
//this will throw an error: can’t substract string. //because coercion is not allowed here.
```
## Pros and cons of TypeScript
#### Pros
-	Make the code more obvious
-	Familiarity: they look like other language’s type system(the design the syntax)
-	Extremely popular these days. It is used in Microsoft and Facebook.
-	They are very sophisticated and good at what they do.

#### Cons
-	They use “non-JS-standard” syntax (or code comments).
-	They require a build process which easies the barrier to entry.
-	Their sophistication can be intimidating to those without prior formal types experience.
-	They focus more on “static types” (variables, parameters, returns, properties, etc) that value types.

## Summary 
JS has a dynamic type system, which users various forms of coercion for value type conversion, including equality comparison.
However, the prevailing response seems to be: avoid as much of this system as possible, and use === to “protect” from needing to worry about types.

# Learning sprint (1), week (3), day (2) delieverables

### QUESTION #1:

What will be the output of the following code snippet? Pick the right choice
then **justify your answer with an explanation**.

```javascript
function testScope1() {
  if (true) {
    var a = 1;
    let b = 2;
    const c = 3;
  }
  console.log(a);
  console.log(b);
  console.log(c);
}

testScope1();

```
**Choices:**

A) `undefined`, `undefined`, `undefined`   
B) `1`, `undefined`, `ReferenceError`  
C) `1`, `ReferenceError`, `ReferenceError`   
D) `1`, `ReferenceError`

#### Answer:
D) is the right choice because a is a variable which is a functional scope, so we can access its value if it is inside a block scope. However, we cannot access let and const values because they are block scope, so we cannot access them from outside their block scope, which results in a reference error. 
-------------------------------------------------------------------

### QUESTION #2:

What will be the output of the following code snippet? Pick the right choice
then **justify your answer with an explanation**.

```javascript
function testScope2() {
  console.log(a);
  console.log(b);
  console.log(c);
  if (true) {
    var a = 1;
    let b = 2;
    const c = 3;
  }
}

testScope2();

```

**Choices:**

A) `undefined`, `ReferenceError`   
B) `1`, `undefined`, `ReferenceError`   
C)`undefined`, `undefined`,`ReferenceError`  
D) `1`, `ReferenceError`

#### Answer:
A) is the correct answer because we var can be hoisted which results in an undefined value, while const and let cannot be hoisted; therefore, a reference error will be thrown.
-------------------------------------------------------------------

### QUESTION #3:

What will be the output of the following code snippet? Pick the right choice
then **justify your answer with an explanation**.

```javascript

function testScope3() {
  var a = 36;
  let b = 100;
  const c = 45;

  console.log([a, b, c]);

  if (true) {
    var a = 1;
    let b = 2;
    const c = 3;

    console.log([a, b, c]);
  }

  console.log([a, b, c]);
}

testScope3();

```

**choices:**

A) `[ 36, 100, 45 ]` | `[ 1, 2, 3 ]` | `[ 36, 2, 3 ]`   
B) `[ 36, 100, 45 ]` | `[1, 2, 3 ]` | `[ 36, 100, 45 ]`   
C) `[ 36, 100, 45 ]` | `[ 1, 2, 3 ]` | `[ 1,100, 45 ]`   
D) `[ 36, 100, 45 ]` | `[ 1, 2, 3 ]` | `[ 1, 2, 3 ]`

#### Answer: 
C) is the correct answer because var, let and const are declared and executed inside the fucnction scope, so the array [36, 100, 45]  will get consoled. Then, var, let and const are declared and executed inside the block scope, so the array [1,2,3] will get consoled. Then, the third console is in the function scope after the block scope; therefore, we can access the new value of var which is in the block scope, but we cannot access the const and let values that are in the block scope, so js prints the values of const and let which we can access which are in the function scope which results in printing the array [1,100,45].
--------------------------------------------------------------
