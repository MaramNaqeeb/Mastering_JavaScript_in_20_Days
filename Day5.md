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

