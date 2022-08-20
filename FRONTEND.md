# <h1 align="center"> FRONT END ❤️ (as read by Liya) </h1>

### SPAs & MPAs

A **single-page application** is an app that works inside a browser and does not require page reloading during use. You are using this type of applications every day. These are, for instance: Gmail, Google Maps, Facebook or GitHub.
SPAs are all about serving an outstanding UX by trying to imitate a “natural” environment in the browser — no page reloads, no extra wait time. It is just one web page that you visit which then loads all other content using JavaScript — which they heavily depend on.

SPA requests the markup and data independently and renders pages straight in the browser.

##### Advantages of single page application
- *Speed and Response Time:* Whenever you click on a tab, SPAs do not load the entire content. Rather, it takes a particular request data to the service and acts. The server can load various resources like scripts, CSS, and HTML at the same time.

- *Mobile-friendly:* The majority of online traffic comes from mobile users. SPAs pattern shares a similar interest. Frameworks used for SPA development help you to create mobile apps and simplifies the reuse of codes.

- *Makes A Website Engaging and Unique:* Single-page applications are attractive. It provides a linear experience to users.

- *Better Conversions:* With the single-page application, its user-friendliness and simplicity, you can do it better. Web pages with less loading time ensure better conversion.

##### Disadvantages of single page application
- *Poor SEO:* SEO is the single major disadvantage of a single-page application. It is better to have a single web app with steady content and separate pages. However, it is not a major problem for a web application development team.

- _Security Issues:_ Cross-site scripting is another major problem area due to security problems. In such cases, attackers try to take advantage of the vulnerabilities of a site and client site code.

- *Scalability:* Single-page application is not scalable. Load time increases the instant more content is added to the page.

- *Browser History:* A single-page application does not save jumping stages. The back button leads users to the previous page instead of the previous stage of the SPA.

**Multiple-page applications** work in a “traditional” way. Every change eg. display the data or submit data back to server requests rendering a new page from the server in the browser. These applications are large, bigger than SPAs because they need to be. Due to the amount of content, these applications have many levels of UI. Thanks to AJAX, we don’t have to worry that big and complex applications have to transfer a lot of data between server and browser. That solution improves and it allows to refresh only particular parts of the application. On the other hand, it adds more complexity and it is more difficult to develop than a single-page application.



##### Advantages of Multi page Applications
- *SEO-friendly:* The best way is to apply multi-page application. Mobile and web application development enterprises desire for their service page on the first page of a search engine.

- *Scalability:* Multi-page application have multiple pages. You can add as many pages to a website as you want. You can also add new pages for a new product without any limitations.

- *Easy to Analyze:* MPAs allow easy integration with Google Analytics. It is necessary for valuable information about your visitors coming to the page.

##### Disadvantages of Multi page Applications
- *Slower:* Unlike single-page apps, multi-page apps are slower. It reloads every time users click on a tab. Resources such as CSS, HTML, and Script refreshes when there is an action. As a result, speed and performance are affected.

- *It Takes More Time to Develop:* Coders start coding right from scratch for frontend as well as backend. Moreover, there may be some difficulties in frontend and backend separation. Programmers should utilize frameworks too. Hence, it takes more time to develop.

- *Security and Maintenance:* It is difficult to maintain and update a website constantly. It also becomes difficult, as the website looks clumsy. Developers have to ensure that every page is secure, which is challenging. Hence, it is a cumbersome process.

### React

React is an open-source JavaScript library used for building high-quality user interfaces for web apps.
The library allows developers to create large web applications that can change data, without reloading the page. It can be used in a combination of other JavaScript libraries or frameworks. 

- React creates a VIRTUAL DOM in memory.

- Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.

- React finds out what changes have been made, and changes only what needs to be changed.

##### The Virtual DOM

The DOM represents the UI of the application, and if there is a change, the DOM is updated to represent the change. If this is a frequent action, it can affect the performance of the app. This is where the Virtual DOM comes in. 

Basically, it is an in-memory representation of the actual elements that are being created for your page. Every time the state of our application changes, the virtual DOM gets updated instead of the real DOM. Long story short, the virtual DOM then calculates the best possible method to transfer the changes to the DOM. Hence, reducing the load of the update.

1. The entire virtual DOM gets updated.
2. The virtual DOM gets compared to what it looked like before you updated it. React figures out which objects have changed.
3. The changed objects, and the changed objects only, get updated on the real DOM.
4. Changes on the real DOM cause the screen to change.

[DOM vs. VDOM](https://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/)

##### JSX

- JSX stands for JavaScript XML.
- JSX allows us to write HTML in React.
- JSX makes it easier to write and add HTML in React.
- JSX converts HTML tags into react elements.
- JSX is an extension of the JavaScript language based on ES6, and is translated into regular JavaScript at runtime.
- With JSX you can write expressions inside curly braces `{ }`.
- - JSX expressions become regular JavaScript function calls and evaluate to JavaScript objects.This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions
- To write HTML on multiple lines, put the HTML inside parentheses: One parent element, please...
- you can use a "fragment" to wrap multiple lines. This will prevent unnecessarily adding extra nodes to the DOM. A fragment looks like an empty HTML tag: `<></>`.
- class = className
- React supports if statements, but not inside JSX.
###### React doesn’t require using JSX
Conditional statements -> result inside JSX || ternary directly in JSX

#### Rendering to the DOM

Applications built with just React usually have a single root DOM node. If you are integrating React into an existing app, you may have as many isolated root DOM nodes as you like.

To render a React element, first pass the DOM element to `ReactDOM.createRoot()`, then pass the React element to `root.render()`:

```js
const root = ReactDOM.createRoot(
  document.getElementById('root')
);
const element = <h1>Hello, world</h1>;
root.render(element);
```

#### Components, Props 'n' Stuff

##### Functional Components:

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
```js
function Welcome({name, age, occupation}) {
  return <h1>Hello, {name}</h1>;
}
```
**All React components must act like pure functions with respect to their props.**
##### Class Components:

```js
class Democomponent extends React.Component
{
    render(){
          return <h1>Welcome Message!</h1>;
    }
}
```
##### Converting a Function to a Class
You can convert a function component like Clock to a class in five steps:

1. Create an ES6 class, with the same name, that extends `React.Component`.
2. Add a single empty method to it called `render()`.
3. Move the body of the function into the `render()` method.
4. Replace `props` with `this.props` in the `render()` body.
5. Delete the remaining empty function declaration.

```js
class Welcome extends React.Component {
  render() {
          return <h1>Hello, {this.props.name}</h1>;
    }
}
```

Local state:
```js
class Welcome extends React.Component {
    constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
  render() {
          return <h1>Hello, {this.props.name}</h1>;
    }
}
```
#### state and props
**props (short for “properties”)** and **state** are both plain JavaScript objects. While both hold information that influences the output of render, they are different in one important way: `props` get passed to the component (similar to function parameters) whereas `state` is managed within the component (similar to variables declared within a function).

###### Component types:
- **Stateless Component** — Only props, no state. There's not much going on besides the render() function and all their logic revolves around the props they receive. This makes them very easy to follow (and test for that matter). We sometimes call these dumb-as-f*ck Components (which turns out to be the only way to misuse the F-word in the English language).
- **Stateful Component** — Both props and state. We also call these state managers. They are in charge of client-server communication (XHR, web sockets, etc.), processing data and responding to user events. These sort of logistics should be encapsulated in a moderate number of Stateful Components, while all visualization and formatting logic should move downstream into as many Stateless Components as possible.

[state vs. props](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md)

##### `props.children`

```js
function HasChildren(props) {
  return (
    <div className={className + props.color}>
      {props.children}
    </div>
  );
}
```

```js
function TheChildrenResideHere() {
  return (
    <HasChildren color="blue">
      <h1 className="kid1">
        CHILD
      </h1>
      <p className="kid2">
        CHILD
      </p>
    </HasChildren>
  );
}
```
##### Typechecking With PropTypes

- https://www.npmjs.com/package/prop-types
```js
import PropTypes from 'prop-types'

function HelloWorldComponent({ name }) {
  return (
    <div>Hello, {name}</div>
  )
}

HelloWorldComponent.propTypes = {
  name: PropTypes.string
}

export default HelloWorldComponent
```

#### HOOKS

**What is a Hook?** A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components. We’ll learn other Hooks later.

**When would I use a Hook?** If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component.

![](https://media1.giphy.com/media/tYAolvs3tZIhG/giphy.gif)

#### `useState`

**What does calling useState do?** It declares a “state variable”. This is a way to “preserve” some values between the function calls — `useState` is a new way to use the exact same capabilities that `this.state` provides in a class. *Normally, variables “disappear” when the function exits but state variables are preserved by React.*

**What do we pass to useState as an argument?** The only argument to the useState() Hook is the initial state. Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need. In our example, we just want a number for how many times the user clicked, so pass 0 as initial state for our variable. (If we wanted to store two different values in state, we would call `useState()` twice.)

**What does useState return?** It returns a pair of values: the current state and a function that updates it. This is why we write `const [count, setCount] = useState();`

**[KEYS](https://adhithiravi.medium.com/why-do-i-need-keys-in-react-lists-dbb522188bbb)**

- identity
- unique only among siblings

#### `useEffect`

The **Effect Hook** lets you perform side effects in function components

**What does `useEffect` do?** By using this Hook, you tell React that your component needs to do something after render. React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates.

**Why is `useEffect` called inside a component?** Placing `useEffect` inside the component lets us access state variables (or any props) right from the effect. We don’t need a special API to read it — it’s already in the function scope. Hooks embrace JavaScript closures and avoid introducing React-specific APIs where JavaScript already provides a solution.

**Does `useEffect` run after every render?** Yes! By default, it runs both after the first render and after every update. Instead of thinking in terms of “mounting” and “updating”, you might find it easier to think that effects happen “after render”. React guarantees the DOM has been updated by the time it runs the effects.

##### Clean-up

Code for adding and removing a subscription is so tightly related that `useEffect` is designed to keep it together. If your effect returns a function, React will run it when it is time to clean up

```js
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
**Why did we return a function from our effect?** This is the optional cleanup mechanism for effects. Every effect may return a function that cleans up after it. This lets us keep the logic for adding and removing subscriptions close to each other.

**When exactly does React clean up an effect?** React performs the cleanup when the component unmounts. However, as we learned earlier, effects run for every render and not just once. This is why React also cleans up effects from the previous render before running the effects next time. 

###### The Dependency Array:

You can tell React to skip applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to `useEffect`:

```js
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Only re-subscribe if props.friend.id changes i.e for different friends
```
-----------------------------------------------------
[SMART & DUMB COMPONENTS](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)

### Routing

##### Client & Server Side Routing

<div class="s-prose js-post-body" itemprop="text">
<p>tl;dr:</p>

<ul>
<li>with server-side routing you download an entire new webpage whenever you click on a link,</li>
<li>with client-side routing the webapp downloads, processes and displays new data for you.</li>
</ul>

<hr>

<p>Imagine the user clicking on a simple link:  <code>&lt;a href="/hello"&gt;Hello!&lt;/a&gt;</code></p>

<p>On a webapp that uses <strong>server side routing</strong>:</p>

<ul>
<li>The browser detects that the user has clicked on an anchor element.</li>
<li>It makes an HTTP GET request to the URL found in the <code>href</code> tag</li>
<li>The server processes the request, and sends a new document (usually HTML) as a response.</li>
<li>The browser discards the old webpage altogether, and displays the newly downloaded one.</li>
</ul>

<p>If the webapp uses <strong>client side routing</strong>:</p>

<ul>
<li>The browser detects that the user has clicked on an anchor element, just like before.</li>
<li>A client side code (usually the routing library) catches this event, detects that the URL is not an external link, and then <strong>prevents the browser</strong> from making the HTTP GET request. </li>
<li>The routing library then <strong>manually changes the URL</strong> displayed in the browser (using the HTML5 history API, or maybe URL hashbangs on older browsers)</li>
<li>The routing library then <strong>changes the state of the client app</strong>. For example, it can change the root React/Angular/etc component according to the route rules.</li>
<li>The app (particularly the MVC library, like React) then processes state changes. It renders the new components, and if necessary, it requests new data from the server. But this time the response isn't necessarily an entire webpage, it may also be "raw" data, in which case the client-side code turns it into HTML elements.</li>
</ul>

<p>Client-side routing sound more complicated, because it is. But some libraries really make it easy these days.</p>

<p>There are several upsides of client-side routing: you download less data to display new content, you can reuse DOM elements, display loading notifications to user etc. However, webapps that generate the DOM on server side are much easier to crawl (by search engines), thereby making SEO optimization easier. Combining these two approaches is also possible, the excellent <a href="https://github.com/kadirahq/flow-router/tree/ssr">Flow Router SSR</a> is a good example for that.</p>
</div>

[REACT ROUTER](https://reactrouter.com/docs/en/v6/getting-started/overview)

### AUTHENTICATION
**What is authentication?**
Authentication is the process of determining whether someone or something is, in fact, who or what it says it is. Authentication technology provides access control for systems by checking to see if a user's credentials match the credentials in a database of authorized users or in a data authentication server. In doing this, authentication assures secure systems, secure processes and enterprise information security.

There are several authentication types. For purposes of user identity, users are typically identified with a user ID, and authentication occurs when the user provides credentials such as a password that matches their user ID. The practice of requiring a user ID and password is known as single-factor authentication (SFA). In recent years, companies have strengthened authentication by asking for additional authentication factors, such as a unique code that is provided to a user over a mobile device when a sign-on is attempted or a biometric signature, like a facial scan or thumbprint. This is known as two-factor authentication (2FA).

Once authenticated, a user or process is usually subjected to an authorization process to determine whether the authenticated entity should be permitted access to a specific protected resource or system. A user can be authenticated but not be given access to a specific resource if that user was not granted permission to access it.

The terms authentication and *authorization* are often used interchangeably. While they are often implemented together, they are two distinct functions. Authentication is the process of validating the identity of a registered user or process before enabling access to protected networks and systems. 

Authorization is a more granular process that validates that the authenticated user or process has been granted permission to gain access to the specific resource that has been requested. The process by which access to those resources is restricted to a certain number of users is called access control. The authentication process always comes before the authorization process.

[AUTH & AUTH](https://www.loginradius.com/blog/identity/authentication-vs-authorization-infographic/)
[REACT AUTH](https://betterprogramming.pub/building-basic-react-authentication-e20a574d5e71)

###### In React

[create/useContext](https://www.bradcypert.com/react-usecontext-hook/)
[solving prop drilling](https://blog.logrocket.com/solving-prop-drilling-react-apps/)

```js
export default function Authenticated({ children }) {
  const { appState } = useContext(AppState);
  const location = useLocation();

  if (!appState.user) {
    return <Navigate to="/login" state={{ from: location.pathname }} />;
  }

  return children;
}
```

---------------------

- A **Controlled Component** is one that takes its current value through props and notifies changes through callbacks like onChange. A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a "dumb component".
- An **Uncontrolled Component** is one that stores its own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.



**[Why React re-renders](https://www.joshwcomeau.com/react/why-react-re-renders/)**
**[How React Works](https://www.youtube.com/watch?v=mLMfx8BEt8g&list=LL&index=1&t=36s)**
