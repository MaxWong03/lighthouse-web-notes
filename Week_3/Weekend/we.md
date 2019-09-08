# What is a Stack
[!What is a stack](https://www.laurencegellert.com/2012/08/what-is-a-full-stack-developer/)
1) `Server`, `Network`, and `Hosting` Environment.
2) Data Modeling
3) Business Logic
4) API layer / Action Layer / MVC
5) User Interface
6) User Experience
7) Understanding what the customer and the business need.

# Event-Driven Architecture
* When `X happens`, then do `Y`
* X is the **EVENT**, Y is the **EVENT HANDLER**

# Document Object Model
* HTML is treated as a  `tree strcuture` 
* Each `node` is an `object` **representing** a `part of the document`
* **DOM**` represents a document with a logical tree
* Each branch of tree ends in a node, each node contains objects
* Dom methods allow you to `change the structure of the tree`, `style`, or `content`
* Nodes can have `event handlers` attached to them

---

* When a `page` is `loaded`, the `browser` is running a `process` that `creates` a DOM 
* Each `HTML element` is also called a `Node` or `DOM Node `(transfering HTML text into an object)
* Which `allows` `Javascript` code to `manipulate` the `web` `page` and `respond`

---
* The broswer creates a representation of the HTML document as the DOM model, which allows JS to access the text content and element of the website document as **objects**
* In the cases where:
  1) DOM is modified by client-side JS
  2) The browser automatically fixes errors in the source code
  HTML source code and DOM arent the same
* **a tbody tag is required inside a table, but developers often fail to include it in their HTML. **

## Event Propagation

## Bubbling and Capturing

### Bubbling
* When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestor
* Bubbling only happens if the parents also have a event handler (doesnt have to be the same handler)
* Almost all events bubble, but not all. focus event is an example

### event.target
* The most deeply nested element that cause the event is called a target element, and its accessible as event.target
* even.target is the target element that initiated the event, it doesnt have through the bubbling process
* this is the current element thats running the handler

> For instance, if we have a single handler form.onclick, then it can “catch” all clicks inside the form. No matter where the click happened, it bubbles up to form and runs the handler.

* Putting a click event listenr on your document will catch all the clicks on your website `document.addEventListener('click'…)`

# Introducing Events
* Whenever `something` interesting `occurs` `on` the `page`, `an event is fired`
* When an event is fired, the `browser` `announces` that something has happened. The announcment allows developer to `listen` for events and `react` to them

## Ways to listen for events
* Developer is only notified about events if they are `listening` for them
* `Listening` for an `event` basically means you are `waiting` for the `browser` to `tell` you a `specific` `event` has `occured` and then you `specify` how the `page should react `
* `Event hanlder` specify to the browser what to do when an event occurs. This function is `executed whenever` the even occurs

``` html
<button onclick="alert('Hello')">Say hello</button>
```

* Here, the `event` we are `listening` to is` specified` by the `onlick` attribute
* And the `event hanlder` is the `alert function`
* `Unobstrusive JS` - keep your HTML and JS file separate and therefore more maintainable
  
### Unobstrusive

``` html
<button id="helloBtn">Say hello</button>
```

```js 
// Event binding using addEventListener
var helloBtn = document.getElementById( "helloBtn" );
 
helloBtn.addEventListener( "click", function( event ) {
    alert( "Hello." );
}, false );
```

* Here we are saving a `reference` to the `button element` by calling `getElementByID` and assinging its return value to a variable
* The `addEventListener` provides an `event hanlder` function that will be called whenver that event occurs

# JQuery
* Jquery abstracts away browser inconsistenices, allowing developer to use a single API
```js
// Event binding using a convenience method
$( "#helloBtn" ).click(function( event ) {
    alert( "Hello." );
});
```
* `$( "#helloBtn" )` selects the button element using the `$` function that returns a JQuery `object`
* the `click` method is called on the jQuery object (returned by the $ function) and pass along an `anonymous function event handler` thats going to be `executed` when a user `clicks the button`

## Example of ways that events can be listened for using Jquery

``` js
$( "#helloBtn" ).on( "click", function( event ) {
    alert( "Hello." );
});
 
// As of jQuery 1.7, attach an event handler to the `body` element that
// is listening for clicks, and will respond whenever *any* button is
// clicked on the page.
$( "body" ).on({
    click: function( event ) {
        alert( "Hello." );
    }
}, "button" );
 
// An alternative to the previous example, using slightly different syntax.
$( "body" ).on( "click", "button", function( event ) {
    alert( "Hello." );
});
```
1) a string `click` is passed as the first argument to the `on` method, then an anonymous function is passed as the second. We are attaching an `event hanlder` `directly` to `#helloBtn`. **If there were any other buttons on the page, they wouldnt alert Hello because the evnet is only attached to the #helloBtn**
2) We are passing an `object` which has the property `click` whose `value` is an `anonymous functions. The `second argument` to the `on method` is a `JQuery selector` string of button`. Example 2 and 3 differes from 1 in the way that the `body element is listening for click events that occur on any button element. 
3) Passed an `event string`, `selector string`, and the `callback` 
* 2 and 3 are an example of `event delegation`, a process by which an `element higher` in the DOM tree `listens` for **events occuring on its childern**

## Event delegation
* `Event delegation` works because of `event bubbling`
* The `delegating element` should always be as `close` to the `delegatees` as possible so the event doesnt have to travel way up the DOM tree before its hanlder function is called

## The event object
``` js
// Binding a named function
function sayHello( event ) {
    alert( "Hello." );
}
 
$( "#helloBtn" ).on( "click", sayHello );
```
* Passing defined functions as event hanlders is important if different elements or different events should perform the same functionality and helps keep the code DRY
* In `all` **DOM event callbacks**, jQuery passes an `event object` that contains `information about the event`
  1) when and where it occured
  2) what type of event it was
  3) which element the event occured on 

* the following code prevent default behaviour of an event and stop event propogation 
``` js
// Preventing a default action from occurring and stopping the event bubbling
$( "form" ).on( "submit", function( event ) {
 
    // Prevent the form's default submission.
    event.preventDefault();
 
    // Prevent event from bubbling up DOM tree, prohibiting delegation
    event.stopPropagation();
 
    // Make an AJAX request to submit the form data
});
```
* the soonest that event bubbling can be stopped is when the event reaches the element that is delegating it
* an `event object` contains a `property` called `originalEvent`. Which is the `event object` that the `browser` itself `created`. This is `useful` for `touch events` on mobile devices and tablets
