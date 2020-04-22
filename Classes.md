## Prototype in Javascript
By default every function in JS has a prototype property which is empty object. <br/>
So if we add properties and methods to prototype then any other object that is constructed using this function will inherit the properties and methods of the prototype. <br/>
In languages like Java you create class and extend that class and create objects out of that. <br/>
But in Javascript though ES6 has class it is not like Java. JS has prototype based inheritance. <br/>
In Java you create class and then create objects out of it. But in JS you create Constructor function and using this constructor you can create objects from it. <br/>

Example: <br/>
function Car(options){ <br/>
  this.title = options.title; <br/>
} <br/>
Car.prototype.drive = function(){ <br/>
  return 'vroom'; <br/>
} <br/>
const car = new Car({title:'Focus'}); <br/>
car.drive(); <br/>

Not only this every function expression in JS is basically a constructor and you can create objects out of it. <br/>
Example: <br/>
var x = function(j){ <br/>
  this.i=0; <br/>
  this.j=j; <br/>
  this.getJ = function(){ <br/>
    return this.j; <br/>
  }; <br/>
}; <br/>

var x1 = new x(1); <br/>
var x2 = new x(2); <br/>

So both x1 and x2 are objects which inherite all properties and methods from x. <br/>
But every object would get its own copy of method getJ. <br/>
In order to avoid this we make use of prototype to add methods to an object. <br/>
var x = function(j){ <br/>
  this.i=0; <br/>
  this.j=j; <br/>
};<br/>
x.prototype.getJ=function(){ <br/>
    return this.j; <br/>
}; <br/>
 

var x1 = new x(1); <br/>
var x2 = new x(2); <br/>
x1.getJ(); <br/>
x2.getJ(); <br/>

So now if we try to invoke getJ function though x1 and x2 do not have those methods they will look up their parent which is prototype.
It finds it and then uses it from the parent. <br/>

Consider below constructor: <br/>
var x = function(){ <br/>
}; <br/>

Notice the heirarchy: <br/>
Object -> function -> x <br/>

You can view the heirarchy by typing: console.dir(x); <br/>

## Creating subClass (or subConstructor) using prototype inheritance in ES5
base class car:
function Car(options){ <br/>
  this.title = options.title; <br/>
} <br/>
Car.prototype.drive = function(){ <br/>
  return 'vroom'; <br/>
} <br/>
function Toyota(options){ <br/>
   this.color = options.color; <br/>
} <br/>
const toyota = new Toyota({color:'red',title:'Daily Driver'}); <br/>
console.log(toyota); <br/>
Output will be: {"color":"red"} <br/>
Now we want to inherit property title from base class. For this whenever we call Toyota constructor we want to call the base call as well as shown below: <br/>
function Toyota(options){ <br/>
   Car.call(this,options); <br/>
   this.color = options.color; <br/>
} <br/>
console.log(toyota); <br/>
Now if we create toyota object  <br/>
const toyota = new Toyota({color:'red',title:'Daily Driver'}); <br/>
console.log(toyota); <br/>
Output will be: {"title":"Daily Driver","color":"red"} <br/>

Now if we need to call the drive method of the Car prototype we need to do the following: <br/>

function Toyota(options){ <br/>
   Car.call(this,options); <br/>
   this.color = options.color; <br/>
} <br/>
Toyota.prototype = Object.create(Car.prototype); <br/>
Toyota.prototype.constructor = Toyota; <br/>
Toyota.prototype.honk=function(){ <br/>
  return 'beep'; <br/>
}; <br/>
 
const toyota = new Toyota({color:'red',title:'Daily Driver'}); <br/>
toyota.drive(); <br/>
toyota.honk(); <br/>

## Creating subClass (or subConstructor) using prototype inheritance in ES6
In ES6 all of the above can be achieved easily using class. <br/>
class Car{ <br/>
  constructor({title}){ <br/>
    this.title=title; <br/>
  } <br/>
  drive(){ <br/>
    return 'vroom'; <br/>
  } <br/>
} <br/>
const toyota = new Car({title:'Toyota'}); <br/>
console.log(toyota); //Output will be {title:'Toyota'} <br/>
toyota.drive(); // Output will be vroom <br/>

Now if we need to create Toyota object by extending Car: <br/>
class Toyota extends Car{ <br/>
   constructor({color}){ <br/>
    this.color = color; <br/>
  } <br/>
  honk(){ <br/>
    return 'beep'; <br/>
  } <br/>
} <br/>
 
const toyota = new Toyota({color:'red'}); <br/>
console.log(toyota); <br/>

We notice the following error: <br/>
 ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor <br/>
 
 In order to resolve this we will have to invoke the constructor of the base class Car in the constructor of the Toyota class: <br/>
 class Toyota extends Car{ <br/>
   constructor(options){ <br/>
     super(options); //Car.constructor() <br/>
     this.color = options.color; <br/>
  } <br/>
  honk(){ <br/>
    return 'beep'; <br/>
  } <br/>
} <br/>

const toyota = new Toyota({color:'red',title:'Daily Driver'}); <br/>
console.log(toyota); //Output will be  {"title":"Daily Driver","color":"red"} <br/>

## When to use classes
Lot of JS libraries like React and Angular make use of class to extend Components.


  
