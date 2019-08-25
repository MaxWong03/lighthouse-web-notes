# Weekend Notes

## Every File in Node Is A Module
* `Every` file run by Node has `access` to a `module object`
> The node module object contains info such as:
``` js
Module {
  id: '.',
  path: '/Users/administrator/LightHouse/w1/weekend',
  exports: {},
  parent: null,
  filename: '/Users/administrator/LightHouse/w1/weekend/moduleCheck.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/administrator/LightHouse/w1/weekend/node_modules',
    '/Users/administrator/LightHouse/w1/node_modules',
    '/Users/administrator/LightHouse/node_modules',
    '/Users/administrator/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ]
}
```
* Each file that Node runs is actually considered a separate module 
## Exporting Modules
* A JS file must `export` the part that it wanst to be `require`-able (importable). Files usually export an `object` / `function`
## Reuqiring a Module
* Here is the basic syntax to import a module from local filesystem using `reuqire`:
``` js
const sayHelloTo = require('./myModule`);
//assuming we have a file called myModule.js in the same directory as the file that is requiring the module
//requiring an module that doesnt exist or hasnt exported yet will return an empty object {}
//node will export an empty object for each file
```
## Exporting Modules Continued 
``` js
module.exports = sayHelloTo; //the function/object you want to export
//now your file exports the function instead of {}
```
## Conclusion
__In Node...__
1) modules are ways of orgnaizing code into individual files
2) Every js file in node is implicity a module
   * `console.log(module)` to see the details
3) `module.exports` tells node `what to export` from a file
   * default is {}
4) use `require` to import

## Packages and npm
* `npm` is node.js` package manager, it allows you to install and use open-source JS packages

### Packages
* `packages` are `self-contained` code libraries that we can intsall and use in our projects
* packages prvide additional `functionality` in node

## Installing Packages
__use__

>npm install chalk

__this downloads chalk into the current directory/project we are in, and save it as a dependency in the pacakge.json file__

## package.json
__a pacakge.json file looks something like this:__
``` js
{
  "name": "project-name",
  "version": "1.0.0",
  "description": "Short project summary",
  "main": "index.js",
  "scripts": {
    "myscript": "ENV=development node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "MIT",
  "dependencies": {
    "express": "^4.13.4"
  }
}
```
__contains basic attributes such as project name, description, and author__
>npm run myscript <- allows you to run commands using alias
## Dependencies in package.json
* The `dependencies` section of package.json `lists` pacakges that `need to be installed` for the project to `run properly`
* npm by `default` __add the package you install__ as a `dependency`
* the subdirectory `nodle_modules` contains each installed pacakge
* Sometimes after you install `only one` package, you will see `multiple packages` gets installed, thats because your installed packages might `depend` on `other` packages
* `package-lock.json` file lists all details about a project's dependicies. It should be checked into git with `package.json`
* `node_modules` directory is `gitignored`
* `Avoid` editing `package-lock.json` directly. Modify indirectly via commands like `npm install`
* lets say you have a `pacakge A` that __depends__ on `pacakge B` that __depends__ on `package C`. Imagine pacakge B depends on a `older version` of pacakge C. Now package C `updates`, and if the author of_ pacakge A_ `decides to pull` the `newer version` of __pacakge C__, it might `break` the project because __pacakge B is still depending on the older version of package C__
* npm uses `package-lock.json` to prevent the above issue
* any future installion base its work off `package-lock.json`
* npm install, npm rm, npm udate `automatically` sync the exisiting lockfile
* use --no-save option to `prevent` saving altogether 
* `commit` the pacakge lock to git
* Sometimes, two `separate` npm install will create package locks that cause `merge conflicts`
* Solve manually by fixing any `package.json` conflicts, then run npm install[--package-lock-only]. Npm will automatically resolve any conflicts for you

## Automated Testing
* A software development techinque in which you divide your software up into small isoalted units 
* and then you write automated tests for those that verify that each unit work as expected 
* Code can start simple and grows into mutiple use cases and too many ot keep in our head, so automated testing is very useful
* Automated Testing is the practice of `writing code` to `programatically` __test__ the `actual code` want to write
* The test should tell you something about the program

## Automated Testing benefits
1) saves testing time (by not repeating manual test)
2) saves debugging time by catching bugs earlier
3) makes it easier to program because we just need the parts that we are working on (instead of keeping the entire application in our head)
4) makes it easier to come back to a program after sometime (test do not forget about programs)
5) test will catch bugs introduced by others on our team
6) acts as a documentation (reading test is a great way to learn about how code is meant to be used
7) imrpoves the quality of our code
## Types of Testing
### Unit Testing
* Unit testing is the practice of `testing small pieces of code`
* typically `individual functions`, __alone and isolated__
* ex: if your test use external resource such as network or database, it isnt unit test
* Unit test should just `give` the `function` thats tested some `inputs`, and `check` what the function `outputs` is `correct`
* Code thats hard to unit test usually has poor design
* Unit case is the safety net when doing changes
* Unit test are great for regression prevention
* Units test are very `specific`
### Integration Testing
* The idea is to `test` how `parts` of the `system` __work__ `together` (integration of parts)
* Integration test `are not` isolated from other components
* When unit testing is not enough, use integration testing
* Ex: have to check two seperate system (database and app) work `together` correctly
* Focus on unit tests unless you abosultey need an integration test
### Functional Testing 
* aka `E2E` testing or `browser` testing
* Defined as the testing of `complete functionality` of some application
* In web dev, this means using some tool to automate a browser then click around on the page to test the application
* Functional test should be used for testing `common` `user` `interaction` (registerting an account)
* Tools: `Selenium, PhantomJS, CasperJS`
### Happy Path Testing
* A happy path is the path through a system where everything works (data ✅, system 🆙, user well-behaved)
* We test happy path first because we understand how the system should function and want to ensure the basic features should work
* 20% happy path, 80% off the path
## Unit test (Revist)
* Unit test tell us if our code is `working`
* Allows use to `add new features` much `faster` than before
* __General Note__: `if there is a task that can be automated, we automate it` 
* When you test your codebase, you take a piece of code (function) and verify it behaves correctly in a sepcific situation
* The more test you write, the bigger the benefit you receive
* The `core` idea with unit testing is to test a function's `bheaviour` when `giving` it a certain `set of inputs`
* __Principles__: given ceratin inputs, we expect a specific outcome
### Tools
* if you want to test code in the borwser, run npm install mocha chai --save-dev
* if you want to test Node.js code. run npm install -g mocha
* `Mocha` allws us to run test and `Chai` contains helpful function to verify our test results
> You should put your tests in a separate directory from your main code files, this makes it easier to structure them. For exmaple if you want to add other types of test in the future. In JS, we but test files in project's root directory test/
### Setting up a Test runner
* Inorder to run our tests in a `browser`, we need to set up a simple HTML page to be our test runner page
* The page loads Mocha(testing library) and test files
* To run the test, we open the runner in a browser
``` html
<div id="mocha"></div>
<script src="node_modules/mocha/mocha.js"></script>
<script src="node_modules/chai/chai.js"></script>
<script>mocha.setup('bdd')</script>

    <!-- load code you want to test here -->

    <!-- load your test files here -->

<script>
  mocha.run();
</script>
```
### The important bits in the test runner are:
1) load Mocha's CSS to give result nice format
2) create a div with `id = mocha`, where test results are inserted
3) load Mocha and Chai located in `node_modules`
4) `mocha.setup` make Mocha`s testing helper available
5) then load the code we want to test and test files
6) call `mocha.run` to run test. Call this `after` loading the source and test file
### The Basic Test Building Blocks
Every test case follow the same pattern. __First__, you have a `describe` block:
``` js
describe('Array', function() {
  it('should start empty', () => {
    //test implemenation goes here
  });
  // more test case
});
```
* `describe` is used to group individual tests
* the first parameter `indicates what` we are testing
* `it` is used to create actual test
* the first parameter provides a readable description of the test
* First we use `describe` to say what we are testing
* Then we use a number of `it` to create the individual test case, each `it` should explain one `specific behavior`
### Writing the Test Code
``` js
const assert = chai.assert;
describe('Array', function(){
  it('should start empty', () => {
    const arr = [];
    assert.equal(arr.length, 1, 'array is empty'); //from chai.assert, the 3rd parameter is the helper message
  });
});
```
* First you have something you are testing
* Then you do something with the test
* The last thing in a test should be the validation (an assertion which checks the result)
``` js 
//this is a good and easy to start listing all the behaviours (within the same case) you want to test
describe('addClass', function() {
  it('should add class to element');
  it('should not add a class which already exists');
});
```
``` js
describe('addClass', function() {
  it('should add class to element', function() {
    var element = { className: '' }; //start with a skeleton empty object

    //passing element to your add class function, test-case is the input
    addClass(element, 'test-class'); // here are you are testing out the behaviour your addClass function, and see if it does indeed add a class if it isnt already in it

    assert.equal(element.className, 'test-class'); // here you are verifying the behaviour output by your function is indeed the expected behaviour
  });

  it('should not add a class which already exists');
});
```

### Testing in Node vs testing in Browser
* Testing in Node you have to first `export` the function you want to test, and then `require` it in your test case doe
* Testing in the browser requires you to include the code you want to test and test code in <script></script>, and if you use require it will general an error when you launch the browser
* You could include multiple function to export by doing 
``` js
module.export = {
  function1: //function 1 implementation / variable
  function2: //function 2 implemetnation / variable
  ...
}
```



## BDD
* BDD (Behavior Driven Development) encourages the `specificity` of the `behaviour` of your app in terms of `user stories` which are broken down into `scenarios` that can be `built` and `tested`
### BDD Frame Works
* When we write `tests`, we are `testing` the `behaviour` of our code
* Every test invovles:
  1) `setting` up `data`
  2) `running` code that `should` `do` `something`
  3) `asserting` that it `does` that thing
### Setting Up
* `Mocha` is the testing frame work and `Chai` is the assertion library

__Warning__
> In order to test in console you must require('chai'). However, there is no require in browser-based JavaScript. When testing in browser we do not include require('chai'). If we do include it in the browser, it will cause an error.
## Javascript things
``` js
//In javascript, you could check if an object has a specific key by doing
(!obj.key) //this means the object doesnt have the property key
(!!obj.key) //this means the object does have the property key
//so for exmaple if you have 
const order = {
  items: [//also this way is a very readable way of lisiting array of objects
    {name: 'dragon food', price: 8, quantity: 8},
    {name: 'dragon cage', price: 800, quantity: 2},
    {name: 'Shipping', price: 40, shipping: true}
  ]
};
//you can get all items inside the order object that doesnt have the key shipping by doing
order.items
  .filter(x => !x.shipping) 
//and you get all the items inside the order object that does have the key shipping by doing
order.items
  .filter(x => !!x.shipping)
//you could chain methods in a more readable way by doing
order.items
  .filter(x = > !x.shipping) //return an array that does not have the key shipping in items (which is inside object)
  .reduce((prev, cur) => prev + (cur.price * cur.quanity),0) //return the value of the sum of all object's (inside the item array) price value and quanity value 
//you could also assign a variable with a trenaory operator
const shipping = totalItems > 100 ? 0 : shippingItem.price
```