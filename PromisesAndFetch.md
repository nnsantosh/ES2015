## Promises
Promises will generally have 3 states:
1. Unresolved/pending- waiting for something to finish.
2. resolved-something finished and it all went OK.
3. rejected-something finished and something went bad.

After promise is resolved we can register callback function with then.
If promise is rejected then we can register callback function with catch.

Since ajax requests take time to execute we can simulate that using setTimeOut

const promise = new Promise((resolve,reject) => {
  setTimeOut(() => {
  resolve();
  },3000});
});

promise.then(() => {
  console.log("finally finished!");
}).then(() => {
  console.log("I was also ran!");
}).catch(() => {
  console.log("uh oh!");
});

In this case we can see after 3 seconds the functions registered in then execute:
finally finished!
I was also ran!

If we call reject:
const promise = new Promise((resolve,reject) => {
  setTimeOut(() => {
  reject();
  },3000});
});
Then the function registered in catch will execute after 3 seconds:
uh oh!

## Fetch
ajax requests are made using fetch.
Example:
url = https://jsonplaceholder.typicode.com/posts/
fetch(url);
fetch returns a promise
So we can register our callbacks using then and catch
fetch(url).then(data => console.log(data));
You will notice that the data that is returned is not the actual data that you expected to see.
It is just response object.
For getting data that we actually care about we need to do following:
fetch(url)
.then(response => response.json())
.then(data => console.log(data));

