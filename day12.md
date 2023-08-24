
# The philpshphy of coercion & Equality & Static typing
In this file, I will continue talking about coercion. After that, I will differentiate between the double equal and the triple equal deeply depending on the data types. 

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
