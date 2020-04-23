## Generators

A generator is a function that can be entered and exited multiple times.

Consider below scenario explained by the diagram:
![Generator Story](https://github.com/nnsantosh/ES2015/blob/master/generator_story.jpeg)



The above diagram can be represented using a generator. <br/>
function* shopping(){ <br/>
  //Stuff on the sidewalk <br/>
  //Walking down the sidewalk <br/>
  //go into the store with the cash <br/>
  const stuffFromStore = yield 'cash'; <br/>
  //Walk back Home <br/>
  return stuffFromStore; <br/>
}
//stuff in the store <br/>
const gen = shopping(); <br/>
gen.next(); //leaving our house Output will be: {"value":"cash","done":false} <br/>
//Walked into the store <br/>
//Walking down the aisles <br/>
//Purchase our stuff <br/>
gen.next('groceries'); //Output will be {"value":"groceries","done":true} <br/>

Whenever we call gen.next we are transitioning from one state to the other. <br/>
First time we entered store with cash. <br/>
Next time we came out of the store with groceries. <br/>
This is represented by yield. <br/>

We can call yield from generator mulitple times as shown below: <br/>
function* shopping(){ <br/>
  //Stuff on the sidewalk <br/>
  //Walking down the sidewalk <br/>
  //go into the store with the cash <br/>
  const stuffFromStore = yield 'cash'; <br/>
  //Walking to laundry place <br/>
  const cleanClothes = yield 'laundry'; <br/>
  //Walk back Home <br/>
  return [stuffFromStore,cleanClothes]; <br/>
} <br/>
 
//stuff in the store <br/>
const gen = shopping(); <br/>
gen.next(); //leaving our house <br/>
gen.next('groceries'); <br/>
gen.next('clean clothes'); <br/>

Output will be: <br/>

{"value":"cash","done":false} <br/> 
{"value":"laundry","done":false} <br/> 
{"value":["groceries","clean clothes"],"done":true} <br/>


Lets take another example: <br/>
function* colors(){ <br/>
  yield 'red'; <br/>
  yield 'blue'; <br/>
  yield 'green'; <br/>
} <br/>
const gen = colors(); <br/>
gen.next(); <br/>
gen.next(); <br/>
gen.next(); <br/>
gen.next(); <br/>

Output is: <br/>
{"value":"red","done":false} <br/>
{"value":"blue","done":false} <br/>
{"value":"green","done":false} <br/>
{"done":true} <br/>

Generators work perfectly with for ..of loop. <br/>
function* colors(){ <br/>
  yield 'red'; <br/>
  yield 'blue'; <br/>
  yield 'green'; <br/>
} <br/>
const myColors = []; <br/>
for(let color of colors()){ <br/>
  myColors.push(color); <br/>
} <br/>
Every time for a yield statement in the generator the for of loop executes and yields the value. <br/>
console.log(myColors); <br/>
The output will be:  <br/>
3 <br/>
["red","blue","green"] <br/>

Example of using generator to loop over properties of object: <br/>
const engineeringTeam = { <br/>
  size: 3, <br/>
  department: 'Engineering', <br/>
  lead: 'Jill', <br/>
  manager: 'Alex', <br/>
  engineer: 'Dave' <br/>
}

function* TeamIterator(team){ <br/>
  	yield team.lead; <br/>
  	yield team.manager; <br/>
  	yield team.engineer; <br/>
}

const names = []; <br/>
for (let name of TeamIterator(engineeringTeam)){ <br/>
     names.push(name); <br/>
 } <br/>
 console.log(names); <br/>
 Output will be: ["Jill","Alex","Dave"] <br/>
 
 ## Delegation of Generators
 
Let us take another use case where in the previous example every engineeringTeam will have testingTeam with their own lead and tester. <br/>
In such a case: <br/>

const testingTeam = { <br/>
  lead:'Amanda', <br/>
  tester:'Bill' <br/>
} <br/>

const engineeringTeam = { <br/>
  testingTeam, <br/>
  size: 3, <br/>
  department: 'Engineering', <br/>
  lead: 'Jill', <br/>
  manager: 'Alex', <br/>
  engineer: 'Dave' <br/>
} <br/>

function* TestingTeamIterator(team){ <br/>
  	yield team.lead; <br/>
  	yield team.tester; <br/>
  
} <br/>

function* TeamIterator(team){ <br/> 
  	yield team.lead; <br/>
  	yield team.manager; <br/>
  	yield team.engineer; <br/>
    const testingTeamGenerator = TestingTeamIterator(team.testingTeam); <br/>
    yield* testingTeamGenerator; <br/>
   
}

const names = []; <br/>
for (let name of TeamIterator(engineeringTeam)){ <br/>
     names.push(name); <br/>
 }
console.log(names); <br/>
 Output will be: ["Jill","Alex","Dave","Amanda","Bill"] <br/>
 
 ## Symbol.Iterator
 Symbol Iterator is a tool that teaches objects how to respond to the for of loop. <br/>
 
 Instead of having separate iterator for testingTeam and using yield* we can do the following: <br/>
 
 const testingTeam = { <br/>
  lead:'Amanda', <br/>
  tester:'Bill', <br/>
  [Symbol.iterator] : function* (){ <br/>
   	yield this.lead; <br/>
  	yield this.tester; <br/>
  } <br/>
}; <br/>

const engineeringTeam = { <br/>
  testingTeam, <br/>
  size: 3, <br/>
  department: 'Engineering', <br/>
  lead: 'Jill', <br/>
  manager: 'Alex', <br/>
  engineer: 'Dave' <br/>
}; <br/>

function* TeamIterator(team){ <br/>
  	yield team.lead; <br/>
  	yield team.manager; <br/>
  	yield team.engineer; <br/>
    yield* team.testingTeam; <br/>
  
}; <br/>

const names = []; <br/>
for (let name of TeamIterator(engineeringTeam)){ <br/>
     names.push(name); <br/>
 } <br/>
 console.log(names); <br/>
Output will be: ["Jill","Alex","Dave","Amanda","Bill"] <br/>

Now in the above example we can implement Symbol.iterator even for the engineering team as shown below:
const testingTeam = { <br/>
  lead:'Amanda', <br/>
  tester:'Bill', <br/>
  [Symbol.iterator] : function* (){ <br/>
   	yield this.lead; <br/>
  	yield this.tester; <br/>
  } <br/>
}; <br/>

const engineeringTeam = { <br/>
  testingTeam, <br/>
  size: 3, <br/>
  department: 'Engineering', <br/>
  lead: 'Jill', <br/>
  manager: 'Alex', <br/>
  engineer: 'Dave', <br/>
  [Symbol.iterator] : function* (){ <br/>
   	yield this.lead; <br/>
  	yield this.manager; <br/>
  	yield this.engineer; <br/>
    yield* this.testingTeam; <br/>
  } <br/>
}; <br/>

const names = []; <br/>
for (let name of engineeringTeam){ <br/>
     names.push(name); <br/>
 } <br/>
 console.log(names);
 Output will be: ["Jill","Alex","Dave","Amanda","Bill"] <br/>
