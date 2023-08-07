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
#### 1st: ```indexOf()``` 
```indexOf()``` is used to return the index of the first appearance of a specific character in a string 
Example:
```“Hello”.indexOf(“e”)```  //the output: 1
```“Hello”.indexOf(“l”)```  //the output: 2

#### Case sensitive
if I ask for a lower case while I have uppercase it returns -1

If I ask to get the index of an inexistent character in a string eg “Hello”.indexOf(“c”) the result is -1

#### 2nd: ```includes()``` 

```includes()```  returns a Boolean of true or false of the existen characters.
#### Example:
 ```“Hello”.includes(“lo”)``` //the output: true 
```“Hello”.includes(“lol”)```  //the output: false

#### 3rd: ```startWith()```

```startWith()``` returns a Boolean of true or false of the first characters in a string.
#### Example:
 ```“Hello”.startWith(”He”)``` //the output: true
```“Hello”.startWith(”lo”)```  //the output: false

#### 4th: ```toLowerCase()``` or ```toUpperCase```
```toLowerCase()```  it gives the lowercase version of the given string

``toUpperCase``` it gives the uppercase version of the given string

#### Note:
We can ask for the index of substrings that have multiple characters 
Using indexOf with multiple characters:
```“Hello”.indexOf(“lo”)```  returns 3 it represents the position of those character 
```“Hello”.indexOf(“lol”)```   returns -1




