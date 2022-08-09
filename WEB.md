# <h1 align="center"> Web Programming ❤️ (as read by Liya) </h1>

### Asynchronous Programming

In a *synchronous programming model*, things happen one at a time. When you call a function that performs a long-running action, it returns only when the action has finished and it can return the result. This stops your program for the time the action takes.
+ You can add other threads: A thread is another running program whose execution may be interleaved with other programs by the operating system—since most modern computers contain multiple processors, multiple threads may even run at the same time, on different processors. A second thread could start the second request, and then both threads wait for their results to come back, after which they resynchronize to combine their results.

An *asynchronous model* allows multiple things to happen at the same time. When you start an action, your program continues to run. When the action finishes, the program is informed and gets access to the result (for example, the data read from disk).
In the asynchronous model, starting a network action conceptually causes a split in the timeline. The program that initiated the action continues running, and the action happens alongside it, notifying the program when it is finished.

![](https://eloquentjavascript.net/img/control-io.svg)

#### Callback asynchronicity

- make functions that perform a slow action take an extra argument, a callback function. The action is started, and when it finishes, the callback function is called with the result.

If a function needs to wait for a slow function it's nested inside of it.
Performing multiple asynchronous actions in a row using callbacks means that you have to keep passing new functions to handle the continuation of the computation after the actions.

Any function that calls a function that works asynchronously must itself be asynchronous, using a callback or similar mechanism to deliver its result.

#### Promised asynchronicity

A **promise** is an object that may produce a single value some time in the future: either a resolved value, or a reason that it’s not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: `fulfilled`, `rejected`, or `pending`. A promise is **settled** if it’s not pending (it has been resolved or rejected). Promise users can attach callbacks to handle the fulfilled value or the reason for rejection.

**[What Is a Promise](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)**

**States:**
Fulfilled: `onFulfilled()` will be called (e.g., resolve() was called)
Rejected: `onRejected()` will be called (e.g., reject() was called)
Pending: not yet fulfilled or rejected
<br> </br>
- Promises are eager, meaning that a promise will start doing whatever task you give it as soon as the promise constructor is invoked.
- Native JavaScript promises don’t expose promise states. Instead, you’re expected to treat the promise as a black box.

The `.then()` method must comply with these rules:

- Both `onFulfilled()` and `onRejected()` are optional.
- If the arguments supplied are not functions, they must be ignored.
- `onFulfilled()` will be called after the promise is fulfilled, with the promise’s value as the first argument.
- `onRejected()` will be called after the promise is rejected, with the reason for rejection as the first argument. The reason may be any valid JavaScript value, but because rejections are essentially synonymous with exceptions, I recommend using Error objects.
- Neither `onFulfilled()` nor `onRejected()` may be called more than once.
- `.then()` may be called many times on the same promise. In other words, a promise can be used to aggregate callbacks.
- `.then()` must return a new promise, `promise2`.
- If `onFulfilled()` or` onRejected()` return a value x, and x is a promise, `promise2` will lock in with (assume the same state and value as) x. Otherwise, `promise2` will be fulfilled with the value of x.
- If either `onFulfilled` or `onRejected` throws an exception e, promise2 must be rejected with e as the reason.
- If `onFulfilled` is not a function and promise1 is fulfilled, promise2 must be fulfilled with the same value as promise1.
- If `onRejected` is not a function and promise1 is rejected, promise2 must be rejected with the same reason as promise1.

```js
const promisedTimeout = new Promise((res, rej) => setTimeout(res, 5000));

promisedTimeout.then(() => console.log('Timed!'))
/* Timed!

[Done] exited with code=0 in 5.084 seconds */
```
```js
const promisedTimeout = new Promise((res, rej) => setTimeout(res, 3000));

promisedTimeout.then(() => console.log('Timed!')) 
/* Timed!

[Done] exited with code=0 in 3.102 seconds */
```
```js
const promisedFakeRead = new Promise((resolve, reject) => { 
    reject(JSON.parse(file));    
})

promisedFakeRead.catch(e => console.log(e.message));
// file is not defined
```
![](https://i.gifer.com/MerC.gif)

#### async and await
The async keyword gives you a simpler way to work with asynchronous promise-based code. Adding `async` at the start of a function makes it an async function. 
1. Inside an async function you can use the await keyword before a call to a function that returns a promise. This makes the code wait at that point until the promise is settled, at which point the fulfilled value of the promise is treated as a return value, or the rejected value is thrown.

2. An async function is a special type of generator. It produces a promise when called, which is resolved when it returns (finishes) and rejected when it throws an exception. Whenever it yields (awaits) a promise, the result of that promise (value or thrown exception) is the result of the await expression.

This enables you to write code that uses asynchronous functions but looks like synchronous code.

```js
async function awaitableExampy(n){
    return n ** 3 + 4 * 8;
}

async function waitingForExapmy(){
    return awaitableExampy(6);
}

(async function logger() {
    console.log(await waitingForExapmy()); // 248
})()
```
```js
async function awaitableExampy(n){
    return n ** 3 + 4 * 8;
}

async function waitingForExapmy(){
    return awaitableExampy(6);
}

(async function logger() {
    console.log(waitingForExapmy()); // Promise { <pending> }
})()
```
#### The event loop

[DOCS: Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

Messages in queue get processed (if any) => call corresponding functions => get frames on stack => return => get popped out => and so on... 

### Ze WEB

- The World Wide Web (WWW), commonly known as the Web, is an information system enabling documents and other web resources to be accessed over the Internet.

Documents and downloadable media are made available to the network through web servers and can be accessed by programs such as web browsers. Servers and resources on the World Wide Web are identified and located through character strings called uniform resource locators (URLs). The original and still very common document type is a web page formatted in Hypertext Markup Language (HTML). This markup language supports plain text, images, embedded video and audio contents, and scripts (short programs) that implement complex user interaction. The HTML language also supports hyperlinks (embedded URLs) which provide immediate access to other web resources. Web navigation, or web surfing, is the common practice of following such hyperlinks across multiple websites. Web applications are web pages that function as application software. The information in the Web is transferred across the Internet using the Hypertext Transfer Protocol (HTTP).


##### Web Clients and Servers
Web content lives onweb servers. Web servers speak the HTTP protocol, so they are often called HTTP servers. These HTTP servers store the Internet’s data and provide the data when it is requested by HTTP clients. The clients send HTTP requests to servers, and servers return the requested data in HTTP responses, as sketched in Figure 1-1. Together, HTTP clients and HTTP servers make up the basic components of the World Wide Web.

![](https://www.oreilly.com/library/view/http-the-definitive/1565925092/httpatomoreillycomsourceoreillyimages96826.png)

You probably use HTTP clients every day. The most common client is a web browser, such as Microsoft Internet Explorer or Netscape Navigator. Web browsers request HTTP objects from servers and display the objects on your screen.

When you browse to a page, such as “http://www.oreilly.com/index.html,” your browser sends an HTTP request to the server www.oreilly.com (see above). The server tries to find the desired object (in this case, “/index.html”) and, if successful, sends the object to the client in an HTTP response, along with the type of the object, the length of the object, and other information.

##### Node & The Browser
Node and web browsers, both executes JavaScript, but Node does that in server side and browsers in client side. Node uses the same JavaScript engine V8 which is the backbone of Chrome, but still we can find few differences between Node and Browser.
<table width="100%">
<thead>
<tr>
<th width="50%">Node</th>
<th width="*">Browser</th>
</tr>
</thead>
<tbody>
<tr>
<td>&nbsp;Node doesn't have a predefined "window" object cause it doesn't have a window to draw anything.</td>
<td>&nbsp;"window" is a predefined global object which has functions and attributes, that have to deal with window that has been drawn.</td>
</tr>
<tr>
<td>&nbsp;"location" object is related to a particular url; that means it is for page specific. So, node doesn't require that.</td>
<td>&nbsp;"location" is another predefined object in browsers, that has all the information about the url we have loaded.</td>
</tr>
<tr>
<td>&nbsp;Ofcourse Node doesn't have "document" object also, cause it never have to render anything in a page.</td>
<td>&nbsp;"document", which is also another predefined global variable in browsers, has the html which is rendered.</td>
</tr>
<tr>
<td>&nbsp;Node has "global", which is a predefined global object. It contains several functions that are not available in browsers, cause they are needed for server side works only.</td>
<td>&nbsp;Browsers may have an object named "global", but it will be the exact one as "window".</td>
</tr>
<tr>
<td>&nbsp;"require" object is predefined in Node which is used to include modules in the app.</td>
<td>&nbsp;Browsers don't have "require" predefined. You may include it in your app for asynchronous file loading.</td>
</tr>
<tr>
<td>&nbsp;In Node everything is a module. You must keep your code inside a module.</td>
<td>&nbsp;Moduling is not mandatory in client side JavaScript, i.e. in browsers.</td>
</tr>
<tr>
<td>&nbsp;Node is headless.</td>
<td>&nbsp;Browsers are not headless.</td>
</tr>
<tr>
<td>&nbsp;Node processes request object.</td>
<td>&nbsp;Browsers processes response objects.</td>
</tr>
</tbody>
</table>


<br/>
<br/>
#### HTML: HyperText Markup Language

HTML is a markup language that defines the structure of your content. HTML consists of a series of elements, which you use to enclose, or wrap, different parts of the content to make it appear a certain way, or act a certain way. The enclosing tags can make a word or image hyperlink to somewhere else, can italicize words, can make the font bigger or smaller, and so on. For example, take the following line of content:

The main parts of our element are as follows:

1. The opening tag: This consists of the name of the element (in this case, p), wrapped in opening and closing angle brackets. This states where the element begins or starts to take effect — in this case where the paragraph begins.
2. The closing tag: This is the same as the opening tag, except that it includes a forward slash before the element name. This states where the element ends — in this case where the paragraph ends. Failing to add a closing tag is one of the standard beginner errors and can lead to strange results.
3. The content: This is the content of the element, which in this case, is just text.
4. The element: The opening tag, the closing tag, and the content together comprise the element.

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics/grumpy-cat-small.png)

**Attributes** contain extra information about the element that you don't want to appear in the actual content. Here, class is the attribute name and editor-note is the attribute value. The class attribute allows you to give the element a non-unique identifier that can be used to target it (and any other elements with the same class value) with style information and other things.

An attribute should always have the following:

- A space between it and the element name (or the previous attribute, if the element already has one or more attributes).
- The attribute name followed by an equal sign.
- The attribute value wrapped by opening and closing quotation marks.

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics/grumpy-cat-attribute-small.png)


##### HTML Doc Anatomy

- ***!DOCTYPE html*** — doctype. It is a required preamble. In the mists of time, when HTML was young (around 1991/92), doctypes were meant to act as links to a set of rules that the HTML page had to follow to be considered good HTML, which could mean automatic error checking and other useful things. However these days, they don't do much and are basically just needed to make sure your document behaves correctly. That's all you need to know for now.

- ***html><html*** — the **html>** element. This element wraps all the content on the entire page and is sometimes known as the root element. It also includes the lang attribute, setting the primary language of the document.
- ***head></head*** — the **head>** element. This element acts as a container for all the stuff you want to include on the HTML page that isn't the content you are showing to your page's viewers. This includes things like keywords and a page description that you want to appear in search results, CSS to style our content, character set declarations, and more.
- meta charset="utf-8"> — This element sets the character set your document should use to UTF-8 which includes most characters from the vast majority of written languages. Essentially, it can now handle any textual content you might put on it. There is no reason not to set this and it can help avoid some problems later on.
- ***meta name="viewport" content="width=device-width">*** — This viewport element ensures the page renders at the width of viewport, preventing mobile browsers from rendering pages wider then the viewport and then shrinking them down.
- ***title></title*** — the **title>** element. This sets the title of your page, which is the title that appears in the browser tab the page is loaded in. It is also used to describe the page when you bookmark/favorite it.
- ***body></body*** — the **body>** element. This contains all the content that you want to show to web users when they visit your page, whether that's text, images, videos, games, playable audio tracks, or whatever else.

**^link rel="stylesheet" href="mystyle.css">** external sheet
