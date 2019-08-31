# Objects in Javscript


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