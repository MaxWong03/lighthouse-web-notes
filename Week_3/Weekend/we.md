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