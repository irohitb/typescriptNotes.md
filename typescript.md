
# TypeScript 

# Reference Links 

[Tutorial Point Link](https://www.tutorialspoint.com/typescript/typescript_overview.html)

[Video Link From Transversry Media](https://www.youtube.com/watch?v=rAy_3SIqT-E)


## What is typescript and why use it?

The most human defination would be. 
1. it is super set of Javascript 
2. it is an interpreted language. Hence, it needs to be run to test that it is valid
3. It compiles the code and gives error in compile time
4. Supports object orineted programming (classes, inheritance..)
5. Can improve your code quailty, error handling when compared to Javascript 

## Getting Started With TypeScript 


### Installation 

Install TypeScript globally using npm 

```
npm install -g typescript
```

### Hello World 

Create a new  `.ts` file (say `index.ts`)

Inside `index.ts` file, write a simple console.log statement 

```
let myString: String = "hello World";
console.log(myString);
```

From terminal do 
```
tsc index.ts
```
This will generate `index.js` file with following content 

```
var myString = "hello World";
console.log(myString);
```

### Getting our First Error with TypeScript 

```
let myString: String = 2;
console.log(myString);
```

Now when we `tsc index.ts` from terminal, this what we would get console 

```
index.ts:1:5 - error TS2322: Type '2' is not assignable to type 'String'.

1 let myString: String = 2;
      ~~~~~~~~
```

but this will still create Javascript file 

### Converting our typescript into Javascript in real time 
```
tsc index.ts -w
``` 

Whenever we save our typescript flag, the `-w` flag will come into play and will convert our typescript into javascript


### Array 

#### Array of types



```
let strArr: string[];

strArr = ["Rohit", "Bhatia"];

console.log(strArr);
```
Here, above we have declared Array type of string 

so if we do something like this 


```
let strArr: string[];

strArr = [5, 9];

console.log(strArr);
```

This will throw an error


We can also declare array type like this
```
let strArr: Array<string>;
```
this is equivalent to 
```
let strArr: string[];
```

### Tuple

Tuple is an array with defiend number of element 

```
let stringandTuple = [string, number]
```

and hence our Array should look like 

```
stringandTuple = ["Rohit", 4]
```

<strong> Note: </strong>  Here our third number can be anything i.e 

## Functions in TypeScript 

With function we can add type to parameters and functions return type

```
function getSum(num1: number, num2: number): number {
  return num1 + num2;
}

console.log(getSum(3, 4));
```

`:number` after parameters tell what is the return type going to be.

### Void functions in TypeScript

Void means that function won't return anything for example if we do something like this 

```
function getSum(num1: number, num2?: number): void {
  return num1 + num2;
}

console.log(getSum(3, 4));
```

Would throw an error since we are returning num1 + num2 here 

but if we do something like this 

```
function getSum(num1: number, num2?: number): void {
  return
}

console.log(getSum(3, 4));
```

then it won't throw any errors

## Interface 

Consider this function 
```
function showToDo(todo: {title: string, text: string}) {
return todo.title + ":" + title.test 
}
```
To clean this up we can create interface

```
interface Person {
  name: string;
  age: number;
}

function personDetails(person: Person) {
  return person.name + person.age;
}

let newPerson = {
  name: "Rohit",
  age: 18
};
personDetails(newPerson);
```

interface are sort of like Schema for our object/ or creating our own type 

## Classes in TypeScript 

Typescript's default target is ES5 so it transpiles to JS code that can execute on browsers as old as IE11. If you set ES6 as target, you'll notice that JS classes will be used

```
class User {
  name: string;
  email: string;

  constructor(name: string, email: string) {
    this.name = name;
    this.email = email;
  }
}

let newUser = new User("Rohit Bhatia", "iro@gmail.com");

console.log(newUser); //This is just a constructor 
```

This would be equivalent to this in ES5 

```
var User = /** @class */ (function () {
    function User(name, email) {
        this.name = name;
        this.email = email;
    }
    return User;
}());
var newUser = new User("Rohit Bhatia", "iro@gmail.com");
console.log(newUser);
```

Where @class is just a comment 

In TS classes we can also set properties to private, protected, and public. 

We will explore the difference as we move on 


### Public and Private

```
class User {
  private name: string;
  email: string;

  constructor(name: string, email: string) {
    this.name = name;
    this.email = email;
  }
}

let newUser = new User("Rohit Bhatia", "iro@gmail.com");



console.log(newUser.email && newUser.name); 
```

Here notice

```
private name: string;
email: string;
```

When we are doing private name string -> we are saying that this property cannot be accessed from outside the class and hence by the defination 

when we do `console.log(newUser.email && newUser.name);`

TypeScript will throw an error saying name is private and hence shouldn't be acessed from outside 

## Inheritance and Protected route

Using above example as our base class 
```
class User {
  private name: string;
  email: string;

  constructor(name: string, email: string) {
    this.name = name;
    this.email = email;
  }
  
   checkUserData(id: number) {
    console.log(
      "This user name is" +
      this.name +
      "his email address is" +
      this.email +
      "and his ID is" +
      id
    );
  };
  
}
```

We want to inherit properites of the above class 

To do that we use the word `extends` 

so to inherit we will write something like 

```
class College extends User {
  id: number;

  // annotate types on function parameters
  constructor(name: string, email: string, id: number) {
    super(name, email);
    this.id = id;
  }

  // a method on the prototype, not function property
  checkUserData() {
    super.checkUserData(this.id);
  };
}
```

and then we call it by doing something like this 

```
let newUser = new College("Rohit Bhatia", "iro@gmail.com", 4556);
console.log(newUser.checkUserData());
```



Understanding what is happening above 

1. We are extending College to inherit properites from User 
2. We are creating new property for user known as id
3. To use the inherit properties we user super() and specify what all properites we are going to use. 

```
 checkUserData() {
    super.checkUserData(this.id);
  };
  ```
   
4. In the above code snippet, we have are inheriting method from class User and calling it in child class College, to call the method we use `super.methodName`

<strong> Note: </strong> By defualt, typescript will compile to ES5 but if we change the defualt to Es6, you can see the equivalent code in JS having class

## The End 

With that we have went through all the major concepts of TypeScript. Again this isn't complete guide but a quick run through to understand typescript



