 # <p align="center"> JavaScript ❤️ Basic Theory (as read by Liya) </p>

## I
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

#####Static Analysis Tools / Linters

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
//Using lodash
const doppelganger = _.cloneDeep(self);
```
#### 