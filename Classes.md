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
  this.i=o; <br/>
  this.j=j; <br/>
};<br/>
x.prototype.getJ=function(){ <br/>
    return this.j; <br/>
}; <br/>
  
  
