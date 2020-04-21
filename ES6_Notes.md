## forEach helper

Traditional way of writing for loop for arrays:

var colors = ['red','blue','green']; <br/>
for(var i=0; i < colors.length; i++){ <br/>
  console.log(colors[i]); <br/>
} <br/>

Writing using foreach:

colors.forEach(function(color){ <br/>
 console.log(color); <br/>
}); <br/>

Another example of forEach to find sum of all the elements in an array

var numbers = [5,2,8,1,3] <br/>

var sum = 0; <br/>
function adder(number){ <br/>
 sum = sum + number; <br/>
} <br/>
numbers.forEach(adder); <br/>
console.log(sum); <br/>

## map helper

Consider example of doubling numbers in an array in traditional way: <br/>
var numbers1 = [5,2,8,1,3]; <br/>
var numbers2 = []; <br/>
for(var i=0; i < numbers1.length; i++){ <br/>
  numbers2.push(numbers1[i]*2); <br/>
} <br/>
console.log(numbers2); <br/>

doing the same thing using map helper: <br/>
function doubler(number){ <br/>
  return number*2; <br/>
} <br/>

var doubledNumbers = numbers1.map(doubler); <br/>
console.log(doubledNumbers); <br/>

Another example lets say we need to collect prices of cars from cars object array <br/>
var cars = [ <br/>
{model:'Buick',price:'cheap'}, <br/>
{model:'Camaro',price:'expensive'} <br/>
] <br/>
var prices = cars.map(function(car){  <br/>
  return car.price; <br/>
}); <br/>

## filter helper

Consider an example of filter all products of type fruit from a product array: <br/>
var products = [ <br/>
  {name:'cucumber',type:'vegetable'}, <br/>
   {name:'apple',type:'fruit'}, <br/>
    {name:'celery',type:'vegetable'}, <br/>
    {name:'orange',type:'fruit'} <br/>
  ]; <br/>

var filteredFruitProducts = []; <br/>
for(var i=0; i < products.length; i++){ <br/>
    if(products[i].type === 'fruit'){ <br/>
  		filteredFruitProducts.push(products[i]); <br/>
		} <br/>
} <br/>
console.log(filteredFruitProducts); <br/>

Consider the same example using filter helper: <br/>
var filteredFruitProducts = products.filter(function(product){ <br/>
	if(product.type === 'fruit'){ <br/>
    return true; <br/>
  } <br/>
}); <br/>
console.log(filteredFruitProducts); <br/>

Consider another example where you need to filter all vegetables whose price is lesser than 10 and quantity is greater than 5

var products = [ <br/>
  {name:'cucumber',type:'vegetable', price:10, quantity: 30}, <br/>
   {name:'apple',type:'fruit', price:20, quantity:20}, <br/>
    {name:'celery',type:'vegetable', price:9, quantity:10}, <br/>
    {name:'orange',type:'fruit', price:15, quantity:5} <br/>
  ]; <br/>

var filteredVegetables = products.filter(function(product){ <br/>
	return product.type === 'vegetable' && product.price < 10 && product.quantity > 5 <br/>
}); <br/>
console.log(filteredVegetables); <br/>

## find helper
Consider an example to find a user with particular name in this case Alex from an array of users
var users = [ <br/>
  {name: 'Jill'}, <br/>
  {name: 'Alex'}, <br/>
  {name: 'Bill'} <br/>
  ] <br/>

var user;
for(var i=0; i < users.length;i++){
  if(users[i].name === 'Alex'){
    user = users[i];
  }
}
console.log(user);

Now in the above example if you want to break out of loop when you find the required user you can use break statement:
for(var i=0; i < users.length;i++){
  if(users[i].name === 'Alex'){
    user = users[i];
    break;
  }
}

The same requirement can be achieved using find helper as shown below:
var user = users.find(function(user){
  return user.name === 'Alex';
});

The difference between filter and find is that filter loops through the entire array and collects all the elements that meet the filtered criteria and return those elements in an array.
Whereas find will find the first instance of element meeting the criteria and return that element. If there are more than one element meeting the criteria it does not matter since it returns only the first elementm matching the criteria.

## every helper

Consider a use case where you want to find out which computers can run program that requires greater than 16 GB RAM.

var computers = [
  {name:'Apple',ram:24},
  {name:'Compaq',ram:4},
  {name:'Acer',ram:32}
];

var allComputersCanRunProgram = true;
var onlySomeComputersCanRunProgram = false;

for(var i=0; i < computers.length; i++){
  	var computer = computers[i];
  	if(computer.ram < 16){
      	allComputersCanRunProgram = false;
    }else{
      onlySomeComputersCanRunProgram = true;
    }
}
console.log("-------")
console.log(allComputersCanRunProgram)
console.log(onlySomeComputersCanRunProgram)

The above approach uses for loop and is kind of tedious for someone to understand.

 var allComputersCanRunProgram = computers.every(function(computer){
    return computer.ram > 16
  });
  The value of allComputersCanRunProgram will be false since every computer does not have ram greater than 16
  
 var onlySomeComputersCanRunProgram = computers.some(function(computer){
    return computer.ram > 16
  });
 The value of onlySomeComputersCanRunProgram will be true since some computers have ram greater than 16
 
 This is like saying only if every object of the array satisifies the boolean condition return true.
 Only if some objects of the array satisfies the boolean condition then return true.
 
 ## some helper
 
 Only if some objects of the array satisfies the boolean condition then return true.
  var onlySomeComputersCanRunProgram = computers.some(function(computer){
    return computer.ram > 16
  });
 The value of onlySomeComputersCanRunProgram will be true since some computers have ram greater than 16
 
 One of the practical use case where every and some helper could be useful is to validate if all the fields entered by the user on the form is not empty.
 
 ## reduce helper
 
 Consider use case of finding some of numbers of an array as shown using for loop:
 var numbers = [10, 20, 30];
 var sum = 0;
 for(var i=0; i < numbers.length; i++){
  sum = sum + numbers[i];
 }
 console.log(sum);
 
 The same thing can be implemented using reduce function as shown below:
 
  var total = numbers.reduce(function(sum,number){
   return sum + number;
  },0);
 console.log(total);
 
Notice that the initial value of sum is set to 0

Another example to use the reduce helper:
Let us say we want to collect all the colors in the primaryColors object array into a new array

var primaryColors = [
  {color:'red'},
  {color:'blue'},
  {color:'yellow'}
  ];

var colors = primaryColors.reduce(function(previous,primaryColor){
  previous.push(primaryColor.color);
  return previous;
},[]);

console.log(colors)






