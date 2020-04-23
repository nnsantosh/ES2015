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
//Purchase our stuff
gen.next('groceries'); //Output will be {"value":"groceries","done":true} <br/>

Whenever we call gen.next we are transitioning from one state to the other. <br/>
First time we entered store with cash. <br/>
Next time we came out of the store with groceries. <br/>
This is represented by yield. <br/>

