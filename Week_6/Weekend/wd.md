# Const Review
``` js
// Although const cannot be reassigned, if the value
// is an array or an object, it's inner parts can be
// changed, as long as the array or object itself isn't
// reassigned
const list = []

// This is allowed because we're not changing the fact
// that list is still the same array. We're just adding
// stuff to it
list.push('Michael')

// But this is not allowed, we cannot change (reassign)
// list to be something other than the array it started
// off to be
list = 'turn list into a string'
```

# Closure Review
* `Nested functions` have `access` to `variables` `declared` in their` outer scope`
* `Functions` in `JS` from `closures`
  - A `clousre` is the `combination` of a `function` and the `lexical environment` within  which that function was `declared`
  - This `environment` consist of `any local variables` that were `in-scope`` at the time the closure was created`
* `Closures` allows `association` of data (lexical environment) with a `function that operates on the data`
* You can use a closure anywhere you might normally use an object with only a single method

``` js
var counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  };
})();
```
* This is a `IFFE`, **which returns an object with three functions that shared one single lexical environment**
* So calling each functions can affect the result of the others, because they all share "privateCounter"
* The shared lexical environment is created in the body of an annonymous functions, which is executed as soon as it has been defined
* The lexical enviornment contains two private items: privateCounter and changeBy
* They must be accessed by the three public functions (wrapped an returned as an object)
* Each closure references a different version, so changing the variable value in one closure do not affect the value in the other closure 

# Functions Review
``` js
// Function Declaration
function getName() {
  return 'Michael'
}

// Function Expression
const getName = function() {
  return 'Michael'
}

// Arrow Function (Which is also an expression)
const getName = () => {
  return 'Michael'
}
```
* The function expression is an expression becaues the function is being assigned to a value
* Declarations can be hoisted and expressions can not
* Arrow functions dont create context so this inside the arrow unfciton is the same as the this on the outside

# Object Shorthand and Destructuring
``` js
const obj = {
  youCanDoThis() {
    //some function
  }
}

function add({x, y}) {
  return x + y;
}

// If the curlies are on the right-hand sign of the
// expression (equal sign) then we're making an object
const obj = { x: 1, y: 2 }

// If they're on the left-hand side (or the receiving
// side as with parameters), then it's destructuring:
const { x } = obj
x // 1
```
* Objects have property names so those have to be used in the destructuring part


# Computed Property Names
``` js
const STATUS_SUCCESS = "STATUS_SUCCESS";
const STATUS_FAILURE = "STATUS_FAILURE";

const messages = {
  [STATUS_SUCCESS]: "Updated",
  [STATUS_FAILURE]: "Error"
};
```

# Spread properties
``` js
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// Object { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }
```


# Array Destructuring
``` js
const arr = ['michael', 'jackson']
const [first, last] = arr
first // michael
last // jackson
```
* Array values are numerically ordered and without names, the order that we destructure is tied to what value we get

``` js
Promise.all([
  Promise.resolve("a"),
  Promise.resolve("b"),
  Promise.resolve("c")
]).then(all => {
  const [a, b, c] = all;
  console.log(a, b, c); // a b c
});

Promise.all([
  Promise.resolve("a"),
  Promise.resolve("b"),
  Promise.resolve("c")
]).then(([a, b, c]) => {
  console.log(a, b, c); // a b c
});
```
* In the first example, all is an array, and [a,b,c] destruct the all array 
* In the second example, it desctructs the array as soon as all the promise is resolved by using ([a, b, c])

# ...Spread Syntax
* A concise way to copy values from existing arrays and objects when creating a new arrays or objects
* Used on the right hand side
* It is used to build object or array
``` js
// Let's say you have this array
const person = ['Michael', 'Jackson']

// If you were to add the above array to a new one like this:
const profile = [person, 'developer']

// The end result would be an array in an array like this:
profile // [['Michael', 'Jackson'], 'developer']

profile[0] // this is an array
profile[1] // this is the string 'developer'

// However, if we had made profile like this with ...
const profile = [...person, 'developer']

// Then the end result would be this:
profile // ['Michael', 'Jackson', 'developer']

// The same concept works with objects
const person = { first: 'Michael', last: 'Jackson' }
const profile = { ...person, occupation: 'developer' }
profile // { first: 'Michael', last: 'Jackson', occupation: 'developer' }
```

# ...Rest Syntax
* Used on the left hand side
* It is used to break array and object down into pieces
* three dots ... followed by a variable name means we want all the rest of the properties into this rest object
``` js
const profile = { first: 'Michael', last: 'Jackson', occupation: 'developer' }
const { occupation, ...rest } = profile
occupation // developer
rest // { first: 'Michael', last: 'Jackson' }

function myFunction(first, last, ...rest) {
  return rest
}

console.log(myFunction('Michael', 'Jackson', 'Developer', 'California'))
// output: ['Developer', 'California']
```
* The function parameters is suggesting that it wants a first and last name as its first two arguments, but anything you pass in after that will all be added to rest as an array.

# Arrays


## .map()
* Map takes an array, iterates over it with a function and whatever the function returns will be the replacement value for the item we are currently on

## .reduce()
* iterates over an array but the end result is just one value instead of repalcing all the values in the array

## .filter()
* filter gives us a new array with the same values, but only if the iterator function returns true

## .find()
* return the first item to get true returned from the iterator function is returned from Find

# Short circuiting with &&
* address issues around accessing properties on undefined variables
* Can be used like a if statement 
``` js
// This will cause an error if `people` is not an array
function findById(people, id) {
  return people.find(item => item.id === id)
}

// Now we are returning the person if `people` is an array
// If `people` is not an array, we the value whatever is before
// && which is `false` in that case
function findById(people, id) {
  return Array.isArray(people) && people.find(item => item.id === id)
}
```

# Throttling and Debounce
* Throttling means to ensure that the function is called at most once in a specificed time period
* Throttling ensure a function is run regualrly at a fixed rate
* A debounced function will ignore all calls to it until the calls have stopped for a specific time period
* Throttling is most useful when the input to the function call doesn’t matter, or is the same each time (for instance, a scroll event), whereas debouncing fits best when the result of the most recent event occurrence (for instance, when resizing a window) is what matters to the end user


