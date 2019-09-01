# Objects in Javscrip

## OOP
* Use `Dependency Injection`Which means passing an object the things it needs rather than having the object access them itselfThat makes for code much more modular and testable

## Bind
### How the THIS keyword works with Object Literals and BIND

``` js
let dog = {
  sound: 'woof',
  talk() {
    console.log(this.sound);
    //here we have a property sound with the value woof
    // and the talk method using the this keyword to brings out the sound property to the console
  }
};

dog.talk();

//Observation
//we took the dog.talk method and we assigned it to a variable and then we called that variable and that returned undefined

let talkFunction = dog.talk;

//reassigning a method to a variable like this, it is now long longer a method it is just a function it has kind of ceased to be a method connected to an object its now just a free flowing function

talkFunction();
//so when you call it here "this" is no longer going to be the dog , it has lots its conenction to the dog object

/**
 * In a function, the THIS keyword does not refer to the context where the function was defined, it refers to the context where the function is being called 
 * 
 * We can bind it to that context by using the function "bind"
 *
 */

let boundFunction = talkFunction.bind(dog);

boundFunction();

/**
 * The bind function here is going to take the talkFunction and its going to return a new function here that has bound dog to the THIS keyword. so BIND forces "THIS" to be dog.  
 */

 let button = document.getElementById('myNiceButton');

 button.addEventListener(
   'click',
   dog.talk
 )

 /**
  * Here we assign the talk method to the click handler of the button but when the click handler is being called THIS is not going to be the dog its going to be the window object becaues that is where the add event listneer are being triggered 
  * 
  * There fore people will solve this by binding dog.talk with dogtalk.bind(dog)
  */

 /**
  * Here we assign the talk method to the click handler of the button but when the click handler is being called THIS is not going to be the dog its going to be the window object becaues that is where the add event listneer are being triggered 
  * 
  * There fore people will solve this by binding dog.talk with dogtalk.bind(dog)
  */

  /**
   * Side note, addEventListenr listen to the click event, and when that event is triggered, it runs the dog.talk.bind(dog) fucntion
   * 
   */
```

## How JS Actually Works
* JS is a single threaded non blocking asynchronous concurrent runtime
* JS has a call stack, an event loop, a callback queue, and some other apis and stuff

![image](js.png)

# The Engine
* `Heap` is the memory allocation and mangament 
* `Callstack` is inside of v8
  - One thread == one call stack == one thing at a time
  - Callstack is how JS runtime figures out what function is JS currently workign through and when the function is finished where the function returns to   
  - The deepest function is at the bottom, and the most recent function that generates the current error is at the top of the call stack

# Concurrency & the Event Loop
* Everytime there is a async code, JS push the task from stack to the webapi (by firing a thread), and put the rest of the code on the stack
* When the async code is finished from the webapi, and puts its callback in the task queue / call back queue
* Event loop: push the call back of that async code in the task queue onto the stack if the stack is cleared
* The call back is then executed and get cleared
* For the DOMS, the DOM stay in the webapi and whenever the dom event is triggered it pushes its callback into the taskqueue (they cant do two things at once, so this is gonna cause a race condition)

# Promise review
* The promise object is used for `deferred` and asynchronous computations
* JS's thread ensure javscript runs synchronously (things run in a single line)
* Promise can only settle once
* Promise execute in the main thread (but still in web api. but can potentially blocking)
* Promise decides what will happen when an asynchronous task settles

``` js
new Promise( (resolve, reject) => {
  let img = documnet.createElement('img');
  img.src = 'image.jpg';
  img.onload =  ;
  img.onerror = reject;
  document.body.appendChild(img);
})
.then(finishLoading)
.catch(showAlternate Image)

```
1) In this Example, the promise either resolve or reject base on whether or not the image onLoad or onError
2) The promise is resolved, but it isnt fulfilled / settled just yet, because it still has some left over code to execute after it has resolved or rejected
3) it then executes another line of code documnet.body.appendChild
4) then when that code finshes, the promise has officially fulfilled / settlted
5) and the THEN gets triggerd, because then only gets triggered when a prommise is fulfilled / setttled
6) Being able to call resolve and reject allows you to define what consitutes reject and resolve in your promise
7) The value passed into resolve and reject is the value THEN and CATCH receives once a promise fulfills
8) If a promised P is passed to resolve, P gets executes FIRST and the resolved value of P will be passed to the next then
9) As soon as a promise rejects, JS skips to the .catch in the chain, that means you just need one .catch to catch all promise errors 




## JS Best Practices
``` js
//put obj short hand notation first 
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

const obj = {
  anakinSkywalker,
  lukeSkywalker,
  ep: 1,
  season: 2
}

//use method shorthand
const obj2 = {
  addvalue(value) {
    return value + 1;
  }
}

//use computed property names when creating objects with dynamic property name

getKey(k) => {
  return `a key name ${k}`;
}

const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('myKey')]: true
  //square bracket notation because its gonna be a string
  //this allows you to generate dynamic property key name
}

//only quote properties that are invalid identifier
const good = {
  foo: 3,
  bar: 4,
  'date-blah': 5
}

//use push instead of direct assignment
const someStack = [];
someStack[someStack.length] = 'abc' //bad
someStack.push(abc) //good

//use array spreads ... to copy arrays
const itemsCopy = [...items]

```
### JS Things
``` js 
let a = [1,2,3,4,5];
console.log(...a) //print 1 , 2, 3, ,4, 5

let obj = {a: 1, b: 2};
console.log({...obj, c:3}) //{a: 1, b: 2, c:3}

//array descturcting
const arr = [1, 2, 3, 4];
const [a,b,c,d] = arr;
a = 1, b = 2, c = 3, d = 4
const [first, second] = arr; 
first = 1, second = 2

//object desctructing
processInput(input) => {
  return {left, right, top, bottom};
}

//the caller selects only the data they need
const {left, top} = processInput(input);

```
> Read Open Source Code to learn best practices 

# Curl
* curl is used to make HTTP requests to given URL and it outputs the response, it allows you to see the URL
* adding the -i flag allows you to inspect the response header 

```
curl -i https://ipvigilante.com/8.8.8.8

header:

HTTP/1.1 200 OK
Server: nginx/1.16.0
Content-Type: application/json
Transfer-Encoding: chunked
Connection: keep-alive
Cache-Control: no-cache, private
X-RateLimit-Limit: 60000
X-RateLimit-Remaining: 59999
Date: Sat, 31 Aug 2019 23:56:06 GMT

body:

{"status":"success","data":{"ipv4":"8.8.8.8","continent_name":"North America","country_name":"United States","subdivision_1_name":"California","subdivision_2_name":null,"city_name":"Mountain View","latitude":"37.38600","longitude":"-122.08380"}}
```

## OOP
* Use `Dependency Injection`
* Which means passing an object the things it needs rather than having the object access them itself
* That makes for code much more modular and testable
* Unless you want your subclass to override the constructor inside ways for whatever reason, you dont have to include the constructor in your subclasses and call super
* That is because the subclass extends the state and behaviour of the super class, so when it extends the superclass it alreadys inherited the constructor methods
* The reamining code in the subclasses is logic that could not be shared with the others

``` js 
/**
 * Here, by storing all the transaction in an array ...
 * the get keyword can then calculate balance on the fly
 * instead of keeping tracks of the balance
 * This is extremely flexible because we dont know how many transaction there will be, and it doesnt matter
 * the get handles the calculating of the balance for us and its flexible in a way that it takes into the # of transaction there is into account
 * The add Transaction opens up a way for the Transaction class to interact with the account class by pushing the transaction into the array that stores all the transaction
 * 
 * */
class Account {
  constructor(username) {
    this.username = username;
    this.transaction = [];
  }
  get balance() {
    const reducer = (prev, curr) => prev + curr;
    return this.transaction.reduce(reducer, 0);
  }
  addTransaction(transaction) {
    this.transactions.push(transaction);
  }
}
class Transaction {
  constructor(account, amount) {
    this.account = account;
    this.amount = amount;
  }
  commit() {
    /**
     * Because in a function, the THIS keyword refers to the contect in which it is called
     * A Transaction is an abstract class so it will never call this function
     * Instead it is the subclass who is going to call this function
     * Therefore, when the subclass Withdrawl and Deposit call this commit function, the this keyword is going to bind to (refers to) the the WithDrawl class and Deposit Class
     * Because that is where the commit function will be called
     * So it results, this.value will not be undefined
     * But it will be the value defined by the getter below
     * * And you dont even have to worry about updating the balance because when we want to retrieve the account will automatically calcualte the balance for us on the fly
     */
    this.account.addTransaction(this.value);
  }
}

class Withdrawal extends Transaction {
  get value() {
    return -this.amount;
  }
}

class Deposit extends Transaction {
  get value() {
    return this.amount;
  }
}
/**
 * The get keyword here is actually very clever
 * it allows one superclass to generalize the fact that there is an amount for all transaction
 * But it determines the value to + or - depending on what kind of transaction it is, and that is done through the get keyword
 * The superclass can then use this.value in the commit function to then again generalize one common commit, but depending on whether withDrawl or Deposit calls the commit methods, it will have different side effect
 */
```

## DNS (Domain Name System)
* A web URL is an `alias` for an `IP address` that `requests` can be `routed` to
* DNS transaltes URL names into IP address numbers
1) When you first enter an URL into your browser, your computer will first determined whether or not they know the IP address already
2) If they both dont know, the OS ask the resolving name server for the URL ip address
3) If it does not, the RNS will ask the ROOT server
4) The root server will guide resolving name server to TLD (top level domain name server)
5) TLD will then guide the resolvling name server to the AUS (authorative name server) that store the URL IP address
6) Resolving name server then goes to the AUS and get a response (ip address) from AUS, cache it in memory, give it back to the OS and the OS gives it back to the browser then makes a collection to that IP address
 
## Refactoring 
* A good example of refactoring is when the implementation of classes or methods changes, but the way you create instances, the interface, the driver code have zero change
  
# Express Server
``` js 
const express = require('express'); //requiring the express package
const app = express(); //starting the express server
const port = 3000; //specify the ports your server is listening to

// "/" will indicate the landing page
//in which if the server sees a connection to the landing page, it will then send a response to the clients
//the response in this case is hello world
app.get("/", (req, res) => {
  res.send("Hello Word!");
});

/**
 * "/parks" here is another page at the address, /parks
 * so when a client request localhost:3000/parks
 * the server sees that request / connection
 * and will send a response being the parks you have seen
 * so in this case, app.get("/parks") allows you to create a new page address and decide what response you want to send back to the client
 * */

app.get("/parks", (req, res) => {
  res.send("The parks you have seen");
});


//here your app server is listening to 3000
app.listen(port, () => {
  console.log("server running);
});

```