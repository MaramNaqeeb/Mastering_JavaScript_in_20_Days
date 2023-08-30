# Object Oriented Programming(OOP) in JavaScript
In this file, I will demonstrate the meaning of OOP and some practical concepts that belong to it which include: prototype, ``` __proto__ ```, dot notation, ``` Object.prototype() ```, ``` Object.create() ```, ``` this ``` keyword, and ``` new ``` keyword. Moreover, I will illustrate four ways of creating objects in JavaScript.

## OOP 
OOP is the opposite of functional programmnig in that functional programming has to do with data and functions that deal with each other without using objects, unlike OOP which is a programming paradigm that allows us to put data and functions inside one unit called an object. Thus, in order to bundle the data with the functionality in one package or organize data structure, we can store the data in an object and access it through the dot notaton which is the notion of encapsulation.

## Ways to create empty objects in js:
 ### Dot Notation
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
### Function Object
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

   The fundamental wrong with this approach is that we store the same function many times, so the code of the function increment() 
    for the two users is identical in which when we create new objects that function will be inside all of them identically, so we
    lose lines and space of memory in the case of a large number of users. Another problem with this approach is that if we want to 
    add a new feature to the object, we have to add it to every user.
          
  #### Generate objects using a function
   - Problems: Each tine we create a new user we make space in our computers’ memory for all our data and functionsm, but
      our functions are just copies 
   - Benefits: it is simple and easy to reason about.
    
  ##### To solve that problem, we need to create one function to be used without making a copy of it when we want to use it with objects; this is called prototype chain.
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
Under the newUser object there is a hidden property called ``` __proto__ ``` which links the object to the functionStore function. This is called prototypal feature, which means when the object does not find a function or data on the object, it goes to ``` __proto__``` property or reference and looks at what it is linking to such as a function or data. This will solve the avoid the problem of wasted memory space. Thus, js has a prototypal nature, which is the ability for objects to connect to other objects.

## ``` hasOwnProperty() ``` Method
Old headline object called Object.prototype() it has a punch or useful functions that are used in our objects because all objects in js has the hidden property ``` __proto__ ``` which link objects to the functions in the object.property such as hasOwnProperty().

##### Example
```javascript
function userCreater(name,score){
const newUser =Object.create(functionStore);
newUser.name=name
newUser.score=score
return newUser
}
const functionStore={
incerement:function() { return this.score+=1},
login: function(){console.log(“log user”)}
}
const user1=userCreater("Will",3)
const user2=userCreater("Jane",11)
user1.hasOwnPropert("score")
```
## ``` this ``` keyword 

``` this ``` refers to the current object in which it enables us to attach the objects in the global memory to that local current object that this refers to. So, in the following example, this keyword is attached to the global object function which is in our example userCreator(); therefore, this keyword will evaluate to the new created object and in our example it evaluates to user1 and user2.
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
    function add() {
      return this.score ++;
    }
    add();
  }
}
const user1 = userCreater("Will", 3);

const user2 = userCreater("Jane", 11);
user1.incerement();
```
Note: we can return the value of score++ by add() function or by using call() or reply() methods.

## Arrow function style:
It is a new shorten style for declaring and saving functions.

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
    const add = () => {
      return (this.score += 1);
    };

    add();
  },
};
const user1 = userCreater("Will", 3);
const user2 = userCreater("Jane", 11);
user1.incerement();
```
 ### ``` new ``` keyword
The third way to create objects in js is by using the ``` new ``` keyword which is used to automate so much stuff in which it automatically creates and returns an object  and it makes a link to some objects automatically, and that object that it is automatically created is called this, so instead of returning newUser in the example, we can simply return this.

##### Example
```javascript
function userCreater(name, score) {
  this.name = name;
  this.score = score;
}
userCreater.prototype;
userCreater.prototype.increment = function () {
  return (this.score += 1);
};

const user1 = new userCreater("Will", 3);
const user2 = new userCreater("Jane", 11);
user1.incerement();
```
#### Explanation
- In the above example, we create the obj ``` this ``` with the help of ``` new ``` keyword, so the user1 object will not be linked to the function increment but to the prototype property instead which is itself an object.

- In the above example there is no need to return an object out because we can run the function with the help of the new keyword or modifier. Also, we need a function that store out functions which is the prototype property. 

- In the global memory we, we have the function userCreator() that has an implicit object combo that has a prototype property which is an object itself and we store our functions inside the prototype object. And finally we declare the objects user1 in the global memory. After that we can initialize our object user1 using the new modifier. In the local memory we assign the values of the properties name: ‘Will’, and score:3. We declare an empty object assigned by this (we do not do that once).  Inside it we have a hidden proto property that will link to prototype object. Then we fill the empty object with the values of the object user1. After that, we return this object into our user1 object in the global memory with the values and the proto property which is linked to the prototype object. For the increment function of user1, it goes to the object user1 to find that function, it does not find it, but there is a proto property that is linked to the prototype object which stores the increment function there.
  
##### Problem:
The problem with this third way of creating objects is that 95% of developers do not know how it is working under the hood, and also it is not a smart design move in which if I forget the new keyword, his will point to the global object. However, Developers help each other out by capitalize the function after the keyword new
##### Benefit: 
Faster to write.

### The class "syntactic sugar"
In the third way of creating objects, the prototype property and user1 object are stored together, but they are not declared together in which we run them separately. However, in this forth way of creating objects, we can run them into one construct or format through using what is called a class.
##### Example
```javascript
class UserCreator {
  constructor(name, score) {
    this.name = name;
    this.score = score;
  }
  increment() {
    return (this.score += 1);
  }
  login() {
    console.log("logni");
  }
}
const user1 = new UserCtreator("Will", 3);
user1.increment();
```
In the above example, everything is wrapped in the class constructor is the function object combo, so it looks prettier and more readable without any other differences.
