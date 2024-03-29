
# OOP In JS

- Javascript doesn,t support native classes like other languages but classes are just constructor function in js like the following :  

## 1. Constructor  Function

1. By Useing Constructor Function 

```javascript

function Base(attr1 = undefined, attr2 = undefined, attr3Value = undefined) {
	
	let attr3 = attr3Value  // private 

	this.attr1 = attr1
    this.attr2 = attr2
	
    this.setAttr3 = function(updateAttr3) {
		attr3 = updateAttr3
	}

	this.getAttr3 = function() {
		return attr3
	}
	
	this.info = function() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}

    /*
    * assgin prototype of Base for new instance or object created by this constructor 
    * we can use __proto__  : obj.__proto__ = Constructor.prototype;
    * this.__proto__ = Base.prototype ;
    * but it isn,t standard between all js runtimes so we will use 
    * Object.setPrototypeOf(obj,Constructor.prototype)
    */

    Object.setPrototypeOf(this,Base.prototype)

}

```

2. with ES6 `class` Keyword Syntax Sugar 

```javascript

class Base {
    
	attr1;
	attr2;
	#attr3;

	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}

	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}

}
```


- Getting an Instance from a Constructor

1. to generate a new instance object from constructor function with `new` keyword

```javascript
let obj = new Base("attr1","attr2","attr3")
```

2. another ways  for Getting an Instance from a Constructor

1. `Constructor.call` 
```javascript
let obj ={}
Base.call(obj,"attr1","attr2","attr3")
```

2. `Object.create(Constructor.prototype)`

```javascript
let obj =  Object.create(Base.prototype)
```


3. Useing Custom `new` function

- implement how `new` work in js exactly
 
```javascript
function new_obj(constructor,...args){
    let obj = {}
    constructor.call(obj,...args)
    obj.__proto__= constructor.prototype
    return obj
}
```

```javascript
function new_obj(constructor,...args){
    let obj = {}
    constructor.call(obj,...args)
    Object.setPrototypeOf(obj,constructor.prototype)
    return obj
}
```

---

## 2. Inheritance 

- Inheritance in object-oriented programming (OOP) is a mechanism that allows a child class to inherit properties and methods from a parent class. This allows for code reuse and a clear organization of related classes.

<br>

1. useing `call` method


```javascript
function Base(attr1 = undefined, attr2 = undefined, attr3Value = undefined) {

	let attr3 = attr3Value  // private 

	this.attr1 = attr1
	this.attr2 = attr2

	this.setAttr3 = function(updateAttr3) {
		attr3 = updateAttr3
	}

	this.getAttr3 = function() {
		return attr3
	}

	this.info = function() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}
}

function Derived(attr1 = undefined, attr2 = undefined, attr3 = undefined, attr4 = undefined) {
	
    Base.call(this, attr1, attr2, attr3)
	this.attr4 = attr4


	this.info = function() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2} , attr4 : ${this.attr4}`)
	}
}
```




2. useing keyword `extends` extends methods , attributes from parent , keyword `super` call the parent constructor

```javascript
class Base {

	attr1;
	attr2;
	#attr3;

	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}

	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}

}

class Derived extends Base {

	attr4

	constructor(attr1, attr2, attr3, attr4) {
		super(attr1, attr2, attr3)
		this.attr4 = attr4
	}

	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2} , attr4 : ${this.attr4}`)
	}
}
```

---

## 3. Encapsulation

- Encapsulation in object-oriented programming (OOP) is a mechanism that allows for the hiding of an object's internal state and methods from the outside world. This promotes data hiding and abstraction, making the code more secure and easier to maintain.

<br>

1. getter and setter 

```javascript

function Base(attr1 = undefined, attr2 = undefined, attr3Value = undefined) {

	let attr3 = attr3Value  // private 

	this.attr1 = attr1
	this.attr2 = attr2

	this.setAttr3 = function(updateAttr3) {
		attr3 = updateAttr3
	}

	this.getAttr3 = function() {
		return attr3
	}

	this.info = function() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}
}


```

2. getter and setter  useing  `get` and `set` es6 keywords , declareing  private attributes useing es6 : `#` 

```javascript

class Base {
    
	attr1;
	attr2;
	#attr3;

	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}

	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}

}
```
---


## 4. Polymorphism

- Polymorphism in object-oriented programming (OOP) is a mechanism that allows objects of different classes to be treated as objects of a common class. This promotes code reusability, modularity, and maintainability.

<br>

1. Overrideing : 
	  
	  1. Method overriding is a run-time polymorphism.
	  2. It is performed in two classes with inheritance relationships.
	  3. In method overriding, methods must have the same name and same signature.


```javascript
class Base {

	attr1;
	attr2;
	#attr3;

	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}

	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2}`)
	}

}

class Derived extends Base {

	attr4

	constructor(attr1, attr2, attr3, attr4) {
		super(attr1, attr2, attr3)
		this.attr4 = attr4
	}

    // @Override info()
	info() {
		console.log(`attr1:${this.attr1} , attr2 : ${this.attr2} , attr4 : ${this.attr4}`)
	}
}

```

2. Overloading :
	  
	  1. Method Overloading is a compile-time Polymorphism.
	  2. It occurs within the class.
	  3. In method Overloading, methods must have the same name and different signatures.

```javascript
 
class Base {

	attr1;
	attr2;
	#attr3;

	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}

	// @ Overload info() 
	
	info(attr1, attr2) {
		if (typeof attr1 == 'string') {
			if (typeof attr2 == 'number') {
				console.log(`attr1 : ${attr1} and attr2 : ${attr2}`)
			}
			else {
				console.log(console.log(`attr1 : ${attr1} and attr2 :  ${this.attr2}`))
			}
		}
		else {
			console.log(`attr1 : ${this.attr1} and attr2 : ${this.attr2} `)
		}
	}

}
```

- another elegant way for Overloading 

```javascript	 
class Base {

	attr1;
	attr2;
	#attr3;

	#info = [

		function() {
			console.log(`attr1 :  ${this.attr1} and attr2 : ${this.attr2} `)
		},

		function(attr1) {
			console.log(`attr1 :  ${attr1} and attr2 : ${this.attr2} `)
		},

		function(attr1, attr2) {
			console.log(`attr1 :  ${attr1} and attr2 :  ${attr2} `)
		},

		function(attr1, attr2, attr3) {
			console.log(`attr1 :  ${attr1} and attr2 : ${attr2} , ${attr3} `)
		}
	]
	constructor(attr1, attr2, attr3) {
		this.attr1 = attr1
		this.attr2 = attr2
		this.#attr3 = attr3
	}

	set setAttr3(attr3) {
		this.#attr3 = attr3
	}

	get getAttr3() {
		return this.#attr3
	}



	// @Overload info()

	info(...args) {
		if (args.length <= this.#info.length) {
			this.#info[args.length](...args)
		}

	}
}
```



---

## 5. Abstraction

- Abstraction in object-oriented programming (OOP) is a mechanism that allows for the hiding of an object's complexity from the outside world, exposing only the essential features. This promotes code reusability, modularity, and maintainability.

<br>

- Abstraction Implementation Useing Es6 Syntax

```javascript

// define AbstractError 

class AbstractError extends Error {
	constructor(message) {
		super(message)
		this.name = AbstractError.name
	}
}

// Abstract Class

class Base {

	constructor() {
		if (this.constructor === Base) {
			throw new AbstractError("Can,t Create Object from Abstract class")
		}
	}

	info() {
		throw new AbstractError("It,s an Abstract Method You Need to Implement it ")
	}
}

// Extending Abstract Class

class Derived extends Base {

	constructor(attr1) {
		super()
		this.attr1 = attr1
	}

	// @Override info()

	info() {
		console.log(`attr1 : ${this.attr1}`)
	}

}


```

- Abstraction Implementation

```javascript



// define Abstract Error Constructor

function AbstractError(message) {
	Error.call(this, message);
	this.name = 'AbstractError';
	this.message = message;
}

AbstractError.prototype = Object.create(Error.prototype);
AbstractError.prototype.constructor = AbstractError;


function Base() {
	if (this.constructor == Base) {
		throw new AbstractError("Can,t Create Object from Abstract class")
	}
	this.info = function() {
		throw new AbstractError("It,s an Abstract Method You Need to Implement it ")
	}

}


// Extending Abstract Constructor

function Derived(attr1) {

	Base.call(this)

	this.attr1 = attr1

	// @Override info()

	this.info = function() {
		console.log(`attr1 : ${this.attr1}`)
	}

}


```

---

## 6. Static Attributes 

-  `static` attribute is a variable that is associated with a `class`, rather than with an instance of a class. 
- This means that there is only one copy of the static attribute, regardless of how many instances of the class are created  .


- we can declare static attributes and methods in javascript useing ES6 `static` keyword


```javascript
class Base{
   
    static staticMethod(){
        console.log("iam a static method")
    }
    
    static staticValue=0
    
    increaseStaticValue(){
       return ++this.constructor.staticValue
    }
    
    getStaticValue(){
        return this.constructor.staticValue 
    }
}
```


- another way to declare static attributes 

```javascript

function Base(){
 
    Base.staticMethod=function(){
         console.log("iam a static method")
    }

   Base.staticValue = 0
    
    this.increaseStaticValue=function(){
        return ++Base.staticValue
    }
    
    this.getStaticValue=function(){
        return Base.staticValue 
    }
    
}


```

---

## 7. MixIn

 - Mixins can be considered a form of object-oriented programming (OOP), as they provide a way to reuse code and implement features in a modular and composable manner. However, they do not provide inheritance in the traditional sense, as mixins do not create a hierarchy of objects like class-based inheritance. Instead, mixins are a way of combining properties and methods from different objects into a single object, offering a different way of reusing and composing code.

- example of  Mixin Pattern Implementation : 

```javascript

	  function infoMixin(someObj){
			someObj.info=()=>{
				  console.log(`${someObj.name} , ${someObj.age } years Old`)
			}
	  }

	  let me = {name:"eslam",age:21,description:"Software Engineer (Backend - Developer) and CyberSecurity Researcher ( Red - Teamer)"}
	  let myBrother={name:"ahmed",age:19, description :"Software Engineer - Web Developer "}
	  let myPit={name:"jack",age:3}
	  
	  infoMixin(me)
	  infoMixin(myBrother)
	  infoMixin(myPit)

	  me.info()
```
---

## 8. Prototype

- `prototype` is property of Constructor Used to Define shareable Object or Refference between all Created Objected and the Constructor it self to avoid duplicaiton of code and also duplicaiton in data in memory 

for example : 

```javascript

	  function Person(name,age){
			this.name=name
			this.age=age
			this.ownABrain=true
	  }

```

so every human instance will have it,s copy of this properties name,age,OwnABrains but every human may have different names and ages but all of them have a brain so if we have a million instances of Person every one will have his own copy of name,age,ownABrain but we can use a shareable or Refference object contain have a brain value between all of them example : 

```javascript

function Person(name,age){
	  this.name=name
	  this.age=age
}

Person.prototype.ownABrain=true 

```

to explain this we in more details let,s see this example : 

```javascript

function Person(name,age){
	  this.name=name
	  this.age=age
	  this.__shareableRef=Person.shareableRef
}

Person.shareableRef={ownABrain:true}

```

now let,s create a 2  instances from Person :

```javascript


let eslam = new Person("eslam",21) // eslam = {name:"eslam",age:21,	__shareableRef:{ownABrain:true}	}
let mohamed = new Person("mohamed",40) //mohamed = {name:"mohamed",age:40,	__shareableRef:{ownABrain:true}	}


mohamed.__shareableRef.ownABrain=false 

// now eslam = {name:"eslam",age:21,	__shareableRef:{ownABrain:false}	} , mohamed = {name:"mohamed",age:40,	__shareableRef:{ownABrain:false} } , Person.shareableRef={ownABrain:false}

let crypto = new Person("crypto",21)  // crypto = {name:"crypto",age:21,	__shareableRef:{ownABrain:false}	}

```

- so this is a simmilar Implementation for Prototype which is shareable Refference between Constructor and all Objects

- to implement this with `prototype` of constructor which is Refferenced by ` __proto__` which is called prototype chain on the new instance  , consider the following example : 

Define the Constructor with Prototype : 

```javascript

function Person(name,age){
	  this.name=name
	  this.age=age
}

Person.prototype={ownABrain:true}

```

let,s Create Instances Objects from This Constructor : 

```javascript

let eslam = new Person("eslam",21) 
let mohamed = new Person("mohamed",40)

console.log(eslam.ownABrain) // true 
console.log(mohamed.ownABrain) //true

eslam.__proto__.ownABrain=false

console.log(mohamed.ownABrain) // false
console.log(eslam.ownABrain) // false

Person.prototype.ownABrain=true

console.log(mohamed.ownABrain) // true 
console.log(eslam.ownABrain) // true 

```


 so if we create 10000000 instance from Person every instance will have it,s own copy from name,age but will share the same ownABrain value as Refference between Constructor and all instances from this Constructor , and it save more memory and code  


- `instanceof` is an oberator used to check if an instance is instance from spefic parent constructor or not 


- `instanceof` work by compareing the `instance.__proto__` with `constructor.prototype` it check if `__proto__` of instance is refer to `prototype` of constructor  like :

```javascript

instance.__proto__ === Constructor.prototype
```
and will loop over subtypes or instances `__proto__` and compare and when it find it refer to `Constructor.prototype` it will return `true` and if didn,t found over all subtypes it will return `false`

- and that,s How It Internally Really Work : 

```javascript

function instanceOf(obj, constructor) {
  let proto = obj.__proto__;
  while (proto) {
    if (proto === constructor.prototype) {
      return true;
    }
    proto = proto.__proto__;
  }
  return false;
}
```

- It's important to note that the `__proto__` property is a non-standard property, and it's not recommended to use it in production code, as it's not part of the official JavaScript specification and may not be supported in all environments. Instead, it's recommended to use the standard `Object.getPrototypeOf` method to access an object's prototype or use `constructor.prototype`.


- Production Implementation that work in node or deno or browser  

```javascript
function instanceOf(obj, constructor) {
  let proto =Object.getPrototypeOf(obj);
    if (proto === constructor.prototype) {
      return true;
    }
  while (proto!=Object.prototype){ 
    if (proto === constructor.prototype) {
      return true;
    }
    proto = Object.getPrototypeOf(obj);
  }
  return false;
}

```

```javascript
function instanceOf(obj, constructor) {
    return constructor.prototype.isPrototypeOf(obj)
}
```

<br> 

```javascript

	  let me = new Person("eslam",21)
	  if(me instanceof Person){
			console.log("me is instance of Person")
	  }
	  else{
			console.log("me is not instance of Person")
	  }
```

<br> 

- `constructor` is property of any instance and it Refference to The Constructor which is instance created from 

```javascript

	  let me = new Person("eslam",21)
	  let crypto= new me.constructor("crypto",21)

	  function Animal(name){
			this.name=name
	  }

	  if (crypto.constructor===Animal){
			console.log("crypto is instance of Animal")
	  }

	  if (crypto.constructor===Person){
			console.log("crypto is instance of Person")
	  }
```

- if we add properties to prototype like `Person.prototype.ownABrain=true`  without assigning it to new Object `instance.constructor` will still refer to parent Constructor Method `Person.prototype.constructor` which is `Person`  but if we change the `prototype` object to new Refference like : `Person.prototype={ownABrain:true}` the `instance.constructor` will be erased and not refer to the `Person` and will refer to  `Object` constructor Method , to fix this we need to do this : `Person.prototype={ownABrain:true,constructor:Person}`


example : 


```javascript

	  function Person(name,age){
			this.name=name
			this.age=age
	  }
	  

	  Person.prototype.ownABrain=true // this will not erase Person.prototype.constructor

	  let me = new Person("eslam",21)

	  console.log(me.constructor === Person) //  true 
	  console.log(me instanceof Person) // true


	  Person.prototype={ownABrain:true} // this will erase Person.prototype.constructor

	  let crypto = new Person("crypto",21)
	  
	  console.log(crypto.constructor === Person)  // false , because constructor value which is Person had been erased and now it will equal the default value : Object 

	  console.log(crypto instanceof Person ) // true , because __proto__ of crypto will still refer to prototype of Person

	  Person.prototype={constructor:Person,ownABrain:true}
	  
	  console.log(crypto.constructor === Person)  // false
	  console.log(crypto instanceof Person ) // false because prototype assigned to new Refference { constructor:Person,ownABrain:true } so __proto__ is Refference to the old prototype 

	  let eslam = new Person("eslam",21)
	  
	  console.log(eslam.constructor === Person)  // true
	  console.log(eslam instanceof Person) // true

	  


```


- `isPrototypeOf` method is a property of the `Object.prototype`, so it's available on all objects in JavaScript , it takes one argument, which is the object being tested to check if the `prototype` property of the object on which isPrototypeOf is called is in the prototype chain of the object being tested and , If the prototype property is found in the prototype chain of the object being tested, isPrototypeOf returns true else it return false 


example : 

```javascript

function Person(name,age){
	  this.name=name
	  this.age=age
}

Person.prototype={constructor:Person,ownABrain:true}

let me = new Person("eslam",21)

console.log(	Person.prototype.isPrototypeOf(me) ) // true
console.log(	Person.prototype.isPrototypeOf({name:"crypto",age:21})	) //false

```


- every object in js have a prototype chain property `__proto__` which is Refference to it,s parent and  prototype chains `__proto__` of  all objects and even constructors is Refference to `prototype` of `Object` 


- It's important to note that the `__proto__` property is a non-standard property, and it's not recommended to use it in production code, as it's not part of the official JavaScript specification and may not be supported in all environments. Instead, it's recommended to use the standard `Object.getPrototypeOf` method to access an object's prototype or use `constructor.prototype`.

- `constructor.prototype` property and the `__proto__` property are similar in that they both refer to the `prototype` object of a `constructor`. However, the `constructor.prototype` property is <ins> the standard way </ins> to access the prototype of a constructor function, while __proto__ is a non-standard feature that has been deprecated in some JavaScript engines and may not work in all browsers and JS RunTimeEnvironments for example : `deno` 

- in this Docs i use `__proto__` to provide the Concept , in production you should use `constructor.prototype` or `Object.getPrototypeOf()` instead  !

```javascript

function Person(name,age){
	  this.name=name
	  this.age=age
}


Person.prototype={constructor:Person,ownABrain:true}

let me = new Person("eslam",21)

console.log(	Person.prototype.isPrototypeOf(me) ) // true

console.log(	Object.prototype.isPrototypeOf(me)  ) //true

console.log(	Object.prototype.isPrototypeOf(Person)  ) //true

console.log(	Object.prototype.isPrototypeOf({})  ) //true


console.log(	Object.prototype.isPrototypeOf({"name":"eslam"})  ) //true

// if we add a property to prototype of Object it will affect all instances

Object.prototype.owner="Crypt00o"

console.log({}.owner) // Crypt00o

console.log({}) // {} 


console.log(me.owner) // Crypt00o

delete Object.prototype.owner

console.log(me.owner) // undefined

{}.__proto__.owner="eslam"

console.log(me.owner) // eslam

me.__proto__.owner="Crypt00o"

console.log(me.owner) // Crypt00o  

console.log({}.owner) // eslam , because me.__proto__.owner Override  it,s own copy of owner not for Object.prototype

{}.__proto__.owner="none"

console.log( me.owner ) // Crypt00o


console.log( {}.owner ) // none

console.log(Person.owner) // none

console.log(Person.prototype.owner) // Crypt00o
```

- `hasOwnProperty` is a method defined on `Object.prototype` so all objects will has this property as Refference

we can Override it on `Object.prototype` so it,s behaviour  will change for all objects for example : 

```javascript

Object.prototype.hasOwnProperty=function hasOwnProperty(property){
	  console.log(`[+] Checking if contains key : ${property} or not `)
	 return (property in this ? true : false)
}
```

now any new Object will have our defined `hasOwnProperty` method

```javascript

	  function Person(name,age){
			this.name=name
			this.age=age
	  }

	  let me = new Person(name="eslam",age=21)
	  console.log(me.hasOwnProperty("name")) // return true
	  console.log(me.hasOwnProperty("none")) // return false
	  console.log({msg:"hello"}.hasOwnProperty("msg")) // true
```
### The Concept of prototype chain

- The `hasOwnProperty` method is defined in `Object.prototype`, which can be accessed by `Person.prototype`, which can then be accessed by `me`. This is an example of the prototype chain. In this prototype chain, `Person` is the supertype for `me`, while me is the subtype. `Object` is a supertype for both `Person` and `me`. `Object` is a supertype for all objects in JavaScript. Therefore, any object can use the `hasOwnProperty` method.


 - So We Can Use This Concept To Achieve Inheritance Useing Prototype 

- ` Object.create(<prototype>, <properties>)` used to create an Object with given prototype . 
- the `Object.create()` method works by creating a new object with a specified `prototype`. The `Object.create()` method internally creates an object with a specified `prototype` by using the following steps:

	  1. it creates a new object.

	  2. it sets the `__proto__` property of the newly created object to the `prototype` object passed as an argument to `Object.create()`.

	  3. The newly created object is returned as the result of `Object.create()`.

- Here's an example to show how Object.create() works internally:

```javascript

function createObject(proto) {
  let obj = {};
  obj.__proto__ = proto;
  return obj;
}
```



example of useing `Object.create()`

```javascript

let crypto = Object.create(Object.prototype , {
			name:{
				  value:"Crypt00o",
				  enumerable:true,
				  writeable:true,
				  configrable:true
			} ,
			age:{
				  value:21,
				  writeable:true,
				  configrable:true,
				  enumerable:true
			}
	  } );

function Person(name,age){
	  this.name=name
	  this.age=age
}

Person.prototype.info=function(){
	  console.log(`name : ${this.name} , age:${this.age} `)
}

let me = Object.create(	Person.prototype, {
			name:{
				  value:"eslam",
				  enumerable:true,
				  writeable:true,
				  configrable:true
			} ,
			age:{
				  value:21,
				  writeable:true,
				  configrable:true,
				  enumerable:true
			}
	  } );

me.info()

```


- let,s Implement inheritance useing `prototype` 


```javascript

	  function Person(name,age){
			this.name=name
			this.age=age
	  }
	  
	  Person.prototype.info=function(){
			console.log(`name : ${this.name} , age : ${this.age}`)
	  }

	  class Developer extends Person{
			#salary
			constructor(name,age,salary){
				  super(name,age)
				  this.#salary=salary
			}

			get getSalary(){
				  return this.#salary
			}
	  }

	  function SecurityEngineer(name,age,field){
			Person.call(this,name,age)
			let team = field
			

			this.getTeam=function(){
				  return team
			}

			this.isRedTeamer=function(){
				  return team==="red"
			}
			
			this.isBlueTeamer=function(){
				  return team==="blue"
			}
	  }

	 
// Setting the Child's Prototype to an Instance of the Parent

SecurityEngineer.prototype = Object.create(Person.prototype)

console.log((new SecurityEngineer("eslam",21,"red") ).constructor === Person)  // true , because it will create an Refference to Person.prototype which it,s constructor = Person
```
- so let,s make `SecurityEngineer.prototype` as Refference to `Person.prototype` , but change `constructor` value which will be `Person` to `SecurityEngineer`

```javascript

SecurityEngineer.prototype = Object.create(Person.prototype,{
	  constructor:{
			value:SecurityEngineer,
			enumerable:true,
			writeable:false,
			configrable:false
	  }
});
```



```javascript

let me = new Developer("eslam",21,salary="sorry , it,s personal things ")

console.log(me instanceof Developer) // true , that,s because me.__proto__==Developer.prototype
console.log(me instanceof Person) // true , that,s because me.__proto__.__proto__==Person.prototype
console.log(me instanceof Object) // true ,  that,s because me.__proto__.__proto__.__proto__==Object.prototype , that,s is the  Hierarchical Inheritance and JS Achieve it through  prototypes
```

let,s create instance from `SecurityEngineer` Constructor

```javascript

let meAlso= new SecurityEngineer("eslam",21,"red")

me.info()
meAlso.info()
```

 let,s Override `info()` inherited method  on `SecurityEngineer` Only

```javascript

// @Override info()
SecurityEngineer.prototype.info=function(){
	  console.log("Deperacated Use describe() Method Instead")
}

// define describe method for SecurityEngineer which can be accessed by SecurityEngineer instances only or by any subtype " ChiledObject or Constructor " that apply or have the same prototype of SecurityEngineer

SecurityEngineer.prototype.describe=function(){
			console.log(` ${this.name} , ${this.age} years , CyberSecurity Engineer - ${String(this.getTeam()).toUpperCase()} Team`)
}
```

- now any instance of `SecurityEngineer` will be have these `info` methods:

	  1. `instance.__proto__.info()` which Refference to => `SecurityEngineer.prototype.info()`
	  2. `instance.__proto__.__proto__.info()` which Refference to => `Person.prototype.info()`

```javascript

meAlso.info() // will print : 'Deperacated Use describe() Method Instead'
meAlso.__proto__.info() // will print : 'name : eslam , age : 21'

me.info() // will print : 'name : eslam , age : 21'


```

- in above example we not Override `info()` method directly , to explain that  really let,s explain how we access method `info()` on instances Objects

```javascript

function accessPrototypeProp(object,prop){
	  while(object && object==null){
			if(object.__proto__[prop]){
				  return object.__proto__[prop]
			}
			object=object.__proto__
	  }
}
```

so when we call `me.info()` this is what is js engine do under the hood :  search on `me.__proto__` or equilevent about method `info` and it not found so search again on `me.__proto__.__proto__` or equilevent for method `info` untill we find it in all prototypes of parents or untill we reach `null` Object mean the root of  parents tree , so calling `me.info()`  will `call me.__proto__.__proto__.info()` which is Refference to `Person.prototype.info()`

in `meAlso.info()`  this is what is js engine do under the hood :  search on `meAlso.__proto__` or  equilevent about method `info` and it found so it,s returned `meAlso.__proto__.info()`  and call it , which Refference to `SecurityEngineer.prototype.info`

- As We See  `constructor` function  inherits its prototype object from a supertype `constructor` function can still have its own methods in addition to inherited methods.

### Additional Notes : 

- In JavaScript, almost everything is an object. JavaScript has six primitive data types: number, string, boolean, null, undefined, and symbol. These primitive data types are not objects and have different characteristics compared to objects.

- However, even the primitive data types can be treated as objects when necessary. For example, a string can be treated as an object using the built-in String object, which provides methods for manipulating strings.

- On the other hand, objects in JavaScript are used to represent complex data structures, such as arrays, functions, and key-value pairs. JavaScript objects are dynamic and can be easily modified, making them a versatile and powerful tool for storing and manipulating data.

- So, while not everything in JavaScript is an object, objects play a central role in the language and are used for a wide range of tasks.

- In JavaScript, primitive values such as numbers, strings, and booleans are not objects, but they can be temporarily converted to objects when necessary, such as when they need to be used as objects, such as when a property or method is called on them. This temporary conversion is known as "boxing".

 - For example, when you write `(1).toFixed(2)`, the number `1` is temporarily boxed into a `Number` object, which provides the `toFixed` method. The `Number` object is then used to call the `toFixed` method, which returns a string representation of the number with a specified number of decimal places.

- This temporary conversion to an object wrapper is done automatically by JavaScript, and it's not something that you need to worry about as a programmer. It's just an implementation detail of the language.

- So, when you write `(1).__proto__`, you're temporarily converting the number `1` to a `Number` object, and then accessing its `__proto__` property. The `__proto__` property refers to the `prototype` of an object, which is another object that it inherits properties and methods from.


 - it's also worth mentioning that when a primitive value is boxed into an object wrapper, it's not actually converted to an object. It's still a primitive value. The object wrapper simply provides a way to access object methods and properties for the primitive value.

 For example, after you call the `toFixed` method on the number `1`, the `Number` object is discarded and the primitive value `1` remains unchanged. This is why primitive values in JavaScript are efficient and fast, as they don't carry the overhead of full-fledged objects.

`(1).__proto__.__proto__`

In this case, the `Number` object inherits from the `Object` object, so its `__proto__` property points to `Object.prototype`. And `Object.prototype` is the base prototype for all objects in JavaScript, so `(1).__proto__.__proto__` is equal to `Object.prototype`.

-  in JavaScript, functions are objects. Functions in JavaScript have properties and methods, just like any other object, and they can be assigned to variables, passed as arguments to other functions, or added to objects as properties

- Functions in JavaScript are callable objects, which means they can be invoked by using parentheses `()` after the function name. Normal objects, on the other hand, are not callable, but they can have properties and methods associated with them.

---








