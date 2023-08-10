# Conditionals, Map &Filter
in this file, I will show how to write conditional statements using different syntax in addition to some logical operators that are used in conditional statements. Furthermore, I will introduce some important and useful methods used with arrays such as map, filter, and spread operator.

## Conditions
- ### ``` if ``` & ``` else ``` statements
  ``` If ``` statement lets us execute code under a certain condition
  ``` else ``` statement lets us run other code if (condition) is false
  ##### Example
  ```javascript
  const employee={
  name:”John”,
  age:12
  }

  if(name){
  return employee.name;
  }else{
  Console.log(“there is no name”)
  }

  ```
- ###  ``` else if ``` statement
  ``` else if ``` accounts for multiple conditions in which it has another condition.
  ##### Example
  ```jacascript
  function compare(x,y){
  if(x>y){
  console.log(“x is greater than y”)
  }else if(x<y){
  console.log(“x less than y”)
  }else {
  console.log(“ x is equal y”)
  }
  }
  ```
- ### truthy loosey
    
    If we pass any kind of data types rather than Boolean, js will convert it to Boolean and consider it true 
    ##### Example
    ```javascript
    if(name){
    return employee.name;
    }else{
    console.log(“there is no name”)
    }
    ```
    Here (name) means that the existence of name=true
## Logical Operators 
  - Boolean logical operator ``` ! ``` for negation (gives the opposite of the value)
    ##### Example
    ```javascript
    let x=false
    If(!x){
    console.log(“Hi”)
    }
    ```
    Here !x means x becomes true
 - The logical operator and  ``` && ```
   
   Sometimes we take into consideration the truthiness of more than one value such as the case of using the operator ``` && ``` which must fulfill both conditions      at the same time.

    ##### Example
    ```javascript
    If(you.happy && you.knowIt){
    console.log(“I am happy because I know it”)
    }
    ```
  - The logical operator or ``` || ```
      
    The logical operator or``` || ``` erquires only one value to be truthy.

  - Ternary operator
    
      The conditional ternary operator is a shortcut fro writing quick conditions without the use of the if statement. 
      ##### Its syntax:
      ``` Condition ? valueIfTrue : valueIfFalse; ```
      
      ##### Example
      ```javascript
      let mood=forecast===”sunny” ? ”happy” : “sad”
      // Instead of 
      let mood;
      If (forecast===”sunny”){
      mood=”happy”
      }else{
      mood=”sad”;
      }
      ```
## Loops
Loops Let us run the same chuck of code multiple time. In other words, they allow us to iterate through code.
##### Example
```javascript
for(let rep=0;rep<10;rep++){
console.log(“now doing rep”, rep);
}
console.log(“do you even lifts bro”)
```
## Method with Arrays
- ### Map
  Map takes an array and a function and calls that function on each item in the array. Instead of mutating the original array, it gives a new array with the result the function called on each item in the array.
    ##### Example
  ```javascript
    const spices =[
    {name:”Jane”, nickname:”Baby”},
    {name:”Ann”, nickname:”Ginger”},
    {name:”John”, nickname:”Scary”},
    ]
    const nicknames=spices.map(s => s.nicknames+ “spices”);
    ```
    #### string template literals 
    We can use the back ticks ``` `` ``` to insert different variables inside a string using ${variable} instead of using + operator 
    ##### Example
    instead of 
    ``` const nicknames=spices.map(s => s.nicknames+ “spices”); ``` 
    
    we can say:
    ``` const nicknames=spices.map(s => `s.nicknames  ${spices}`); ```

- ### Filter
      Filter calls a true/false function on each item and creates a new array with only the items where the function returns true.
      ##### Example
     ```javascript
     const spices =[
     {name:”Jane”, nickname:”Baby”},
     {name:”Ann”, nickname:”Ginger”},
     {name:”John”, nickname:”Scary”},
     ]
     const mels= spices.filter(s=>s.name.includes(“mel”));
     ```
- ### Spread Operator ``` ... ```
  
   Spread operator takes items from an array and spread them around in which it makes a copy of an array. We can use it to expand an array by putting an array       inside another array.
  
   ##### Example
     ```javascript
      const num1=[1,2,3]
      const num2=[4,5,6]
      const nums=[…num1,…num2]
      //which is the equivalent to 
      const nums=num1.concat(num2)
     
     ```







