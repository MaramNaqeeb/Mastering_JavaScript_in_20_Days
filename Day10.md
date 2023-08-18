# Object Orented Programming(OOP) in JavaScript
In this file I will demonstrate the meaning of OOP and some practical concepts that belong to it which include: prototype, ``` __proto__ ```, dot notation, ``` Object.prototype() ```, ``` Object.create() ```, ``` this ``` keyword, and ``` new ``` keyword. Moreover, I wtll illustrate for ways of creating objects in JavaScript.

## OOP 
OOP is the opposite of functional programmnig in that functional programming has to do with data and functions that deal with each other without using objects, unlike OOP which is a programming paradigm that allows us to put data and functions inside one unit called an object. Thus, in order to bundle the data with the functionality in one package or organize data structure, we can store the data in an object and access it through the dot which is the notion of encapsulation.

## Ways to create empty objects in js:
- Dot Notation
  We can use the dot notation to create a new object to add properties to it afterward.
  ##### Example
  ```javascript
    const newUser = {};
    newUser.name = "Will";
    newUser.score = 3;
    newUser.increment = function () {
      return (newUser.score += 1);
    };
    
    console.log(newUser.name);
    console.log(newUser.score);
    console.log(newUser.increment());
  ```
  Note: the functions on objects are called methods.
  
  - ``` Objecct.create() ```
    If we have a code that is run multiple times like adding properties or methods, we can wrap them up in  generalize function (abstract it) which means we save that function and use it again for many times for different objects.

      ##### Example
        ```javascript
      function userCreater(name, score) {
        const newUser = {};
        newUser.name = name;
        newUser.score = score;
        newUser.incerement = function () {
          return (newUser.score += 1);
        };
        return newUser;
      }
      const user1 = userCreater("Will", 3);
      const user2 = userCreater("Jane", 11);
      user1.incerement();
      ```
      The fundamental wrong with this approach is that we store the same function many times, so the code of the function increment() for the two users is identical in which when we create new objects that function will be inside all of them identically, so we lose lines and space of memory in the case of a large number of users. Another problem with this approach is that if we want to add a new feature to the object, we have to add it to every user.
      
  #### Generate objects using a function
    - Problems: Each tine we create a new user we make space in our computers’ memory for all our data and functions. But our functions are just copies 
    - Benefits: it is simple and easy to reason about.
  ##### To solve that problem, we need to create one function to be used without making a cope of it when we want to use it with objects; this is called prototype chain.
  ## Prototype chain
  I will explan the prototype chain through the following example:
  ##### Example
 ```javascript
    function userCreater(name, score) {
    const newUser = Object.create(functionStore);
    newUser.name = name;
    newUser.score = score;
    return newUser;
  }
  const functionStore = {
    incerement: function () {
      return (this.score += 1);
    },
    login: function () {
      console.log("log user");
    },
  };
  const user1 = userCreater("Will", 3);
  const user2 = userCreater("Jane", 11);
  user1.incerement();
```
#### Explanation of the above example:
In the above example, when it does not find the increment function in the object, its newUser object and user1 object itself will have a link to the function that increment function is in and use it.
Under the newUser object there is a hidden property called __proto__ which links the object to the functionStore function. This is called prototypal feature, which means when the object does not find a function or data on the object, it goes to __proto__ property or reference and looks at what it is linking to such as a function or data. This will solve the avoid the problem of wasted memory space. Thus, js has a prototypal nature, which is the ability for objects to connect to other objects.

