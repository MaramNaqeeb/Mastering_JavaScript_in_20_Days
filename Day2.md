# Values and Data Types
This chapter gives an overview of data types of values and focuses more on strings by introducing many functions do deal with strings. Moreover, it explains the diffrent operators used in JavaScript with some exercises.

### What is Value
Value is a unit of info that have certain characteristics (data).

## Types of Values
 #### Primitive Data Types
 #### Objects

 ### Primitive data type
 It includes strings, numbers, boolean, undefined, and null.
We can use ```typeOf``` to return a string that indicates the type of values in js. 

#### String: is a textual data type that can be represented using back text, single quote, or double quotes such as "Hello".
#### Number: is an integer or long integer such as 23.
#### Boolean: it returns true or false values
#### Undefined: it happens when the user does not assign the variable to a value mistakely.
#### Null: it happens when the user assign the variable to null value intendedly.


## Exercise  
#### Define the type of the value: 
```false```   Boolean 

```“true” ```  string

```document.title ```   string 

```“some string”.length```    number 

```Null```    null despite of the fact that in the console it returns its type as an object  

## Strings 
Strings are made up of smaller units of text called characters that spin together to form a word ,a sentence or emoji etc.

#### Some features with strings
```indexOf()```  to return the index of the first appearance of a specific character in a string 
Example:
```“Hello”.indexOf(“e”)```  //the output: 1
```“Hello”.indexOf(“l”)```  //the output: 2

#### Case sensitive
if I ask for a lower case while I have uppercase it returns -1

If I ask to get the index of an inexistent character in a string eg “Hello”.indexOf(“c”) the result is -1







