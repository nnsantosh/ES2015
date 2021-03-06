
## const and let

const is a keyword that is used to declare a variable whose values we never expect to change. <br/>
let is a keyword that is used to declare variables whose values we expect to change over time. <br/>

## Template Strings or Template Literals

Whenver we used to concatenate variables to string we used to do in the following way: <br/>

function getMessage(){ <br/>
  const year = new Date().getFullYear(); <br/>
  return "the year is "+year; <br/>
} <br/>
getMessage(); <br/>
The output will be: the year is 2020 <br/>

Same thing can be written as: <br/>

function getMessage(){ <br/> 
  const year = new Date().getFullYear(); <br/>
  return `the year is ${year}`; <br/>
} <br/>
In fact we can put any valid javascript expression inside the curly braces along with $ symbol. <br/>
function getMessage(){ <br/>
 return `the year is ${new Date().getFullYear()}`; <br/>
} <br/>

Lets take another example: <br/>
const device_id= 4; <br/>
const guid = 20; <br/>
const username = 'Santosh'; <br/>
const data = '{"device_id":"'+ device_id +'","guid":"'+ guid +'","username":"'+ username +'"}' <br/>
console.log(data) <br/>
The output will be: {"device_id":"4","guid":"20","username":"Santosh"} <br/>

Now the same thing can be done using template strings as shown below: <br/>
const data = `{"device_id":${device_id},"guid":${guid},"username":${username}}`; <br/>

## Arrow functions
Let us say we have function to add two numbers and return the sum: <br/>
const add = function(a,b){ <br/>
  return a + b; <br/>
} <br/>
We can write this using fat arrow function as: <br/>
const add = (a,b) => { <br/>
  return a + b; <br/>
} <br/>

If the body of the javascript function has just one single expression then we can write as: <br/>
const add = (a,b) => a + b; <br/>
We gain implicit return in this case. Only if curly braces are not used then we get this implicit return. <br/>

If the function has single parameter then the paranthesis for parameters is also not required. <br/>
Example: <br/>
const double = function(num){ <br/>
  return num * 2; <br/>
} <br/>
We can write this using fat arrow function as: <br/>
const double = num => num * 2; <br/>

In case function does not have any parameters then in that case also paranthesis has to be maintained for the parameters. <br/>

We can also surround the arrow function with parantheis as below: <br/>
const double = (num => num * 2) <br/>

Fat Arrow functions solve one major problem. <br/>

Consider below function: <br/>
const team = { <br/>
  members: ['Jane','Bill'], <br/>
  teamName: 'Super Squad', <br/>
  teamSummary: function(){ <br/>
    return this.members.map(function(member){ <br/>
      return `${member} is on team ${this.teamName}` <br/>
    }); <br/>
  } <br/>
} <br/>
Now when we invoke teamSummary() function: <br/>
team.teamSummary(); <br/>

We get following error: TypeError: Cannot read property 'teamName' of undefined <br/>

Now if we replace the function with arrow function as shown below: <br/>
const team = { <br/>
  members: ['Jane','Bill'], <br/>
  teamName: 'Super Squad', <br/>
  teamSummary: function(){ <br/>
    return this.members.map((member) => { <br/>
      return `${member} is on team ${this.teamName}` <br/>
    }); <br/>
  } <br/>
} <br/>
And if we invoke team.teamSummary() we get the following output correctly:  <br/>
["Jane is on team Super Squad","Bill is on team Super Squad"] <br/>

Fat arrow functions make "this" behave as we expect it to by binding it to current lexical scope. <br/>

## Enhanced Object Literals

Lets make a function that creates bookshop object: <br/>
function createBookShop(inventory){ <br/>
  	return { <br/>
      inventory: inventory, <br/>
      inventoryValue: function(){ <br/>
        return this.inventory.reduce((total,book) => total + book.price,0); <br/>
      }, <br/>
      priceForTitle: function(title){ <br/>
        return this.inventory.find(book => book.title === title).price; <br/>
      }	 <br/>
    }; <br/>
} <br/>

const inventory = [ <br/>
   {title:'Harry Potter',price:10}, <br/>
   {title:'Eloquent JavaScript',price:15} <br/>
 ] <br/>
 
 Now lets invoke the function <br/>

const bookShop = createBookShop(inventory); <br/>
bookShop.inventory <br/>
bookShop.inventoryValue() <br/>
bookShop.priceForTitle('Eloquent JavaScript') <br/>

Output will be: <br/>
[{"title":"Harry Potter","price":10},{"title":"Eloquent JavaScript","price":15}] <br/>
25 <br/>
15 <br/>

Now with ES6 enhanced object literals we can do certain things to make the object compact: <br/> 
1. Whenever object has key value pair with same name you can omit the colon and use only the key name <br/>
2. Whenever object has key value pair with value being function you can omit the colon and the keyword function <br/>

With the above rules the createBookShop function can be written as: <br/>
function createBookShop(inventory){ <br/>
  	return { <br/>
      inventory, <br/>
      inventoryValue(){ <br/>
        return this.inventory.reduce((total,book) => total + book.price,0); <br/>
      }, <br/>
      priceForTitle(title){ <br/>
        return this.inventory.find(book => book.title === title).price; <br/>
      }	 <br/>
    }; <br/>
}  <br/>

## Default Function Arguments
Let us say we have function with two parameters: <br/>
function makeAjaxRequest(url,method){ <br/>
  	//logic to make request <br/>
} <br/>
Now if we call this function without passing second parameter then the second parameter value will be undefined. <br/>
makeAjaxRequest('google.com'); <br/>

This can be handled by giving default value to the parameter inside the function as shown below: <br/>
function makeAjaxRequest(url,method){ <br/>
  if(!method){ <br/>
    method = 'GET'; <br/>
  } <br/>
  	//logic to make request <br/>
} <br/>

But instead of having this logic inside function we can make use of default value for function arguments as shown below: <br/>
function makeAjaxRequest(url,method='GET'){  <br/>
  //logic to make request <br/>
} <br/>

If we pass null while invoking the function for parameter having default value then the default value does not apply: <br/>
makeAjaxRequest('google.com',null); <br/>

Consider below use case where you are providing a function to create admin user: <br/>

function User(id){ <br/>
  this.id = id; <br/>
} <br/>

function generateId(){ <br/>
  	return Math.random() * 9999; <br/>
} <br/>

function createAdminUser(user){ <br/>
  	user.admin=true; <br/>
  	return user; <br/>
} <br/>

const usr = createAdminUser(new User(generateId())); <br/>
console.log(usr) <br/>

In the above function the users of createAdminUser function have to provide the user. But you can assign default value to user parameter in which case the users need not pass the user object as shown below: <br/>

function createAdminUser(user=new User(generateId())){ <br/>
  	user.admin=true;  <br/>
  	return user; <br/>
} <br/>

const usr = createAdminUser(); <br/>
console.log(usr) <br/>
Output of usr will be: <br/>
{"id":7865.072967009408,"admin":true} <br/>

## Rest and Spread Operator

Let us take use case of reduce helper function that we used previously to sum numbers in an array.  <br/>
function addNumbers(numbers){  <br/>
  return numbers.reduce((sum,number) => {  <br/>
    return sum + number;  <br/>
  },0);  <br/>
}  <br/>
addNumbers([1,2,3,4,5]);  <br/>
Output will be 15  <br/>

Now what if the input to addNumbers was not an array of numbers but multiple numbers. Then in that case the function needs to be modifed as shown below:  <br/>
function addNumbers(num1,num2,num3,num4,num5){  <br/>
  const numbers = [num1,num2,num3,num4,num5];  <br/>
  return numbers.reduce((sum,number) => {  <br/>
    return sum + number;  <br/>
  },0);  <br/>
}  <br/>
addNumbers(1,2,3,4,5);  <br/>
Output will be 15  <br/>

Now in the above case we were aware of the number of arguments to the function. But what if we do know the number of arguments then in such case you can use Rest operator as shown below:  <br/>

function addNumbers(...numbers){  <br/>
  return numbers.reduce((sum,number) => {  <br/>
    return sum + number;  <br/>
  },0);  <br/>
}  <br/>
addNumbers(1,2,3,4,5,6,7,8,9);  <br/>

This would work with any number of arguments to the function.  <br/>
So rest operator is used in function arguments whenever we want to capture list of arguments.  <br/>
So rest operator is used to gather arguments.  <br/>
Similarly there is spread operator that is used to do exactly opposite that is spread the arguments.  <br/>

Let us say we want to combine two arrays:  <br/>
const defaultColors = ['red','green'];  <br/>
const userFavouriteColors = ['orange','yellow'];  <br/>

In previous javascript we used to  use concat function as shown below:  <br/>
defaultColors.concat(userFavouriteColors);  <br/>
Output will be ['red','green',orange','yellow']  <br/>

Same thing can be achieved with the use of spread operator as shown below:  <br/>
[ ...defaultColors, ...userFavouriteColors ];  <br/>

Now if we want to include some additional elements in the output array we would do that as shown below:
['blue', ...defaultColors, ...userFavouriteColors ]; <br/>

Lets take another example of using rest and spread together. Let us say we want to validate my daily grocery shopping list and ensure that I do not forgot buying milk. I can use below function: <br/>

function validateShoppingList(...items){ <br/>
  if(items.indexOf('milk') < 0){ <br/>
    return [ 'milk', ...items ]; <br/>
  }else{ <br/>
    return items; <br/>
  } <br/>
} <br/>

validateShoppingList('oranges','bread','eggs'); <br/>
Output will be: ["milk","oranges","bread","eggs"] <br/>
So even if I forgot to add milk to my shopping list it got included. <br/>

## Destructuring

### Destructuring object
var expense ={ <br/>
  type: 'Business', <br/>
  amount: '$45 USD' <br/>
}; <br/>

//var type = expense.type; <br/>
//var amount = expense.amount; <br/>

Notice that in the above commented var you can see that type is repeated and amount is repeated. <br/>

const {type} = expense; <br/>
const {amount} = expense; <br/>

The above can further be reduced as shown below: <br/>
const {type,amount} = expense; <br/>
The variable name should be identical to the property of the object. Else it will be undefined. <br/>

### Destructuring arguments
Another way of destructuring arguments: <br/>

var savedFile = { <br/>
  extension: 'jpg', <br/>
  name: 'repost', <br/>
  size: 14040 <br/>
}; <br/>

function fileSummary(file){ <br/>
  return `The file ${file.name}.${file.extension} is of size ${file.size}`; <br/>
} <br/>

fileSummary(savedFile); <br/>
Output will be: <br/>
The file repost.jpg is of size 14040 <br/>

The above function can be rewritten by destructuring arguments as shown below: <br/>
function fileSummary({name,extension,size}){ <br/>
  return `The file ${name}.${extension} is of size ${size}`; <br/>
} <br/>

If there is another object such as {color:'red'} that needs to be passed as second argument to the fileSummary function then we can rewrite as: <br/>
function fileSummary({name,extension,size},{color}){ <br/>
  return `The file ${name}.${extension} is of size ${size}`; <br/>
} <br/>

### Destructuring arrays
When we destructure objects we pull off properties. Similarly destructuring arrays is about pulling off elements. <br/>
const companies = [ <br/>
  'Apple', <br/>
  'Google', <br/>
  'Facebook', <br/>
  'Netflix' <br/>
  ] <br/>

const [name,name2,name3,name4] = companies; <br/>
console.log(name); <br/>
console.log(name2); <br/>
console.log(name3); <br/>
console.log(name4); <br/>

We can combine above approach with rest and spread operator as shown below: <br/>
const[name,...rest] = companies; <br/>
Now if you type console.log(rest) you will get the following: <br/>
['Google','Facebook','Netflix'] <br/>

### Destructuring objects and arrays together

const companies = [ <br/>
  {name:'Google', location:'Mountain View'}, <br/>
  {name:'Facebook', location:'Menlo Park'}, <br/>
  {name:'Uber', location:'San Francisco'} <br/>
] <br/>

var locationOfGoogle = companies[0].location; <br/>
The same thing can be achieved using : <br/>
const [{location}] = companies; <br/>
We pulled out the first element of array and then the property location of the first element of the array <br/>
So output can be seen using console.log(location) and it will be Mountain View <br/>

Let us take another example: <br/>
const Google = { <br/>
  locations: ['Mountain View','New York','London'] <br/>
} <br/>
If we had to pull out the first location from locations array we would do the following: <br/>
Google.locations[0] <br/>

Same thing can be done using destructuring as follows: <br/>
const {locations:[location]} = Google; <br/>

One practical use case of destructuring arguments is that we need not worry about the order of the properties that we pull from the object. <br/>
Example: <br/>
const user = { <br/>
  username: 'myusername', <br/>
  password:'mypassword', <br/>
  dateOfBirth: '1/1/1990', <br/>
  city: 'Torrance', <br/>
  email:'test@gmail.com' <br/>
} <br/>

Now if we make a method signup that takes user object as input then we can define it using destructuring as follows: <br/>
function signup({email,dateOfBirth,city,username,password}) <br/>
  //Do something <br/>
} <br/>
Now it can be invoked using signup(user); <br/>

Let us try another use case where destructuring makes code very compatible. <br/>
Lets say we have an array of points: <br/>
const points = [ <br/>
  [4,5], <br/>
  [10,1], <br/>
  [0,40] <br/>
] <br/>

Now we want to convert this to lets say: <br/>
const pointsObjArray = [ <br/>
{x:4,y:5}, <br/>
{x:10,y:1}, <br/>
{x:0,y:40}, <br/>
]  <br/>

This can be done in the following way using traditional approach without ES6: <br/>
points.map(function(pointsArray){ <br/>
  return { <br/>
    x:pointsArray[0], <br/>
    y:pointsArray[1] <br/>
  } <br/>
}); <br/>

Using ES6 destructuring this can be done as follows: <br/>
points.map(([x,y])=>{ <br/>
  return { <br/>
    x:x, <br/>
    y:y <br/>
  } <br/>
}); <br/>

Using enhanced object literal this can be further written as: <br/>
points.map(([x,y])=>{ <br/>
  return { <br/>
    x,y <br/>
  } <br/>
}); <br/>



