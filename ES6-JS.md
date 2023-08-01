

## Var , Let , Const


1. `var` :   variable can be access in any scope because it is global and  can  be declared with var many times.
2. `let` :   variable can be access only through its scope and the variable declared localy and once,
3. `const` :  variable can be access only through its scope and the variable declared localy and once and it also immutable 


```javascript

function define_global_x(x){
	  // x in global 
	  var x = x
}

let y = 2 ; // i in global scope 

const arr = [1,2,3,4]

arr[0]=0 // work because the refference still as it , it unchaged we change that data the refference reffer to

// arr = [1,2] uncommenting this will through an error because is was fixed or constant and  we want to assign it to new refference



function define_local_z(){
	  // z in local scope
	  let z = 9;
}

```


## Object Freezing

- object freezing :  mean make it,s attributes readonly and unwritable . 
- Object freezing is a way to prevent an object from being modified.
- Object freezing can be done using the `Object.freeze()` method.
- Once an object is frozen, its properties cannot be added, removed, or modified.
- Object freezing can be used to protect data from being accidentally modified.
- Object freezing can also be used to improve performance, by preventing the need to check for property existence.


Example :

```javascript
let myObj = {name :"eslam" , age: 20 };

if(myObj.hasOwnProperty("name"))
    myObj.name="eslam mohamed";

// now name  is 'eslam mohamed' and note that Obj.hasOwnProberty("Prop") to know if the object has this property or not 
Object.freeze(myObj);

myObj.name="eslam mohamed elabd";

if(Object.isFrozen(myObj))
    console.log(myObj.name); // it will out eslam mohamed only because object was freezen mean any prop can,t be changed
```


## Arrow Functions

- Arrow functions are a concise way to write functions.
- Arrow functions are defined using the `=>` symbol.
- Arrow functions can be used in place of regular functions in most cases.
- Arrow functions have some limitations compared to regular functions, arrow functions cannot be used as constructors, and they cannot be used with the `new` keyword.


```javascript
let arrowFunction = (x,y) => x+y ;

let arrowFunction = (x,y)=> {
							 console.log( x + y ) ;
				             return x+y
				       }

```


## Anonymous Function

- Anonymous functions are functions that do not have a name.
- Anonymous functions are often used as callbacks.
- Anonymous functions can be created using the function keyword or the arrow function syntax.

```javascript
()=>{
	  console.log('iam anonymous')
} ;

function(){
	  consloe.log('iam anonymous')
} ;

( 
	  ()=>{
			console.log('iam self invoked anonymous')
	  } 
)() ;

( 
	  function(){
			console.log('iam self invoked anonymous')
	  } 
)() ;

function applyTwice(x,y,callback){
	  return callback(callback(x,y),y)
}


applyTwice(2,3,(x,y)=>x*y);

```

# Default Parameter 

- Default parameters are values that are assigned to function parameters if no value is passed to the function when it is called.
- Default parameters can be used to make your code more concise and efficient.
- Default parameters can help to prevent errors, by ensuring that all function parameters have a value, even if no value is passed to the function.
- Default parameters can be used to make your code more reusable, by allowing you to call the function with different values for the parameters.


```javascript

mulOne = (num=1)=> num * 1; 

// mulOne(4) will retrun 4  ,  mulOne() will return 1;

```


## Rest Operator


- rest operator, allows you to accept an indefinite number of arguments as an array. 
- It is denoted by three dots `...`.
- rest operator can only be used as the last parameter of a function.

```javascript
 let funcionWithRest = ( ...args )=>{
	  console.log("this is args length: "+args.length, "and this is args Array : "+args)
 };

funcionWithRest = (x,y,z, ...args )=>{
	  console.log("this is args length: "+args.length, "and this is args Array : "+args)
 };


```

## Spread Operator


- spread operator , is denoted by three dots `...`.
- spread operator can be used to expand an iterable into individual elements.
- An iterable is an object that can be iterated over, such as an array or an object.


The spread operator can be used in a variety of ways, such as:

- To expand an array into individual arguments when calling a function.
- To expand an object into individual key-value pairs when creating a new object.
- To expand an iterable into individual elements when creating a new iterable.

```javascript
let arr = [1,22,3,4];

Math.max(...arr); // unpacking array , Math.max(...arr) this is like to Math.max(1,22,3,4) 

let arrcpy=[...arr];    // it will copy the elements throgh get them unpacked then packed with []

arrcpy = arr.slice() ; // also copy the array

arrcpy=arr.slice(0,length)  // also copy the array

```

## Destructeing Assignments


### 1. Destructeing Assignments Extract Values from Objects

- destructing assignments allow you to extract values from objects into variables.
- This can be useful when you need to access the values of an object in multiple place

```javascript

const user = { name: "0xCrypt00o" , age: 22 } ;

let { name, age } = user ;

let { name: username , age: userage } = user ;

console.log( username , userage ) ;

const nested = { nest: user } ;

{ nest: { name: username, } } = nested ;

{ nest: { name:username, age:userage } } = nested ;

console.log( username , userage ) ;

```

### 2. Destructuring Assignment to Assign Variables from Arrays

 - destructuring assignment to extract multiple elements from an array into an array.
 - To do this, you use the square brackets `[]` after the list of variables.

```javascript

let [a, b] = [1, 2, 3, 4, 5, 6];

console.log(a, b);

[a, b,,, c] = [1, 2, 3, 4, 5, 6];

console.log(a, b, c);

[a, b, ...arr] = [1, 2, 3, 4, 5, 7];

console.log(a, b);
console.log(arr);


[a, b, , , ...arr] = [1, 2, 3, 4, 5, 7];

console.log(a, b);
console.log(arr);


```


### 3. Destructuring Assignment to Pass an Object as a Function's Parameters

Instead Of :

```javascript
let profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;
}
```

Do Like :
```javascript
profileUpdate = ({ name, age, nationality, location }) => {

}
```

## Concise Declarative Functions

Instead Of : 

```javascript
const person = {
  name: "0xCrypt00o",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

Do Like :

```javascript
const person = {
  name: "0xCrypt00o",
  sayHello(){
    return `Hello! My name is ${this.name}.`;
  }
};
```


## Concise Object Literal Declarations Using Object Property Shorthand

Instead Of :

```javascript
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
```

Do Like :

```javascript
const getMousePosition = (x, y) => ({ x, y });
```

## Strings using Template Literals

- Template literals are a JavaScript feature that allows you to create strings that can contain expressions.
- Template literals are enclosed in backticks (`).
- Expressions in template literals are enclosed in curly braces `${ }`
- The value of the expression is substituted into the string at the point where the expression is enclosed in curly braces.
- Template literals can be used to create more concise and readable code.

```javascript
const person = {
  name: "0xCrypt00o",
  age: 22
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);
```

## class, constructor , new 
- In ES5, an object can be created by defining a constructor function and using the `new` keyword to instantiate the object.

- In ES6, a `class` declaration has a `constructor` method that is invoked with the `new` keyword. If the constructor method is not explicitly defined, then it is implicitly defined with no arguments.

```javascript
// Explicit constructor
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
  takeOff() {
    console.log("To " + this.targetPlanet + "!");
  }
}

// Implicit constructor 
class Rocket {
  launch() {
    console.log("To the moon!");
  }
}

const zeus = new SpaceShuttle('Jupiter');
// prints To Jupiter! in console
zeus.takeOff();

const atlas = new Rocket();
// prints To the moon! in console
atlas.launch();
```

## getter , setter

- Getter functions are meant to simply return `get` the value of an object's private variable to the user without the user directly accessing the private variable.

- Setter functions are meant to modify `set` the value of an object's private variable based on the value passed into the setter function. This change could involve calculations, or even overwriting the previous value completely.

```javascript

class Book {

  this.#author="unknown";

  constructor(author) {
    this.#author = author;
  }

  // getter
  get writer() {
    return this.#author;
  }
  
  // setter
  set writer(updatedAuthor) {
    this.#author = updatedAuthor;
  }

}

const novel = new Book('anonymous');
console.log(novel.writer);
novel.writer = 'newAuthor';
console.log(novel.writer);
```
## Modules

- Modules are a way of organizing code into reusable units. 
- They can be imported into other modules, which allows you to use the code in the imported module without having to copy it.

### 1. Export  Modules

- To export a module, we use the `export` keyword.
- we can export a single value, such as a function.
- we can export an object containing multiple values.


```javascript
export const add = (x, y) => {
  return x + y;
}
```

```javascript
const add = (x, y) => {
  return x + y;
}

export { add };
```



```javascript
const add = (x, y) => {
  return x + y;
}

export { sum : add };
```

```javascript
const add = (x, y) => {
  return x + y;
}

const subtract = (x, y) => {
  return x + y;
}

export { add, subtract };
```


- `export default`  : statement is used to export a single value or object from a module as the default export.
- we can export default only one thing at the same file or module , can be function or object or any thing 
- This means that when you import a module, you can choose to import the default export without using curly braces `{}` around the name of the export.

```javascript 
export default add = (x,y)=>x+y
```


```javascript
const add = (x, y) => {
  return x + y;
}

const subtract = (x, y) => {
  return x + y;
}

export defualt add // we can export default one thing only
export { add , substract }
```


```javascript
const add = (x, y) => {
  return x + y;
}

const subtract = (x, y) => {
  return x + y;
}

export defualt { sum : add, sub: subtract }
```

- exporting from other modules 

```javascript 
export *  as Module from 'module.js' 
export {add,subtract} from 'moudle.js'
export {sum:add,sub:subtract} from 'moudle.js'
export Module from 'module.js'
```

### 2. importing Modules

1. Importing named exports: This is the most common way to import modules, You can import specific named exports from a module by using the import keyword and a comma-separated list of names in curly braces.

2. Importing the default export: If a module only has one export, you can import it using the import keyword and the name of the export.

3. Importing all exports: If you want to import all of the exports from a module, you can use the `import * as` syntax

```javascript
import {add,subtract} from 'moudle.js'
import Module from 'moudle.js'
import * as Module from 'moudle.js'
```
## Promises

- Before Promises were introduced in JavaScript, callback hell was a common pattern used to handle asynchronous operations. Here's an example of how to simulate callback hell to handle multiple asynchronous operations:
```javascript
getUser(userId, function(error, user) {
  if (error) {
    console.error('Error getting user:', error);
    return;
  }

  getPosts(user.id, function(error, posts) {
    if (error) {
      console.error('Error getting posts:', error);
      return;
    }

    getComments(posts[0].id, function(error, comments) {
      if (error) {
        console.error('Error getting comments:', error);
        return;
      }

      // Do something with the comments
      console.log('Comments:', comments);
    });
  });
});
```

-  promise is an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
- Promises were introduced in ECMAScript 6 (ES6) as a way to handle asynchronous operations in a more elegant and maintainable way than using callbacks.


- promise is in one of three states:
    - `pending` : the initial state, neither`fulfilled` nor `rejected`.
    - `fulfilled` : meaning that the operation completed successfully.
    - `rejected` : meaning that the operation failed
    - `settled` : final state , either `fulfilled` or `rejected`.

Here's an example of a simple promise that wraps a `setTimeout` function:


```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Hello World!");
  }, 5000);
});
```

- we create a new promise by passing a function to the `Promise` constructor. 
- This function takes two arguments, `resolve` and `reject`, which are functions that can be called to change the state of the promise.
- In this example, we call `resolve("Hello World!")` after `5` second, which changes the state of the promise to `fulfilled` and makes the resolved value `"Hello World!"` available to any code that is listening for the promise to be `settled`.

- To use the promise, we can attach a `.then()` method to it, which takes a single argument, a function that is called when the promise is `fulfilled`:

```javascript
promise.then((value) => {
  console.log(value);
});
```

In this example, the function passed to `.then()` will be called with the resolved value of the promise, which is `Hello World!`, and it will log the value to the console.

- We can also attach a `.catch()` method to the promise, which takes a single argument, a function that is called when the promise is `rejected`.

```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("Something went wrong!"));
  }, 1000);
});
promise.catch((error) => {
  console.log(error);
});
```

In this example, the function passed to `.catch()` will be called with the rejected value of the promise, which is an error object with the message `"Something went wrong!"`, and it will log the error to the console.

- Promise also provides a `.finally()` method which is called when the promise is `settled` regardless of whether the promise is `settled` either `fulfilled` or `rejected`.

```javascript
let somePromise = new Promise(
	  (resolve,reject) => setTimeout( ()=> reject('Timeout'), 5000 ) 
	  );

somePromise.then(
	  (value) => console.log(`Executed Successfully returned : ${value}`)
	  ).catch( 
	  (error) => console.log(`Error Occured : ${error}`)
	  ).finally(
			()=> console.log('Finished')
	  ) ; 
```

- Promise allows you to handle asynchronous operations in a more elegant and maintainable way than using callbacks. It also allows for a clear separation of concerns, making it easier to understand and change the code. It also helps in handling errors in a better way.



## Async / Await

- `async/await` is a way of writing asynchronous code that makes it look and behave more like synchronous code. It was introduced in ECMAScript 2017 (ES8) as a syntax sugar on top of promises.
- It allows you to write asynchronous code that looks similar to synchronous code, making it easier to read and understand.

- `async` is a keyword that is used to define an asynchronous function. 
- An asynchronous function is a function that returns a promise and can be await-ed.

```javascript
async function example() {
  // asynchronous code here
}
```

- `await` is a keyword that is used inside an asynchronous function to pause the execution of the function until a promise is `settled` (`fulfilled` or `rejected`).

```javascript
async function example() {
  let result = await promise;
  // the code execution will pause here until the promise is settled
  // after the promise is settled, the value of the promise will be assigned to the variable 'result'
  // the rest of the code will continue to execute
}
```

For example, consider a simple promise that wraps a `setTimeout` function:

```javascript
let promise = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Hello World!");
  }, 1000);
});
```
Here is an example of using async/await with the above promise:

```javascript
async function example() {
  let result = await promise;
  console.log(result); // logs "Hello World!" after 1 second
}

example();
```

In this example, the `await` keyword is used to pause the execution of the `example()` function until the promise is `settled`. Once the promise is `settled`, the resolved value `"Hello World!"` is assigned to the result variable, and the rest of the function continues to execute, logging the result to the console.

- In case of any error occured in the promise, we can use `try-catch` block to handle the error

```javascript
function returnPromise(){
	  return new Promise( (resolve,reject) => setTimeout( () => resolve("HelloWorld") , 5000) )
}

async function example() {
    try {
       let result = await returnPromise();
       console.log(result); 
    } catch (error) {
        console.log(error);
    }
}

example();

```


- `async/await` makes it easy to write asynchronous code that looks and behaves like synchronous code. It is a more readable and maintainable way of handling asynchronous operations compared to using callbacks or chaining promises.



## Iterators

- ES6 introduces a new way of traversing data structures called iteration.
- Iteration is based on two main concepts: iterable and iterator.


- ### Iterable

    - An iterable is an object that wants to make its elements accessible to the public.
    - It does so by implementing a method with a key of `Symbol.iterator`.
    - This method is a factory for creating iterators.

- ### Iterator

    - An iterator is a pointer for traversing the elements of an iterable. 
    - It keeps track of where the iterator currently is in the data structure and allows for the retrieval of the next element in the sequence.


- The following data structures are examples of iterables:

    - `Arrays`
    - `Strings`
    - `Maps`
    - `Sets`

- However, plain objects are not iterable by default.

- The idea behind iterability is to provide a standard way for data consumers (such as `for-of` loops and the spread operator `...`) to retrieve values from data sources (such as `arrays`, `maps`, and `strings`).

- ES6 introduces the Iterable interface to provide a standard way of creating consumers for various data sources.
    - To use an iterable, a consumer calls the `Symbol.iterator` method on the iterable object, which returns an iterator.
    - The consumer can then call the `next()` method on the iterator to retrieve the next value in the sequence.
    - repeat this untill next retrun `{ done: false }`

```javascript


 // Define Iterable Object

const obj = {
    name: '0xCrypt00o',
    age: 22,
    job: 'Software Engineer | Cybersecurity Researcher',
 
    [Symbol.iterator]() {
        const properties = Object.keys(this);
        let index = 0;
        return {
            next: () => {
			    if (index < properties.length) {
				    const value = this[properties[index]];
				    index++;
				    return { value, done: false };
			    } else {
				    return { done: true };
			    }
		    }
	    };
    }


}; 


// make iterator function non-enumerable when logding object

Object.defineProperty(obj, Symbol.iterator, { enumerable: false });

// now we can use for-of with object , because it worked with iterable objects only

for (let i of obj) {
console.log(i)
}

// and also we can use spread operator with iterables

let me = {...obj}
console.log(me)

```

-  The following ES6 language constructs make use of the Iterable:
    - Destructuring via an Array pattern
    - `for-of` loop
    - `Array.from()`
    - Spread operator `...`
    - `Constructors` of `Maps` and `Sets`
    - `Promise.all()` , `Promise.race()`
    - `yield*`

## Generators

- Generators are functions in JavaScript that allow you to define an iterative algorithm by writing a single function that can maintain its own state and is capable of producing a sequence of values.
- The key feature of generators is that they allow you to pause and resume the execution of a function, which gives you more control over the flow of execution.
- A generator function is defined using the `function*` syntax and contains one or more `yield` statements that can pause the execution of the function and return a value.
- When a generator function is called, it returns a generator object that can be used to control the execution of the function.
- Generators can be thought of as processes that can be paused and resumed while executing a particular piece of code. 
- This allows you to write code that can generate a sequence of values over time, rather than having to generate all the values at once and store them in memory.

```javascript

// implemntation for range which is in python & rust , and implement it as generator function

function* range(start = 0, stop = 0, step = 1) {
  if (step === 0) throw new Error('Step cannot be zero');
  
  if ( (step > 0 && start >= stop) || (step < 0 && start <= stop) ) return;
  
  let current = start;

  while ((step > 0 && current < stop) || (step < 0 && current > stop)) {
    yield current;
    current += step;
  }

}

for ( let i of range(0,5) ) console.log(i);


for ( let i of range(5,0,-1) ) console.log(i);


```

so Generator functions are a special type of function in JavaScript that allow you to define an iterative algorithm by writing a single function that can maintain its own state and is capable of producing a sequence of values. 

- Generator functions can be declared in several ways:

    1. Function declarations:

    ```javascript
    function* genFunc() {
        // ...
    }
    const genObj = genFunc();
    ```

    2. Function expressions:

    ```javascript
    const genFunc = function* () {
        // ...
    };
    const genObj = genFunc();
    ```

    3. Generator method definitions in object literals:

    ```javascript
    const obj = {
        *generatorMethod() {
        // ...
        }
    };
    const genObj = obj.generatorMethod();
    ```

    4. Generator method definitions in class definitions:

    ```javascript
    class MyClass {
        *generatorMethod() {
            // ...
        }
    }
    const myInstance = new MyClass();
    const genObj = myInstance.generatorMethod();
    ```


- Generators in JavaScript have many use cases, which include:

    - Simplifying asynchronous code: Generators can be used to execute simple asynchronous blocks of code, making it easier to write code that works with asynchronous operations without the complexity of traditional callbacks or promises.

    - Receiving asynchronous data using generators: The new async/await syntax in JavaScript is internally based on generators. This allows developers to write cleaner and more readable code when working with asynchronous operations.

    - Implementing Iterables: Generators can be used to define custom iterables in JavaScript, allowing developers to iterate over complex data structures or objects in a more natural and efficient way than with traditional iteration methods. For example, the `objectEntries()` function shown above uses a generator to create an iterable over the properties of an object.
```javascript 
function* objectEntries(obj) {
    const propKeys = Reflect.ownKeys(obj);

    for (const propKey of propKeys) {
        // `yield` returns a value and then pauses
        // the generator. Later, execution continues
        // where it was previously paused.
        yield [propKey, obj[propKey]];
    }
}
```

Overall, generators provide a powerful and flexible tool for working with complex data structures, asynchronous operations, and other advanced programming concepts in JavaScript. They allow for cleaner and more efficient code that is easier to read and maintain, which can be especially valuable in large or complex codebases.
