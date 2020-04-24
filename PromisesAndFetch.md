## Promises
Promises will generally have 3 states:
1. Unresolved/pending- waiting for something to finish.
2. resolved-something finished and it all went OK.
3. rejected-something finished and something went bad.

After promise is resolved we can register callback function with then. <br/>
If promise is rejected then we can register callback function with catch. <br/>

Since ajax requests take time to execute we can simulate that using setTimeOut. <br/>

const promise = new Promise((resolve,reject) => { <br/>
  setTimeOut(() => { <br/>
  resolve(); <br/>
  },3000}); <br/>
}); <br/>

promise.then(() => { <br/>
  console.log("finally finished!"); <br/>
}).then(() => { <br/>
  console.log("I was also ran!"); <br/>
}).catch(() => { <br/>
  console.log("uh oh!"); <br/>
}); <br/>

In this case we can see after 3 seconds the functions registered in then execute: <br/>
finally finished! <br/>
I was also ran! <br/>

If we call reject: <br/>
const promise = new Promise((resolve,reject) => { <br/>
  setTimeOut(() => { <br/>
  reject(); <br/>
  },3000}); <br/>
}); <br/>
Then the function registered in catch will execute after 3 seconds: <br/>
uh oh!

## Fetch
ajax requests are made using fetch. <br/>
Example: <br/>
url = https://jsonplaceholder.typicode.com/posts/ <br/>
fetch(url); <br/>
fetch returns a promise <br/>
So we can register our callbacks using then and catch <br/>
fetch(url).then(data => console.log(data)); <br/>
You will notice that the data that is returned is not the actual data that you expected to see. <br/>
It is just response object. <br/>
For getting data that we actually care about we need to do following: <br/>
fetch(url) <br/>
.then(response => response.json()) <br/>
.then(data => console.log(data)); <br/>

Shortcoming of fetch:
fetch(url) <br/>
.then(response => console.log(response)) <br/>
.catch(error => console.log('BAD',error)); <br/>

With fetch in case of any error it does not execute the call back function registered with catch.
The only time the call back function registered with catch will execute with fetch is if the network request fails.(ex: if the url domain itself is wrong).



