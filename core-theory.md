 # <h1 align="center"> JavaScript ❤️ Basic Theory (as read by Liya) </h1>

 JavaScript (often shortened to JS) is a lightweight, interpreted, object-oriented language with first-class functions, and is best known as the scripting language for Web pages, but it's used in many non-browser environments as well. It is a prototype-based, multi-paradigm scripting language that is dynamic, and supports object-oriented, imperative, and functional programming styles.

 JavaScript runs on the client side of the web, which can be used to design / program how the web pages behave on the occurrence of an event. JavaScript is an easy to learn and also powerful scripting language, widely used for controlling web page behavior.

 - First-class Function
A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.

## JS Core Theoretical Prep
### Loops:
#### Definition: 

A loop is a statement that repeats a set of actions until a given condition fails - becomes false.
#### Types of loops:

##### for loop:
```
for ([initialExpression]; [conditionExpression]; [incrementExpression]) {
  statement/s
}
```

- the initial expression will usually define a counter variable to serve as basis of the loop
- then the condition expression will evaluate to true of false: if it's true the loop will go on otherwise it will terminate (if omitted - evaluates to true)
- if the condition expression is true, the statement/s will execute
- the increment expression will execute if it exists 
- for the next iteration the condition expression is evaluated again and so on.

##### for-of loop:

A for-of loop is used to iterate over iterables (basically something that can be ordered according to the way natural numbers are ordered), it iterates over the property values, and executes the given statement/s for each value
```
for (variable of object) {
  statement/s
}
```

- it will iterate over an array and return its items
- it will iterate over a string and return its characters
- it will iterate over sets and maps and other stuff I don't know well enough for now

##### for-in loop:

A for-in loop is used to iterate over the enumerable properties of an object (basically something that cannot be ordered), it gets the properties themselves (the keys, not the values) and executes the given statement/s for each property

```
for (variable in object) {
  statement/s
}
```

- when I've made mistakes and used it on arrays/strings it returns the indexes but it seems it can get other properties too and be somewhat unpredictable like that

##### while loop:

A while statement will execute its statements over and over as long as the given condition/s are true; If the condition evaluates to false the loop will stop 

```
while (condition) {
  statement/s
}
```

##### do-while loop:

Behaves pretty much as the while loops behave but will execute once no matter the condition since the condition is evaluated after the do statement/block

```
do {
  statement/s
} while (condition);
```

##### break statement:

- break without a label will terminate the while, do-while, for, or switch statement that's wrapped around it immediately and will control to the following indipendent statement

- break with label will terminate the labeled statement, not necessarily the one it lives in 

###### break;
```
while (hair === long) {
    braid hair;
    if (hair !== long) {
        break;
    }
}
```

###### break [label];
```
stopVanityLoop: while (vanity in liya) {
    console.log('Mirror, mirror on the wall...')
    while (hair === long) {
        braid hair;
        if (hair !== long) {
            break;
        }
        if (!(vanity in liya)) {
            console.log('The witch is dead.');
            break stopVanityLoop;
        }
    }
}
```

##### continue statement:

The continue statement will skip the current iteration according to a given condition and the loop will move on to the next one. Can be used with a label like the break statement. I wish I'd learned that sooner. Welp.
```
const theHigh6 = ['Rumi', 'Tedi', 'Liya', 'Bobi', 'Velko', 'Misho'];
const people = ['Tedi', 'Misho', 'Pesho', 'Bobi'];

for (const name of people) {
   if (!theHigh6.includes(name)) {
      continue;
    }
  console.log(''Give candy to ${name}'');
}
```
### Arrays:
#### Definition: 

An array is an object that stores an `ordered` collection of data: it holds values (of any type and heterogeneously) not in named properties/keys, but rather in numerically indexed positions. 

An array can help us store many values as a single variable instead of creating a bazillion of indipended variables which can become unmanageable quickly. It also allows us to manipulate and retrieve its contents systematically. 

###### literal creation
```
const theHigh6 = ['Rumi', 'Tedi', 'Liya', 'Bobi', 'Velko', 'Misho'];
```
###### new creation

- The new Array() constructor creates a new Array instance from a variable number of arguments,
```
const theHigh6 = new Array('Rumi', 'Tedi', 'Liya', 'Bobi', 'Velko', 'Misho')
 // same result as the literal 
```
- unless it's a number, then it will use it as the length for the array
```
const the6 = new Array(6) // array of 6 empty slots
```

###### array methods creation
- The Array.of() method creates a new Array instance from a variable number of arguments
```
const one6 = Array.of(6); // [6]
```

- The Array.from() static method creates a new, shallow-copied Array instance from an array-like or iterable object.
```
const nameHigh6 = Array.from('thehigh6') // ['t','h','e','h','i','g','h','6'];
```

### Functions:
#### Definition:

A function is a block of code that that performs a task or calculates a value; It should take some input (as parameters) and return an output where there is some obvious relationship between the input and the output. To return a value other than the default (funcs without return statement return undefined), a function must have a return statement that specifies the value to return.

##### Function declaration:
A function definition (also called a function declaration, or function statement) consists of the function keyword, followed by:

 - The name of the function.
 - A list of parameters to the function, enclosed in parentheses and separated by commas.
 - The JavaScript statements that define the function, enclosed in curly brackets, {...}.

```
function explainCoding(topic, explanation) {
    return `A/An ${topic} ${explanation};
}

const explained = explainCoding('array', 'is an object containing ordered values');
// ^^^ assigning the return value of a function called with given arguments to a variable 
```
- function declarations are hoisted in their entirety; You can call them from above... 
##### Function expression:

The function keyword can be used to define a function inside an expression. 

```
const funcExpress = function(a, b) {
    return a + b
}
const result = funcExpress(1, 2); // calling the function
```
Basically assigning the function to a variable. The function name can be omitted as the variable will act as a name. *(Search for Named Function Expression for info why you'd need a name)*
- Unlike the function declaration in this case the definiton of the function will not be hoisted to the top 

##### Arrow function: 

An arrow function expression is a compact alternative to a traditional function expression, but has certain limitations and can't be used in all situations.

- One param. With simple expression return is not needed:
```
const arr = [1, 2, 3];
const doubleIT = a => a * 2; // single-line arrow function to be used as a callback in map();
const doubledValues = arr.map(doubleIT);
```
- Multiple params require parentheses. With simple expression return is not needed:

```
const sumAgain = (a, b) => a + b
```

- Multiline statements require body braces and return:

```
const arr = [6, 5, 6, 5, 6];
const multiplying = (acc, el) =>{
    if (el > 5) {
      acc= acc * el;
    } else if (el === 5) {
      acc = acc / el;
    }
    return acc;
  };
  const test2 = arr.reduce(multiplying);
```
**~** Do whachu will with this: *The single-responsibility principle (SRP) is a computer-programming principle that states that every module, class or function in a computer program should have responsibility over a single part of that program's functionality, and it should encapsulate that part. All of that module, class or function's services should be narrowly aligned with that responsibility.*

##### **IIFEs** Immediately Invoked Function Expressions:
IIFE's are function expressions that are called immediately and only once, and cannot be called again. They're used so as to not pollute the global scope. 

- IIFE with function declaration syntax (wrapped in parens to be treated as an expression):
```
(function() {
  /* */
})()
```
- IIFE with arrow function syntax:
```
const ArrowIIFE = (() => {
  /* */
})()
\\ the return value will be assigned to the variable instead of the function itself
```

### Exceptions:
#### Definition:

When the code runs into an unexpected problem, the JavaScript idiomatic way to handle this situation is through exceptions. The code will stop its execution and an error message will be printed according to the specifics of the encountered error. 

##### throw statement:

```
function sum(a, b){
    if (isNaN(a) || isNaN(b)) {
        throw 'Parameter is not a valid number';
    } 
    return a * b
}
console.log(sum(2, 'dasd')) 
```
##### Exception handling: try, catch, finally
- **try block**: contains the statements we want to be executed if everything goes well
- **catch block**: specifies the handling of any exceptions thrown during the try block execution
- **finally block**: contains statements to be executed no matter the result of the `try` and `catch` blocks 
```

function jibbleObject(obj){
  try {
  obj.name = 'lily'
  return obj.name
  }
  catch (err) {
    console.log(err.message);
  } finally {
    console.log('Returns object name');
  }
  
}

console.log(jibbleObject());
console.log(jibbleObject({type: 'flower'}));
```
**\*** a return statement in the finally block will act as the default return and will override returns in the `try` and `catch`

### NPM (Node Package Manager): 
#### Definition: 
https://www.npmjs.com/

- npm is the package manager for Node.js
- The npm Registry is a public collection of packages of open-source code
- npm is the command line client that allows developers to install and publish those packages

NPM allows us to use external modules thus relieving us from the need to personally write every functionality we might need every time we need it 
##### Installing npm and modules:
0. Open a terminal in the directory you will use for the project. 
1. Installing NPM; If we have Node we already have npm
2. We need to initialize a project and save its information (name, version, description, dependencies etc.) in a package.json file
If you want to put in the info manually:
```
npm init
```
For auto-complete: 
```
npm init -y
```
3. After that we can install any package and save it as a dependency for the project by writing: 
```
npm install <pkg>
```
Adding as a dev-dependency: 
```
npm install <pkg> -D
```
A finished project can be sent anywhere (without the node_modules folder) and can be run with:
```
npm install
``` 
\* to be run in the folder where package.json resides since it will look up the info in the file to install the correct packages

##### Importing from a module in a file:

###### Named export/import

someFile.js has:
```
export const aThing = 'A thing is here.'
export function someFunc() {
    let a = 4;
    return a
}
```
the exports of someFile.js can be imported in several ways: 
```
import {aThing, someFunc} from 'someFile';
let res = someFunc();

```
```
import * as someStuff from './someFile.js'
let res = someStuff.someFunc();
```
###### Default export/import
You can have only one default per module.

```
export const aThing = 'A thing is here.'
export function someFunc() {
    let a = 4;
    return a
}
export default function loggin(sth) {
    console.log(`${sth} is logged.`)
}
```
```
import defaultFunc, {namedExp...} from 'path'
```
##### Modules:

Modules give you a better way to organize variables and functions. With modules, you group the variables and functions that make sense to go together.
The ES module format was created to standardize the JavaScript module system. It has become the standard format for encapsulating JavaScript code for reuse.
**CommonJS is the default module standart for Node.js. To use ES Modules you need to specify it in the package file.**
CommonJS imports are dynamically resolved at runtime. The require() function is simply run at the time our code executes. As a consequence, you can call it everywhere in your code.

With ES Modules, imports are static, which means they are executed at parse time. This is why imports are “hoisted”. They are implicitly moved to the top of the file. Therefore, we cannot use the import syntax we have seen above just in the middle of your code.

#### ECMAScript / ESNext / ESLint

**ECMAScript** is a JavaScript standard meant to ensure the interoperability of web pages across different web browsers. It is standardized by Ecma International according to the document ECMA-262. ECMAScript is commonly used for client-side scripting on the World Wide Web, and it is increasingly being used for writing server applications and services using Node.js. 

##### Static Analysis Tools / Linters

- Static code analysis is the process of analyzing code before it is executed. It is the automated equivalent to another developer reading and reviewing your code, except with the added efficiency, speed, and consistency afforded by a computer that no human could match.
- Static code analysis analyses its aspects such as readability, consistency, error handling, type checking, and alignment with best practices. Static analysis is not primarily concerned with whether your code provides the expected output but rather with how the code itself is written. It's an analysis of the quality of source code, not its functionality.

![Alt text](https://i.redd.it/uwc7cddddcp51.png "a title")

- Most static analyzers, especially linters and formatters, will not just point out issues but can also fix most of them for you. Linters like Black for Python and ESLint for JavaScript integrate with IDEs and can then automatically fix the edited files as soon as you save them.

##### Installing ESLint:
```
npm install eslint --save-dev
```
Configuration of the file containing the "rules" for the code in the project: 
```
npm init @eslint/config
```
\* must have a package.json to configure eslint 

After that, you can run ESLint on any file or directory like this:
```
npx eslint yourfile.js
```
Fixing found errors:
```
eslint --fix file.js
```

#### Git / GitLab / GitHub:
**Git** is software for tracking changes in any set of files, usually used for coordinating work among programmers collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows (thousands of parallel branches running on different systems);

![Alt text](https://git-scm.com/book/en/v2/images/areas.png "a title")

The basic Git workflow goes something like this:

1. You modify files in your working tree.

2. You selectively stage just those changes you want to be part of your next commit, which adds only those changes to the staging area.

3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

`git commit` creates a commit, which is like a snapshot of your repository. These commits are snapshots of your entire repository at specific times. You should make new commits often, based around logical units of change. Over time, commits should tell a story of the history of your repository and how it came to be the way that it currently is. Commits include lots of metadata in addition to the contents and message, like the author, timestamp, and more.
```
git commit -m "wibbly wobbly timey wimey stuff added"
```
- The "commit" command is used to save your changes to the local repository.
```
git push
```
- The git push command is used to upload local repository content to a remote repository.

###### GitLab
- GitLab is a web-based Git repository that provides free open and private repositories, issue-following capabilities, and wikis. 

### Objects ('n Ghosts 'n Stuff)

#### Types: Primitives and References

##### Primitive types: null, undefined, boolean, number, string, symbol
- Primitives are known as being immutable data types because there is no way to change a primitive value once it gets created.
- Primitives are compared by value. Two values are strictly equal if they have the same value.
```
let num1 = 6;
let num2 = 8;

console.log(num1 === num2); // false

num1 = 8;

console.log(num1 === num2); // true

let str1 = 'That's not my name'
str1[2] = 'o';
let str2 = 'That's not my name'

console.log(str1); // 'That's not my name'
console.log(str1 === str2); // true
```
##### Reference types: well, object (objects and arrays)

- Non-primitive values are mutable data types. The values of (or rather inside) an object can be changed after it gets created.

```
let myArr = [3, 4, 6, 8];
myArr[0] = 2;
console.log(myArr); // [2, 4, 6, 8]
```
- Objects are not compared by value. This means that even if two objects have the same properties and values, they are not strictly equal. Same goes for arrays. Even if they have the same elements that are in the same order, they are not strictly equal. 


```
const obj1 = { 'name': 'Sunny' };
const obj2 = { 'name': 'Sunny' };
console.log(obj1 === obj2);  // false

const arr1 = [ 1, 2, 3, 4, 5 ];
const arr2 = [ 1, 2, 3, 4, 5 ];
console.log(arr1 === arr2);  // false
```

- Non primitive values can also be referred to as reference types because they are being compared by reference instead of value. Two objects are only strictly equal if they refer to the same underlying object. 

Like this:
```
const object1 = {who: 'Me', when: 'Then'};
const object2 = object1;

console.log(object1 === object2) // true 
```

The **Object** class represents one of JavaScript's data types. It is used to store various keyed collections and more complex entities. Objects store data in the form of key - value pairs. You can retrieve and modify information stored in an object by using its existing properties and creating new properties. We use objects when it's logically consistent to bind the data to certain names and not order it numerically.

```
const self = {
    name: 'Liya',
    birthday: {
        day: 24,
        month: '',
        year: 1998
    },
    skills: null,
    haircolour: 'dark brown',
    eyecolour: 'green' 
}
```
#### Copying an object: reference, shallow & deep copy

1. Reference copy - will point to the same object in the memory:
```
const self = {
    name: 'Liya',
    birthday: {
        day: 24,
        month: '',
        year: 1998
    },
    skills: null,
    haircolour: 'dark brown',
    eyecolour: 'green' 
}

const doppelganger = self;
doppelganger.haircolour = 'blonde';

console.log(self.haircolour); // 'blonde'
```
2. Shallow copy - primitive types inside the object will be copied by value but the references inside will be copied by reference 

```
const self = {
    name: 'Liya',
    birthday: {
        day: 24,
        month: '',
        year: 1998
    },
    skills: null,
    haircolour: 'dark brown',
    eyecolour: 'green' 
}

const doppelganger = {...self};// || const doppelganger = Object.assign({}, self);

doppelganger.haircolour = 'blonde';
console.log(self.haircolour); // 'dark brown'

doppelganger.birthday.day = 28;
console.log(self.birthday.day); //28
```
3. Deep copy - all values inside the object are disconnected from the original, reference types will have other references

```
const self = {
  name: 'Liya',
  birthday: {
      day: 24,
      month: '',
      year: 1998
  },
  skills: null,
  haircolour: 'dark brown',
  eyecolour: 'green' 
}

function copyInDepth(data) {
  let newObject = {};

  for (let entry of Object.entries(data)) {
    if (entry[1] === null || entry[1] === undefined) {
      if (entry[1] === null) {
        newObject[entry[0]] = null;
      }
      if (entry[1] === undefined) {
        newObject[entry[0]] = undefined;
      }
    } else {
      if (typeof entry[1] !== "object") {
        newObject[entry[0]] = entry[1];
      } else {
        newObject[entry[0]] = copyInDepth(entry[1]);
      }
    }
  }

  return newObject;
}

const doppelganger = copyInDepth(self);
doppelganger.birthday.day = 28;

console.log(doppelganger.birthday.day); //28
console.log(self.birthday.day); //24

```
\* one option is to create a function that copies recursively if it encounters an object

- More ready-to-go methods: 

```
const doppelganger = JSON.parse(JSON.stringify(self)); 
```
```
// Using lodash
const doppelganger = _.cloneDeep(self);
```
##### Destructuring objects 

```
const numArray = [2, 3, 4, 5, 6, 7];
let a, restOfArr;
[a, ...restOfArr] = numArray;
// a = 2;
// restOfArr = [3, 4, 5, 6, 7];

let [m, , n, , o] = numArray;
console.log(m, n, o) // 2 4 6
```

```
const self = {
  name: 'Liya',
  birthday: {
      day: 24,
      month: '',
      year: 1998
  },
  skills: null,
  haircolour: 'dark brown',
  eyecolour: 'green' 
}

let {name, eyecolour} = self;
console.log(`${name} has ${eyecolour} eyes.`); // Liya has green eyes.
```
#### this.thing

```
const stranger1 = {
  name: 'Steve'
};
const stranger2 = {name: 'Dave'};

function getName() {
  console.log('Speak your name, stranger!');
  console.log(`My name is ${this.name}`);
}

stranger1.speak = getName;
stranger2.speak = getName;

stranger1.speak()
/* Speak your name, stranger!
My name is Steve */
stranger2.speak()
/* Speak your name, stranger!
My name is Dave */
```
The value of `this` is the object “before dot”, the one used to call the method (**object method**: a function that is a property of an object).
- In JavaScript, keyword this behaves unlike most other programming languages. It can be used in any function, even if it’s not a method of an object.
- The value of this is evaluated during the run-time, depending on the context.
- In the example above the same function is assigned to two different objects and has different “this” in the calls

#### Linked Lists

A **linked list** is a linear collection of data elements whose order is not given by their physical placement in memory. Instead, each element points to the next. It is a data structure consisting of a collection of nodes which together represent a sequence. In its most basic form, each node contains: data, and a reference (in other words, a link) to the next node in the sequence. This structure allows for efficient insertion or removal of elements from any position in the sequence during iteration. 

\+ Nodes can easily be removed or added from a linked list without reorganizing the entire data structure. 

\- Search operations are slow in linked lists. Unlike arrays, random access of data elements is not allowed. Nodes are accessed sequentially starting from the first node.  

![Alt text](https://pbs.twimg.com/media/FQWxavtUYAk2vsT.jpg "a title")

###### Creating linked list from array

```
function toLinkedList (array) {
    let list = {};
    let c = 0;

    while (c <= array.length) {
        list['value'] = array[c];
        array.shift()
        
        if (c === array.length) {
            list['next'] = null;
        } else list['next'] = toLinkedList(array);
        c++;
    }
    
    return list;
}
const linkedList = toLinkedList([8, 12, -31, 8, 6]);
//console.log(linkedList);

//---------------------------------------------------------\\

function toLinkedNoRec (array) {
    let link = {};
    let list = null;

    for (let i = array.length-1; i >= 0; i--) {
        link = {value: array[i], next: list};
        list = link;
    };
    return list;
}

const linkedList1 = toLinkedNoRec([8, 12, -31, 8, 6]);
console.log(linkedList1); // { value: 8, next: { value: 12, next: { value: -31, next: [Object] } } }
```
##### Search for a value in linked list
```
function find (linkedList, value) {
    let valueFound = false;
    let list = linkedList
    while (true) {
        if (list.value === value) {
            valueFound = true;
            break;
        }
        if (list.next === null) {
            if (list.value === value) {
                valueFound = true;
                break;
            }
            break;
        }
        list = list.next;
    }  
    
    return valueFound;
}

const linkedList2 = toLinkedList(['pesho', 'gosho', 'tosho']);
const linkedList3 = toLinkedNoRec(['pesho', 'gosho', 'tosho']);
// console.log(`${find(linkedList2, 'lily')}, Lily's not here`); // false
// console.log(`${find(linkedList2, 'pesho')}, Pesho's here`); // true
```
##### From LL to Array

```
function arrayIT (linkedList) {
    let LLArr = [];
    let list = linkedList
    while (true) {
        LLArr.push(list.value)
        list = list.next;
        if(list.next === null) {
            LLArr.push(list.value)
            break;
        }
    } 
    return LLArr;
}
console.log(arrayIT(linkedList2));
// code above needed
```
### Scope & Closure

#### Scope

- Scope is the set of rules that determines where and how a variable (identifier) can be looked-up. This look-up may be for the purposes of assigning to the variable, which is an LHS (left-hand-side) reference, or it may be for the purposes of retrieving its value, which is an RHS (right-hand-side) reference. 

In other words the scope is the field where the variable is discoverable. 

`let:`
- variables declared with let will be discoverable only inside the block in which they're declared OR in the blocks inside the block; Same goes for `const` with the difference being that the `const`-`s` cannot be reassigned. 

**`let` and `const` have block-scope**

```
let love = true;
if (love === true) {
  let happy;
  love === false;
} else {
  love === true;
}

console.log(love) // false
console.log(happy) //ReferenceError: happy is not defined
```
##### **Lexical/Static scope:** 

- Lexical scope is determined by the way the code is written. In other words, an item's lexical scope is the place in which the item got created. The place an item got invoked (or called) is not necessarily the item's lexical scope. Instead, an item's definition space is its lexical scope.

***Looking for variables happens from the inside going outwards; The internal scopes can reach the variables in the external scope but not the other way around: If you're inside the house you can see the people outside but they cannot see you.*** 
##### Hoisting
> Yo, ho, haul together,

> Hoist the colors high

- JavaScript Hoisting refers to the process whereby the interpreter appears to move the declaration of functions, variables or classes to the top of their scope, prior to execution of the code.
- In preparation for execution (which will be done line by line) the whole code is read and compiled, and in this process the declarations in the code seem to have happened at the top. Declarations themselves are hoisted, but assignments, even assignments of function expressions, are not hoisted. 

*most of the declarations haven't really happened so don't try to abuse the hoisting fact, it can't help you*

Hoisting allows functions to be safely used in code before they are declared.
###### Hoisting `let` & `const`
`lets` and `consts` are hoisted without initialization and will throw an error if you tried to reach them "above" their declaration point
`ReferenceError: Cannot access 'someVariable' before initialization`

`var`
- variables declared with the `var` keyword don't have block-scope and they can be reached from everywhere in the file/module 

```
let love = true;
if (love === true) {
  var happy = null;
  love === false;
} else {
  love === true;
}

console.log(happy); // null
console.log(love) // false
```

Now we can read the value of happy from the outside (even if we haven't actually assigned a meaningful value to it because we are not sure how we feel)

###### Hoisting `var`
`vars` are hoisted with declaration but without the initializing value if one was given; read from above they equal `undefined`

```
console.log(happy) // undefined
let love = true;
if (love === true) {
  var happy === null;
  love === false;
} else {
  love === true;
}
```
##### **Function scope**

- Functions create a scope that is indipendent from the outside field. That said, they can still look for variables on the outside, but the variables declared inside them can only be reached from the inside

```
console.log(happy); // ReferenceError: happy is not defined

function fallInLove(){
  let love = true;
  if (love === true) {
    var happy = null;
    love = false;
  } else {
    love === true;
  }
}
console.log(love) // ReferenceError: love is not defined
console.log(happy); // ReferenceError: happy is not defined
```
Of course, if I return `love` I can get its value from the outside:

```
function fallInLove(){
  let love = true;
  if (love === true) {
    happy = null;
    love = false;
  } else {
    love === true;
  }
  return love
}
console.log(fallInLove()); // false
```

###### !!! `let`, `const` and `var` - declared variables have function scope, omitting the keyword will result in a global variable which will leak outside of the scope of the function or block

```
function fallInLove(){
  let love = true;
  if (love === true) {
    happy = null; // declaring a naked happy variable
    love = false;
  } else {
    love === true;
  }
  return love
}

console.log(happy); // null
```
- let's also say that such a definition will not be hoisted 
`ReferenceError: a is not defined` will be thrown if we try to access it from above
##### Function Hoisting

1. Function declarations
 - function declarations will be hoisted in their entirety and can be called before their lexical declaration

 ```
console.log(fallInLove()); // false; yes, it's still false

function fallInLove(){
  let love = true;
  if (love === true) {
    happy = null;
    love = false;
  } else {
    love === true;
  }
  return love
}
 ```

 2. Function expressions / Arrow functions
- Function expressions will be hoisted according to the keyword used to declare them 

- `var` declarations will throw the following error since fallInLove is actually `undefined`

 ```
 console.log(fallInLove()); // ReferenceError: fallInLove is not a function
 var fallInLove = () => {
  let love = true;
  if (love === true) {
    happy = null;
    love = false;
  } else {
    love === true;
  }
  return love
}

 ```
 - `let`/`const`
 
 
```
 console.log(fallInLove()); // ReferenceError: Cannot access 'fallInLove' before initialization
 const fallInLove = () => {
  let love = true;
  if (love === true) {
    happy = null;
    love = false;
  } else {
    love === true;
  }
  return love
}
```
#### Closure

Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

- As far as I'm concerned `closure` is the ability of functions to remember and to carry whatever they need for their execution even if it happens away from their birthplace. Even if it's burned to the ground.


```
function giveXMasGift(gift) {
    return function(name) {
         return `Santa brought ${gift} for ${name}`;
    }
 }
 let secretSanta = giveXMasGift('socks');
 let secretSanta1 = giveXMasGift('DS3');
 
 console.log(secretSanta('Ed')); // Santa brought socks for Ed
 console.log(secretSanta1('Eddie')); // Santa brought DS3 for Eddie
```

In this example the return of the giveXMasGift function is another function that gets a `name` as a parameter and returns a string. The return statement, though, doesn't use only the given name but also the parameter `gift` that is given to the outer function.

To get to the inner function we need to call giveXMasGift so that it can create it, and we need to call it with the argument the inner function will use later on. Then, to see what has Santa brought to our current person of interest, we need to call the returned function (`secretSanta` in this case) with the name as an argument. This will return a string, containing both the `gift` and the `name` even though `gift` is passed to the outer function which has been called and has gone to the great beyond some time ago. 

![Alt text](https://64.media.tumblr.com/e5bcac2ad89c8de6c815a3dd8990c01a/tumblr_ofhy8yIRVx1vfdr29o1_400.gifv "a title")

We can also skip the assignment of the inner function to a variable and call it immediately: 
```
function giveXMasGift(gift) {
    return function(name) {
         return `Santa brought ${gift} for ${name}`;
    }
 }
 let secretSanta = giveXMasGift('socks')('Ed');

 
 console.log(secretSanta); // Santa brought socks for Ed
```
We can do this for as many functions as we can track with our limited attention span.

###### Beware the loop and non-block-scoped variables

```
for (var index = 1; index <= 3; index++) {
    setTimeout(function () {
        console.log('after ' + index + ' second(s):' + index);
    }, index * 1000);
}
```
###### To be fair, beware the leaking variables in general...
###### IIFE-It
```
let secretSanta = (function giveXMasGift(gift) {
    return function(name) {
         return `Santa brought ${gift} for ${name}`;
    }
 })('socks')
 
 console.log(secretSanta('Ed')); // Santa brought socks for Ed
```

This way we can't call giveXMasGift more than once. Everybody will be getting socks for Christmas when we call `secretSanta`.

![Alt text](https://c.tenor.com/aCMbLF-QvmIAAAAC/hohoho-holycrap.gif "when you think about closures for too long")

#### Module Pattern 

The Module Pattern is one of the important patterns in JavaScript. It is a commonly used Design Pattern which is used to wrap a set of variables and functions together in a single scope.
- It is used to define objects and specify the variables and the functions that can be accessed from outside the scope of the function.

- We expose certain properties and function as public and can also restrict the scope of properties and functions within the object itself, making them private: This means that those variables cannot be accessed outside the scope of the function.

```
const bankAccount = (function createBankAccount(){
  let balance = 0;
  
  const deposit = function (depositAmount) {
    if (typeof depositAmount === 'number' && !isNaN(depositAmount) && depositAmount >= 0) {
      balance += depositAmount;
      return balance;
    } else throw "Not a valid deposit amount! Must be a number bigger than zero.";
  };
  const withdraw = function (withdrawAmount) {
    if (withdrawAmount > balance) {
      throw "Balance too low to withdraw from.";
    } else {
      if (typeof withdrawAmount === 'number' && !isNaN(withdrawAmount && withdrawAmount >= 0)) {
        balance -= withdrawAmount;
        return balance;
      } else throw "Not a valid deposit amount! Must be a number bigger than zero.";
    }
  };
//   const getBalance = function () {
//     return `Current balance: ${balance} CRNCY`;
//   }
  
  return {
    deposit,
    withdraw,
    get CurrentAmount() {
        return  `Current balance: ${balance} CRNCY`;
    },
    //set CurrentAmount() {.......}
  };
})();

bankAccount.deposit(6000);
bankAccount.withdraw(200);
console.log(bankAccount.CurrentAmount); // Current balance: 5800 CRNCY


console.log('😘'); 
```

- The value assigned to `bankAccount` is the return value of the `createBankAccount` function expression (originally it didn't have a name, but I found it useful to add one for the purposes of this explanation and nothing else); `createBankAccount` returns an object that has as properties the various function defined inside `createBankAccount` that can help us manage our bank account. Those functions are then methods of `bankAccount` and they're *public*. 
We could define more functions inside that do something for our current balance but not return them because we don't want them to be used from the outside the function scope (the `balance` variable for example lives only to give us basis of the following functions and is *private*). 

#### Functional programming 

> the func the whole func and nothing but the func

##### Declarative vs. Imperative Programming Paradigm

| Declarative | Imperative |
| ----------- | ----------- |
|Declarative programming is a programming paradigm <br> that expresses the logic of a computation<br> without describing its control flow.|Imperative programming is a programming paradigm <br> that uses statements that changes the program’s state.|
|Declarative programming focuses on what <br> the program should accomplish.|Imperative programming focuses on how <br> the program should achieve the result.|
|Declarative programming provides less flexibility.|Imperative programming provides more flexibility.|
|Declarative programming simplifies the program.|Imperative programming can increase the complexity of the program.|
|Functional, Logic, Query programming <br> falls into declarative programming.|Procedural and Object Oriented programming <br> falls into imperative programming.|


#### FP

-  Functional programming is a paradigm of building computer programs using expressions and functions without mutating state and data. By respecting these restrictions, functional programming aims to write code that is clearer to understand and more bug resistant. This is achieved by avoiding using flow-control statements (for, while, break, continue, etc.) which make the code harder to follow. Also, functional programming requires us to write pure, deterministic functions which are less likely to be buggy.

- A large program is a costly program, and not just because of the time it takes to build. Size almost always involves complexity, and complexity confuses programmers. Confused programmers, in turn, introduce mistakes (bugs) into programs. A large program then provides a lot of space for these bugs to hide, making them hard to find.

- Functional programming provides a higher level of abstraction: what's happening when we invoke a function is not shown in details but rather implied (for example by the function's name). Abstractions hide details and give us the ability to talk about problems at a higher (or more abstract) level. 

##### Pure Functions

> Be thou as chaste as ice,
> as pure as snow, 
>thou shalt not escape calumny

- Pure functions are functions that are realiable: They garantee that the output value for a given input will always be the same no matter how many times we pass it to them. To achieve this they should not use anything that may change without their knowledge.

```
const constant = 24;
function getAlienYears(humanYears) {
  return humanYears * constant
}
```
In this case the `constant` variable may change from the point of view of the function since it's separate from it. It can get changed or deleted and then `getAlienYears` will no longer work as expected.

```
function getAlienYears(humanYears) {
  return humanYears * 24
}
```
Now `getAlienYears` is a pure function. No matter how many times we tell it to compute 2 human years to alien years the output will always be 48.

- Pure functions don't have **side effects**

```
let liyaAge = 23;
function ageLiya() {
  return ++liyaAge
}

console.log(ageLiya()); // 24
```
The function `ageLiya` has a side effect: It increments a variable that does not belong to it AND it has the audacity to use a non-local variable in the first place.

Modifying an array or an object, writing to a file, and logging to the console are other examples of side effects.

### Pure Array Methods
#### The Holy Trinity: `.map`, `.filter`, and `.reduce`

- The Holy Trinity are what we call ***higher order functions*** - functions that accept as parameters other functions and/or return functions as result. 

In our example of closure we used a HOF:

```
function giveXMasGift(gift) {
    return function(name) {
         return `Santa brought ${gift} for ${name}`;
    }
 }
 let secretSanta = giveXMasGift('socks')('Ed');
 ```

- `giveXMasGift` is a HOF since it returns another function.

`.map`, `.filter`, and `.reduce` all accept a function as an argument:

```
arr = [1, 2, 3]; // calling array
arr
.map(callback function)
.filter(callback function)
.reduce(callback, accumulator*)
```
### `.map`
- The map() method creates a new array filled with the results of calling a provided function on every element in the calling array. 
##### .map syntax:
```
// Arrow function
map((element) => { /* ... */ })
map((element, index) => { /* ... */ })
map((element, index, array) => { /* ... */ })

// Callback function
map(callbackFn)
map(callbackFn, thisArg)

// Inline callback function
map(function(element) { /* ... */ })
map(function(element, index) { /* ... */ })
map(function(element, index, array){ /* ... */ })
map(function(element, index, array) { /* ... */ }, thisArg)
```
```
const arr = [1, 2, 3];
const mapped = arr.map(x => x**2);
console.log(mapped) // [1, 4, 9]

```
### `.filter` 

- The filter() method creates a new array with all elements that pass the test implemented by the provided function. The function called with the element is a predicate to be confirmed or denied - i.e, it will return `true` and the element will be put in the new array or `false` and the element will not appear in the returned array. 
##### .filter syntax:

```
// Arrow function
filter((element) => { /* ... */ } )
filter((element, index) => { /* ... */ } )
filter((element, index, array) => { /* ... */ } )

// Callback function
filter(callbackFn)
filter(callbackFn, thisArg)

// Inline callback function
filter(function(element) { /* ... */ })
filter(function(element, index) { /* ... */ })
filter(function(element, index, array){ /* ... */ })
filter(function(element, index, array) { /* ... */ }, thisArg)
```

```
const arr = [1, 2, 3];
const isEven = (x) => (x % 2 === 0)? true:false;
const filtered = arr.filter(x => isEven(x));
console.log(filtered) // [2]
```

### `.reduce` 

- The reduce() method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

- The first time that the callback is run there is no "return value of the previous calculation". If supplied, an initial value may be used in its place. Otherwise the array element at index 0 is used as the initial value and iteration starts from the next element (index 1 instead of index 0).

##### .reduce syntax:

```
// Arrow function
reduce((previousValue, currentValue) => { /* ... */ } )
reduce((previousValue, currentValue, currentIndex) => { /* ... */ } )
reduce((previousValue, currentValue, currentIndex, array) => { /* ... */ } )
reduce((previousValue, currentValue, currentIndex, array) => { /* ... */ }, initialValue)

// Callback function
reduce(callbackFn)
reduce(callbackFn, initialValue)

// Inline callback function
reduce(function(previousValue, currentValue) { /* ... */ })
reduce(function(previousValue, currentValue, currentIndex) { /* ... */ })
reduce(function(previousValue, currentValue, currentIndex, array) { /* ... */ })
reduce(function(previousValue, currentValue, currentIndex, array) { /* ... */ }, initialValue)
```
 - the `previousValue` is the accumulator/accumulated value i.e. the value that will be returned in the end

 ```
let sum = [0, 1, 2, 3].reduce(function (previousValue, currentValue) {
  return previousValue + currentValue
}, 0)
// sum is 6
 ```
 The return value of reduce is a single value, but it can be an array or an object.

 The callback functions can be more complex...:

 ```
 function groupBy(data) {
  const toGroup = data[data.dataProp];
  
  const result = (toGroup) => {
    const grouped = toGroup.reduce((acc, el) => {
      const GBP = data['groupByProp'];
      const key = el[GBP];

      if (!(key in acc)) {
        acc[key] = [];
        acc[key].push(el);
      } else {
        acc[key].push(el);
      }
      return acc;
    }, {});
    return grouped;
  };
  return result(toGroup);
};

```
...And even much more complex than this.

*This is a custom implementation of the groupBy method:
###### The groupBy() method groups the elements of the calling array according to the string values returned by a provided testing function. The returned object has separate properties for each group, containing arrays with the elements in the group. This method should be used when group names can be represented by strings.

