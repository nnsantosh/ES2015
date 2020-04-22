## const and let

const is a keyword that is used to declare a variable whose values we never expect to change.
let is a keyword that is used to declare variables whose values we expect to change over time.

## Template Strings or Template Literals

Whenver we used to concatenate variables to string we used to do in the following way:

function getMessage(){
  const year = new Date().getFullYear();
  return "the year is "+year;
}
getMessage();
The output will be: the year is 2020

Same thing can be written as:

function getMessage(){
  const year = new Date().getFullYear();
  return `the year is ${year}`;
}
In fact we can put any valid javascript expression inside the curly braces along with $ symbol.
function getMessage(){
 return `the year is ${new Date().getFullYear()}`;
}

Lets take another example:
const device_id= 4;
const guid = 20;
const username = 'Santosh';
const data = '{"device_id":"'+ device_id +'","guid":"'+ guid +'","username":"'+ username +'"}'
console.log(data)
The output will be: {"device_id":"4","guid":"20","username":"Santosh"}

Now the same thing can be done using template strings as shown below:
const data = `{"device_id":${device_id},"guid":${guid},"username":${username}}`;

## Arrow functions
Let us say we have function to add two numbers and return the sum:
const add = function(a,b){
  return a + b;
}
We can write this using fat arrow function as:
const add = (a,b) => {
  return a + b;
}

If the body of the javascript function has just one single expression then we can write as:
const add = (a,b) => a + b;
We gain implicit return in this case. Only if curly braces are not used then we get this implicit return.

If the function has single parameter then the paranthesis for parameters is also not required.
Example:
const double = function(num){
  return num * 2;
}
We can write this using fat arrow function as:
const double = num => num * 2;

In case function does not have any parameters then in that case also paranthesis has to be maintained for the parameters.

We can also surround the arrow function with parantheis as below:
const double = (num => num * 2)

Fat Arrow functions solve one major problem.

Consider below function:
const team = {
  members: ['Jane','Bill'],
  teamName: 'Super Squad',
  teamSummary: function(){
    return this.members.map(function(member){
      return `${member} is on team ${this.teamName}`
    });
  }
}
Now when we invoke teamSummary() function:
team.teamSummary();

We get following error: TypeError: Cannot read property 'teamName' of undefined

Now if we replace the function with arrow function as shown below:
const team = {
  members: ['Jane','Bill'],
  teamName: 'Super Squad',
  teamSummary: function(){
    return this.members.map((member) => {
      return `${member} is on team ${this.teamName}`
    });
  }
}
And if we invoke team.teamSummary() we get the following output correctly: 
["Jane is on team Super Squad","Bill is on team Super Squad"]






