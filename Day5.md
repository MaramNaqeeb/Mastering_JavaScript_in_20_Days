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

