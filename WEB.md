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
**[Promisesss](https://web.dev/promises/?gclid=Cj0KCQjwl92XBhC7ARIsAHLl9akniUe24enj6Y4mG72YefsCmnmiJv8oUbL7YiqHq-4-g9FwH4IKU7AaAj86EALw_wcB)

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

![](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png)

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

#### CSS: Cascading Style Sheets

Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML or XML (including XML dialects such as SVG, MathML or XHTML). CSS describes how elements should be rendered on screen, on paper, in speech, or on other media.

CSS is among the core languages of the open web and is standardized across Web browsers according to W3C specifications.

CSS is a style sheet language. CSS is what you use to selectively style HTML elements. For example, this CSS selects paragraph text, setting the color to red and so on:

```css
p {
  color: red;
  background-color: #f9fbf2;
  padding-left: 10px;
  margin-top: 6rem;
}
```

##### Anatomy of a CSS ruleset

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/css-declaration-small.png)

<table class="standard-table no-markdown">
  <thead>
    <tr>
      <th scope="col">Selector name</th>
      <th scope="col">What does it select</th>
      <th scope="col">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Element selector (sometimes called a tag or type selector)</td>
      <td>All HTML elements of the specified type.</td>
      <td><code>p</code><br>selects <code>&lt;p&gt;</code></td>
    </tr>
    <tr>
      <td>ID selector</td>
      <td>
        The element on the page with the specified ID. On a given HTML page,
        each id value should be unique.
      </td>
      <td>
        <code>#my-id</code><br>selects <code>&lt;p id="my-id"&gt;</code> or
        <code>&lt;a id="my-id"&gt;</code>
      </td>
    </tr>
    <tr>
      <td>Class selector</td>
      <td>
        The element(s) on the page with the specified class. Multiple instances
        of the same class can appear on a page.
      </td>
      <td>
        <code>.my-class</code><br>selects
        <code>&lt;p class="my-class"&gt;</code> and
        <code>&lt;a class="my-class"&gt;</code>
      </td>
    </tr>
    <tr>
      <td>Attribute selector</td>
      <td>The element(s) on the page with the specified attribute.</td>
      <td>
        <code>img[src]</code><br>selects
        <code>&lt;img src="myimage.png"&gt;</code> but not
        <code>&lt;img&gt;</code>
      </td>
    </tr>
    <tr>
      <td>Pseudo-class selector</td>
      <td>
        The specified element(s), but only when in the specified state. (For
        example, when a cursor hovers over a link.)
      </td>
      <td>
        <code>a:hover</code><br>selects <code>&lt;a&gt;</code>, but only when
        the mouse pointer is hovering over the link.
      </td>
    </tr>
  </tbody>
</table>

<br/>
<br/>

##### CSS basic box model

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/box-model.png)

CSS layout is mostly based on the box model. Each box taking up space on your page has properties like:

- **padding**, the space around the content. In the example below, it is the space around the paragraph text.
- **border**, the solid line that is just outside the padding.
- **margin**, the space around the outside of the border.

**[THE BOX MODEL, BOX-SIZING](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)**

**[FLEXBOX](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)**

**[SELECTOR SPECIFICITY](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)**

![](https://d1rytvr7gmk1sx.cloudfront.net/wp-content/uploads/2013/11/CSSSpecificityFigA110513.gif)
![](https://static.javatpoint.com/csspages/images/types-of-css.png)


### DO-DO-DO-DOMMM DO-DO-DO-DOMMM

**The Document Object Model (DOM)** is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as nodes and objects; that way, programming languages can interact with the page.

The DOM represents a document with a logical tree. Each branch of the tree ends in a node, and each node contains objects. DOM methods allow programmatic access to the tree. With them, you can change the document's structure, style, or content.

Nodes can also have event handlers attached to them. Once an event is triggered, the event handlers get executed.

A web page is a document that can be either displayed in the browser window or as the HTML source. In both cases, it is the same document but the Document Object Model (DOM) representation allows it to be manipulated. As an object-oriented representation of the web page, it can be modified with a scripting language such as JavaScript.


![](https://www.freecodecamp.org/news/content/images/2022/06/DOM-tree.png)

[VERY TECHNICAL](https://www.w3.org/TR/DOM-Level-1/introduction.html)
[DOCUMENT](https://javascript.info/document)

```js
document.querySelector(selector)
document.querySelectorAll(selector)
document.querySelector(selector).innerHTML = HTMLstring
element.setAttribute()
element.getAttribute()
element.addEventListener()
document.getElementById(id)

const id = '#id'; 
const class = '.class'; 

const heading = document.createElement("h1");
         const heading_text = document.createTextNode("Big Head!");
         heading.appendChild(heading_text);
         document.body.appendChild(heading);
```

```js
/**
 * Shorthand for document.querySelector
 * @param {string} selector
 * @return {Element}
 */
export const q = (selector) => document.querySelector(selector);

/**
 * Shorthand for document.querySelectorAll
 * @param {string} selector
 * @return {NodeLists<Element>}
 */
export const qs = (selector) => document.querySelectorAll(selector);

export const renderAdditionalTrending = async (limit, offset) => {
  const moreTrendingGifs = await loadTrendingGifs(limit, offset);

  q(`.${GIF_CONTAINER_SELECTOR}`).innerHTML += toMultipleGIFsView(
    moreTrendingGifs.data,
  );
};

document.addEventListener('DOMContentLoaded', async () => {
  let offsetTrending = 0;
  const limit = 20;

  document.addEventListener('click', async (event) => {
    if (event.target.classList.contains('nav-link')) {
      await loadPage(event.target.getAttribute('data-target-page'));
    }

    if (event.target.classList.contains('logo')) {
      await renderHomePage();
      event.target.classList.add('active');
    }

    if (event.target.classList.contains('theme')) {
      changeThemes();
    }

    if (event.target.classList.contains('suggestion')) {
      document.body.style.backgroundImage = 'none';
      renderSearchItems(event.target.innerHTML);
      // setSearchBarInnerHTML(event.target.innerHTML);
      setSearchBarInnerHTML();
      hideSuggestions();
      q('input#search').focus();
    }

    if (event.target.classList.contains('toUpload')) {
      console.log('in nav');
      console.log(event.target);
      await loadPage(UPLOAD);
    }

    // toggle favorite event
    if (event.target.classList.contains('favorite')) {
      toggleFavoriteStatus(event.target.getAttribute('data-gif-id'));
    }
  });

  document.addEventListener('change', (event) => {
    if (event.target.id === 'file-upload') {
      const file = document.getElementById('file-upload').files[0];
      uploadsHandler(file);
    }
  });

  // search events
  q('input#search').addEventListener('keypress', (event) => {
    setActiveNav();
    // q(`#${CONTAINER_SELECTOR}`).innerHTML = '';

    if (event.key === ENTER_KEY) {
      document.body.style.backgroundImage = 'none';
      // hideSuggestions();
      renderSearchItems(event.target.value);

      hideSuggestions();
      setSearchBarInnerHTML();
    }
  });

  // search suggestions
  q('input#search').addEventListener('keyup', (event) => {
    renderSearchSuggestion(event.target.value);
  });

  setSearchBarInnerHTML;
  document.body.addEventListener('click', () => {
    hideSuggestions();
    setSearchBarInnerHTML();
  });

  // load landing
  await renderHomePage();

  // infinite scroll on trending
  window.onscroll = debounce(async function () {
    const isActive = document
      .querySelector('[data-target-page="trending"]')
      .classList.contains('active');
    const isPageEnd =
      window.scrollY >
      document.documentElement.offsetHeight - window.outerHeight;

    if (isActive && isPageEnd && !q(LOGO).classList.contains('active')) {
      try {
        offsetTrending += limit;
        if (offsetTrending === 4999) offsetTrending = 0;
        renderAdditionalTrending(limit, offsetTrending);
      } catch (error) {
        alert(error);
      }
    }
  }, 600);
});

```

##### Document & Window

- **Document Object**: The document object represent a web page that is loaded in the browser. By accessing the document object, we can access the element in the HTML page. With the help of document objects, we can add dynamic content to our web page. The document object can be accessed with a window.document or just document.
- **Window Object**: The window object is the topmost object of the DOM hierarchy. It represents a browser window or frame that displays the contents of the webpage. Whenever a window appears on the screen to display the contents of the document, the window object is created. 
[DOCU & WIN](https://www.geeksforgeeks.org/differences-between-document-and-window-objects/)
<table><thead><tr><th><h4 style="text-align:center"><strong>document</strong></h4></th><th><h4 style="text-align:center"><strong>window</strong></h4></th></tr></thead><tbody><tr><td><p style="text-align:justify">It represents any HTML document or web page that is loaded in the browser.</p></td><td><p style="text-align:justify">It represents a browser window or frame that displays the contents of the webpage. &nbsp;&nbsp;</p></td></tr><tr><td><p style="text-align:justify">It is loaded inside the window.</p></td><td><p style="text-align:justify">It is the very first object that is loaded in the browser.</p></td></tr><tr><td><p style="text-align:justify">It is the object of window property.</p></td><td><p style="text-align:justify">It is the object of the browser.</p></td></tr><tr><td><p style="text-align:justify">All the tags, elements with attributes in HTML are part of the document.</p></td><td><p style="text-align:justify">Global objects, functions, and variables of JavaScript are members of the window object.</p></td></tr><tr><td><p style="text-align:justify">We can access the document from a window using the window. document</p></td><td><p style="text-align:justify">We can access the window from the window only. i.e. window.window</p></td></tr><tr><td><p style="text-align:justify">The document is part of BOM (browser object model) and dom (Document object model)</p></td><td><p style="text-align:justify">The window is part of BOM, not DOM.</p></td></tr><tr><td><p style="text-align:justify">Properties of document objects such as title, body, cookies, etc can also be accessed by a window like this window. document.title</p></td><td><p style="text-align:justify">Properties of the window object cannot be accessed by the document object.</p></td></tr><tr><td><p>syntax:</p><p>&nbsp; &nbsp; &nbsp; document.propertyname;</p></td><td><p>syntax:</p><p>window.propertyname;</p></td></tr><tr><td><p>example:</p><p>&nbsp; &nbsp; &nbsp;document.title : &nbsp;will return the title of the document</p></td><td><p>example:</p><p>window.innerHeight : will return the height of the content area of the browser</p></td></tr></tbody></table>

##### Event Bubbling and Capturing

[EVENTS](https://javascript.info/events)
[UI EVENTS, Mice & Stuff](https://javascript.info/event-details)


When an event happens – the most nested element where it happens gets labeled as the “target element” (event.target).

- Then the event moves down from the document root to event.target, calling handlers assigned with addEventListener(..., true) on the way (true is a shorthand for {capture: true}).
- Then handlers are called on the target element itself.
- Then the event bubbles up from event.target to the root, calling handlers assigned using on<event>, HTML attributes and addEventListener without the 3rd argument or with the 3rd argument false/{capture:false}.

Each handler can access event object properties:

- **event.target** – the deepest element that originated the event.
- **event.currentTarget** (=this) – the current element that handles the event (the one that has the handler on it)
- **event.eventPhase** – the current phase (capturing=1, target=2, bubbling=3).

Any event handler can stop the event by calling **event.stopPropagation()**, but that’s not recommended, because we can’t really be sure we won’t need it above, maybe for completely different things.

The capturing phase is used very rarely, usually we handle events on bubbling.

![](https://y.yarn.co/3b84c43f-3096-4737-a2cb-05f8447b1d66_text.gif)
### DATA TRANSFER, REQUESTS

A **protocol** is a system of rules that define how data is exchanged within or between computers. Communications between devices require that the devices agree on the format of the data that is being exchanged. The set of rules that defines a format is called a protocol.

A ***network protocol*** is a set of established rules that dictate how to format, transmit and receive data so that computer network devices -- from servers and routers to endpoints -- can communicate, regardless of the differences in their underlying infrastructures, designs or standards.

To successfully send and receive information, devices on both sides of a communication exchange must accept and follow protocol conventions. In networking, support for protocols can be built into software, hardware or both.

#### HTTP

[OVERVIEW](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
[FETCH](https://web.dev/introduction-to-fetch/)

**HTTP** is a protocol for fetching resources such as HTML documents. It is the foundation of any data exchange on the Web and it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. A complete document is reconstructed from the different sub-documents fetched, for instance, text, layout description, images, videos, scripts, and more.

Clients and servers communicate by exchanging individual messages (as opposed to a stream of data). The messages sent by the client, usually a Web browser, are called ***requests*** and the messages sent by the server as an answer are called ***responses***.

 It is an application layer protocol that is sent over [TCP](https://developer.mozilla.org/en-US/docs/Glossary/TCP), or over a [TLS](https://developer.mozilla.org/en-US/docs/Glossary/TLS)-encrypted TCP connection, though any reliable transport protocol could theoretically be used. Due to its extensibility, it is used to not only fetch hypertext documents, but also images and videos or to post content to servers, like with HTML form results. HTTP can also be used to fetch parts of documents to update Web pages on demand.

<h5> HTTP vs. HTTPS </h5>
HTTPS is the use of Secure Sockets Layer (SSL) or Transport Layer Security (TLS) as a sublayer under regular HTTP application layering. HTTPS encrypts and decrypts user HTTP page requests as well as the pages that are returned by the web server. It also protects against eavesdropping and man-in-the-middle (MitM) attacks. HTTPS was developed by Netscape. Migrating from HTTP to HTTPS is considered beneficial, as it offers an added layer of security and trust.

##### Requests

![HTTP Request Anatomy](https://i.stack.imgur.com/n9Gwe.png)

- An **HTTP method**, usually a verb like GET, POST, or a noun like OPTIONS or HEAD that defines the operation the client wants to perform. Typically, a client wants to fetch a resource (using GET) or post the value of an HTML form (using POST), though more operations may be needed in other cases.
- The path of the resource to fetch; the URL of the resource stripped from elements that are obvious from the context, for example without the protocol (http://), the domain (here, developer.mozilla.org), or the TCP port (here, 80).
- The version of the HTTP protocol.
- Optional headers that convey additional information for the servers.
- A body, for some methods like POST, similar to those in responses, which contain the resource sent.


##### Responses

![HTTP Response Anatomy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_response.png)

- The version of the HTTP protocol they follow.
- A status code, indicating if the request was successful or not, and why.
- A status message, a non-authoritative short description of the status code.
- HTTP headers, like those for requests.
- Optionally, a body containing the fetched resource.

![HTTP Status Codes](https://kblinux.com/wp-content/uploads/2021/07/http-status-codes-1024x892.jpeg)

[STATUS CODES](https://www.restapitutorial.com/httpstatuscodes.html)


##### AJAX 

Ajax (also AJAX /ˈeɪdʒæks/; short for "Asynchronous JavaScript and XML") is a set of web development techniques that uses various web technologies on the client-side to create asynchronous web applications. With Ajax, web applications can send and retrieve data from a server asynchronously (in the background) without interfering with the display and behaviour of the existing page. By decoupling the data interchange layer from the presentation layer, Ajax allows web pages and, by extension, web applications, to change content dynamically without the need to reload the entire page. In practice, modern implementations commonly utilize JSON instead of XML.

Ajax is not a technology, but rather a programming concept.

![](https://www.w3schools.com/xml/ajax.gif)

#### fetch( )

![](https://i.pinimg.com/originals/60/a0/f1/60a0f10e9227fa654939884d40c2d8f3.gif)

**[BASICS](https://web.dev/introduction-to-fetch/)
[FETCH API DOCS](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)**

###### My lonely fetch request 🥺
```js
export const loadTrendingGifs = async (limit = 20, offset = 0) => {
  const API_URL = `https://api.giphy.com/v1/gifs/trending?api_key=${API_KEY_LM}&limit=${limit}&offset=${offset}&rating=g`;
  const response = await fetch(API_URL);

  if (!response.ok) {
    alert(`An error occurred: ${response.status}`);
  }
  return response.json();
};
```

[BLOBS](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

### API 

![](https://www.cleveroad.com/images/article-previews/40ca78a7a9db7adfb6bb861fc6b8910ae2ef4bb79f5508007d166f01df5c1038.png)

**[WHAT's an API](https://www.cleveroad.com/blog/what-is-an-api/)
[RESTfulness](https://restfulapi.net/)**

#### URL

![](https://blog.hubspot.com/hs-fs/hubfs/Parts%20of%20a%20URL.png?width=650&name=Parts%20of%20a%20URL.png)

A Uniform Resource Locator (URL), colloquially termed a web address, is a reference to a web resource that specifies its location on a computer network and a mechanism for retrieving it. A URL is a specific type of Uniform Resource Identifier ([URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)), although many people use the two terms interchangeably. URLs occur most commonly to reference web pages (HTTP) but are also used for file transfer (FTP), email (mailto), database access (JDBC), and many other applications.

A URL is nothing more than the address of a given unique resource on the Web. In theory, each valid URL points to a unique resource. Such resources can be an HTML page, a CSS document, an image, etc. In practice, there are some exceptions, the most common being a URL pointing to a resource that no longer exists or that has moved. As the resource represented by the URL and the URL itself are handled by the Web server, it is up to the owner of the web server to carefully manage that resource and its associated URL.

![](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)

**[MDN DEETS](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)**

![](https://danielmiessler.com/images/url-structure-and-scheme-2022.png)

