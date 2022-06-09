# <h1 align="center"> Object-Oriented Programming ❤️ (as read by Liya) </h1>

## Object-Oriented Programming (OOP)

#### Data

Data can be defined as a representation of facts, concepts, or instructions in a formalized manner, which should be suitable for communication, interpretation, or processing by human or electronic machine.

Data is represented with the help of characters such as alphabets (A-Z, a-z), digits (0-9) or special characters (+,-,/,*,<,>,= etc.)

##### What is Information?
Information is organized or classified data, which has some meaningful values for the receiver. Information is the processed data on which decisions and actions are based.

For the decision to be meaningful, the processed data must qualify for the following characteristics −

 - **Timely** − Information should be available when required.

- **Accuracy** − Information should be accurate.

- **Completeness** − Information should be complete.


```js
const age = 'green';    
```

Unless we have specified what green means according to the age (e.g. 0-30 years equals green age), the example above is completely meaningless considering that age is measured in years or months and not in colours. If we do specify what `green` means and for example we want to label specific age groups in this manner, though, we will have meaningful information. Why we would do that is another question entirely...

***In computing***, data is information that has been translated into a form that is efficient for movement or processing. Relative to today's computers and transmission media, data is information converted into binary digital form. It is acceptable for data to be used as a singular subject or a plural subject. Raw data is a term used to describe data in its most basic digital format.


###### The term `big data` has been used to describe data in the petabyte range or larger. 

Just sayin'.

[Data (computing), Wikipedia](https://en.wikipedia.org/wiki/Data_(computing))

##### Data Processing Cycle

- Data processing is the re-structuring or re-ordering of data by people or machine to increase their usefulness and add values for a particular purpose. 

![Alt text](https://image.slidesharecdn.com/vii-cs-1-130603024919-phpapp01/95/data-processing-cycle-24-638.jpg?cb=1370227825 "when you think about closures for too long")

[Data Processing](https://www.simplilearn.com/what-is-data-processing-article#data_processing_cycle)

<h2>VALIDATE YOUR DATA</h2>

#### Objects as data-keepers

Objects allow us to hold - to group or split - information in a meaningful way. They also allow us to pass it around keeping this meaning intact.

An object consists of the following:

 - Data members - Data members are the variables. They establish the state or attributes for the object.

- Member functions - Member functions represent the code to manipulate the data. The behaviour of the object is determined by the member functions.

Objects can have `state` and `behaviour`.

**State** refers to the data that is stored in the object - organized in *fields* - properties and values.
**Behaviour** refers to the predifined functions (methods) of the object.

You can change the state of an object by directly accessing its properties (1) or by using its methods (2).
1.
```js
const self = {
    name: 'Liya',
    birthday: {
        day: 24,
        month: '',
        year: 1998
    },
    age: 23,
    skills: null,
    haircolour: 'dark brown',
    eyecolour: 'green',
    growUp: function (years) {this.age = years}
}

self.age = 24

console.log(self.age);
```

2.
```js
const self = {
  name: 'Liya',
  birthday: {
      day: 24,
      month: '',
      year: 1998
  },
  age: 23,
  skills: null,
  haircolour: 'dark brown',
  eyecolour: 'green',
  growUp: function (years) {this.age = years}
}

self.growUp(25)

console.log(self.age); // 25

```

By using a method you can protect the state of your data from becoming invalid:

```js
const self = {
    name: 'Liya',
    birthday: {
        day: 24,
        month: '',
        year: 1998
    },
    age: 23,
    skills: null,
    haircolour: 'dark brown',
    eyecolour: 'green',
    growUp: function (years) {
        if (isNaN(years)) throw 'Age must be a valid number!';
        else this.age = years;
    }
}

self.growUp('blue pink'); // Age must be a valid number!
```

#### Context Binding

![Alt text](https://c.tenor.com/O0ra4ogBjYEAAAAC/lord-of-the-rings-gandalf.gif)

- `this` is used in functions
- `this` does not refer to the function itself

- `this` is a placeholder which binds itself to *something* when the function is invoked and its reference depends on where the function is being called 

Its bond can be determined according to 4 rules:

##### 1. Default Binding

```js
const speak = function () {
  console.log(`Hi, my name is ${this.name}`)
}

speak() // Hi, my name is undefined
```

If we call a function, using `this`, on its own, it will bind itself to the global scope that doesn't have a name so the result will be `undefined`.

If the global scope gets a name, then `this` will get that name.

```js
name = 'Global'
const speak = function () {
  console.log(`Hi, my name is ${this.name}`)
}

speak() // Hi, my name is Global
```

##### 2. Implicit binding

``` js
const speak = function () {
  console.log(`Hi, my name is ${this.name}`)
}

const context = {
  name: 'Implicit',
  presentYourself: speak 
}

context.presentYourself() // Hi, my name is Implicit
```
In this case the method `presentYourself` refers to the `speak` function and thus the `speak` function is called inside the `context` object and `this` binds itself to it and searches for `context.name` which is *Implicit*.

##### 3.1 Explicit Binding 

Until now we haven't actually told our `speak` function to bind itself to anything. We just called it indirectly inside an object that makes sense to it and it happened um, *naturally*.


``` js
const speak = function () {
  console.log(`Hi, my name is ${this.name}`)
}

const context = {
  name: 'Explicit'
}

speak.call(context) // Hi, my name is Explicit
```
Here the `context` object no longer has a method that refers to the function. We explicitly tell `speak` to be called in the context of, well, `context`. 

##### 3.2 Explicit Hard Binding

``` js
const speak = function () {
  console.log(`Hi, my name is ${this.name}`)
}

const context = {
  name: 'Hard Explicit'
}

const SpeakInContext = speak.bind(context) 
SpeakInContext() // Hi, my name is Hard Explicit
```

`.bind()` returns a new, bound function. `SpeakInContext` will execute the functionality of `speak` always in the context of `context`.

*P.S.* In all these, though, `speak`, on its own, will give the result `Hi, my name is undefined`: the `this` inside of it refers to the global scope. We are not actually changing that. Just the context.

*P.P.S.* In strict mode `this` is `undefined` and will not refer to the global object. 

##### 4. `new` Binding

- A `new` keyword is used to create an object from the constructor function.

- Bound functions are automatically suitable for use with the new operator to construct new instances created by the target function. When a bound function is used to construct a value, the provided this is ignored.

```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function() {
  return `${this.x},${this.y}`;
};

const p = new Point(1, 2);
p.toString();
// '1,2'

//  not supported in the polyfill below,

//  works fine with native bind:

const YAxisPoint = Point.bind(null, 0/*x*/);

const emptyObj = {};
const YAxisPoint = Point.bind(emptyObj, 0/*x*/);

const axisPoint = new YAxisPoint(5);
axisPoint.toString();                    // '0,5'

axisPoint instanceof Point;              // true
axisPoint instanceof YAxisPoint;         // true
new YAxisPoint(17, 42) instanceof Point; // true
```


```js
const Cartoon = function(name, character) {
    this.name = name;
    this.character = character;
    this.log = function() {
        console.log(this.name +  ' is a ' + this.character);
    }
};

const tom = new Cartoon('Tom', 'Cat');
//let jerry = new Cartoon('Jerry', 'Mouse');

tom.log() // Tom is a Cat
```
- When a function is invoked with the `new` keyword, JavaScript creates an internal this object (like this, `this = {}`) within the function. The newly created `this` binds to the object being created using the `new` keyword.
- Here the function Cartoon is invoked with the `new` keyword. So the internally created `this` will be bound to the new object being created here, which is `tom`.
###### This constructor function may be converted to a class declaration.ts (80002) 😁
```js
class Cartoon {
    constructor(name, character) {
        this.name = name;
        this.character = character;
        this.log = function () {
            console.log(this.name + ' is a ' + this.character);
        };
    }
}

const tom = new Cartoon('Tom', 'Cat');
//let jerry = new Cartoon('Jerry', 'Mouse');

tom.log() // Tom is a Cat
console.log(tom instanceof Cartoon); // true
```
`console.log(tom instanceof Cartoon);` is also true when the constructor function and not the class declaration is used to create the instance.

#### OOP Fundamentals

- Object-oriented programming (OOP) is a computer programming model that organizes software design around data, or objects, rather than functions and logic.

- OOP focuses on the objects that developers want to manipulate rather than the logic required to manipulate them. 

##### Classes 



##### The 4 Principles of OOP

![](https://cdn.climatechangenews.com/files/2014/01/800px-Apocalypse_vasnetsov.jpg)

1. **Encapsulation**:
- This principle states that the state and the methods of the object are enclosed together (in a logically sound way).

**Information hiding** - important information is contained inside an object and only select information is exposed. The implementation and state of each object are privately held inside a defined class. Other objects do not have access to this class or the authority to make changes. They are only able to call a list of public functions or methods. This characteristic of data hiding provides greater program security and avoids unintended data corruption.

2. **Abstraction**:
- Objects only reveal internal mechanisms that are relevant for the use of other objects, hiding any unnecessary implementation code. Objects in an OOP language provide an abstraction that hides the internal implementation details. Similar to the coffee machine in your kitchen, you just need to know which methods of the object are available to call and which input parameters are needed to trigger a specific operation. But you don’t need to understand how this method is implemented and which kinds of actions it has to perform to create the expected result. 

3. **Inheritance**:
- Classes can reuse code from other classes. Relationships and subclasses between objects can be assigned, enabling developers to reuse common logic while still maintaining a unique hierarchy. This property of OOP forces a more thorough data analysis, reduces development time and ensures a higher level of accuracy.

4. **Polymorphism**:
- is the ability to create a variable, a function or an object that has more than one form. 

[PM](https://blog.sessionstack.com/how-javascript-works-3-types-of-polymorphism-f10ff4992be1)



**method overriding** - a child class' method with the same name as a parent class' method will override it [the parent method].

#### Classes & Instances

[OOP Classes & Instances, examples in Python](https://brilliant.org/wiki/classes-oop/#:~:text=The%20class%20is%20a%20blueprint,a%20mechanism%20of%20reusing%20code.)

In object-oriented programming, a class is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables or attributes), and implementations of behavior (member functions or methods). The user-defined objects are created using the class keyword. An instance is a specific object created from a particular class.

```js
class Adams {
    constructor(name) {
        this.name = `${name} Adams`
    }

    speak() {
        return `My name is ${this.name}`
    }
}

let child = new Adams('Wednesday')

console.log(child.speak()); // My name is Wednesday Adams
```

- After declaring the class name, a programmer must define a constructor method. While a class is a blueprint for a new data type, the programmer still needs to create values of this data type in order to have something that can store in variables or pass to functions. When called, the constructor creates the new object, runs the code in the constructor, and returns the new object.

##### Static Members 

- static members are fields or methods that are called for the class itself and not for each of the instances separately 

```js
class BibliographyOfWilde {
    static author = 'Oscar Wilde'
  
    constructor(name, pubYear, genre) {
      this.name = name;
      this.pubYear = pubYear;
      this.genre = genre;
    }
  
    giveBookInfo() {
      return `Book name: ${this.name}, written by ${BibliographyOfWilde.author}, published in ${this.pubYear}, genre: ${this.genre}`
    }
}

let DorianGray = new BibliographyOW('The Picture of Dorian Gray', 1890, 'Gothic fiction')

console.log(DorianGray.giveBookInfo());
```
The author will not vary for the instances since all the oeuvres will be authored by Oscar Wilde so we can give the class this static property. You cannot access it through `this`.

##### Private Fields

```js
class Author {
    #authorName;
    birthplace;
}

let ACDoyle = new Author();

ACDoyle.birthplace = 'UK'
console.log(ACDoyle.birthplace); // UK
ACDoyle.#authorName // Property '#authorName' is not accessible outside class 'Author' because it has a private identifier.ts(18013)
```
- private fields can be accessed from within the class instance but not from the outside, but there are ways to work with it...

```js
class Author {
    #authorName;
    birthplace;
    constructor(name) {
        this.#authorName = name
    }

    name() {return this.#authorName}
}

let Doyle = new Author('Sir Arthur Conan Doyle');

Doyle.birthplace = 'UK'
console.log(Doyle.birthplace, Doyle.name()); // UK Sir Arthur Conan Doyle
```

##### Properties 

- Properties are written like methods but used as fields. They are often used to manage the values of private fields. 
- Properties have two parts: A `get` part, used to access the value of the property (has no parameters and returns a value), and a `set` part which is used to write a value to the property (the `set` has one parameter and no return value).

```js
class Author {
    #authorName;
    birthplace;
    
    get authorName() {return this.#authorName}
    set authorName(name) {this.#authorName = name}

}

let Doyle = new Author();

Doyle.birthplace = 'UK'
Doyle.authorName = 'Sir Arthur Conan Doyle'
console.log(Doyle.birthplace, Doyle.authorName); // UK Sir Arthur Conan Doyle
```

Using only a getter will result in a read-only property and using only a setter will result in a write-only property (which is strange and unusual).

#### Inheritance 

- Through inheritance classes can inherit the characteristics of a *base/super* (parent) class using `extends`. 

```js
class Author {
    #authorName;
    #bibliography;
    constructor(name, ...works) {
        this.#authorName = name;
        this.#bibliography = works;
      
    }
    get bibliography() {return [...this.#bibliography].join(',')}
    set bibliography(b) {
      if (b instanceof Array) this.#bibliography = b;
    }
    get authorName() {return this.#authorName}
    set authorName(name) {this.#authorName = name}

}

let MT = new Author('Mark Twain', 'The Adventures of Tom Sawyer', 'The Prince and the Pauper')

console.log(MT.bibliography); // The Adventures of Tom Sawyer,The Prince and the Pauper

class Poet extends Author {
// all the functionality from Author is implicitly here
}

let IV = new Poet('Иван Вазов', 'Люлека ми замириса', 'Опълченците на Шипка');

console.log(IV.authorName); // Иван Вазов
```

- the *derived* (child) classes should be used to build upon the inherited functionality by adding new fields, methods or properties or modifying existing members

- using inheritance makes sense if the child class is truly a sub-class of the parent class 

##### Member overriding 

Overriding the constructor:
```js
class Author {
    #penName;

    constructor(penname) {
        this.#penName = penname;      
    }
    
    get penName() {return this.#penName}
    set penName(name) {this.#penName = name}

}

let MT = new Author('Mark Twain')

console.log(MT.penName); // Mark Twain

class Poet extends Author {
#bibliography;

constructor(penname, ...works) {
    super(penname);
    this.#bibliography = works;
}


get bibliography() {return this.#bibliography.join(', ');}
}

let HS = new Poet('Христо Смирненски', 'Братчетата на Гаврош', 'Цветарка');

console.log(HS.penName, HS.bibliography); // Христо Смирненски Братчетата на Гаврош, Цветарка
```

We can add as many new methods and fields as we want/need. We can change the existing members and access the superclass' members (as long as they're public) with the `super` keyword.

##### Uses of Inheritance
- Since a child class can inherit all the functionalities of the parent's class, this allows code reusability.
- Once a functionality is developed, you can simply inherit it. No need to reinvent the wheel. This allows for cleaner code and easier to maintain.
- Since you can also add your own functionalities in the child class, you can inherit only the useful functionalities and define other required features.

#### Composition

- Composition describes a class that references one or more objects of other classes in instance variables. This allows you to model a has-a association between objects.

[Object composition in JS](https://medium.com/code-monkey/object-composition-in-javascript-2f9b9077b5e6)

Creating an instance of `Bibliography` inside the constructor:
```js
class Bibliography {
    #prose;
    #poetry;
  
    constructor(proseOeuvres, poetryOeuvres) {
      this.#prose = proseOeuvres.split(', ');
      this.#poetry = poetryOeuvres.split(', ')
    }

    get prose() {return this.#prose.join(', ');}
    get poetry() {return this.#poetry.join(', ');}
}

class Author {
    #name;
    #bibliography;

    constructor(name, prose, poetry) {
        this.#name = name;
        this.#bibliography = new Bibliography(prose, poetry);
    }

    get name() {return this.#name;}
    get bibliography() {
        return `
        Prose: ${this.#bibliography.prose},
        Poetry: ${this.#bibliography.poetry}
        `;
    }
}

let OW = new Author('Oscar Wilde', 'The Picture of Dorian Gray', 'Requiescat, The Garden of Eros');

console.log(`${OW.name}: ${OW.bibliography}`); 
/* 
Oscar Wilde: 
        Prose: The Picture of Dorian Gray,
        Poetry: Requiescat, The Garden of Eros
*/
```

Passing any instance of `Bibliography` as a parameter to the constructor:
```js
class Bibliography {
    #prose;
    #poetry;
  
    constructor(proseOeuvres, poetryOeuvres) {
      this.#prose = proseOeuvres.split(', ');
      this.#poetry = poetryOeuvres.split(', ')
    }

    get prose() {return this.#prose.join(', ');}
    get poetry() {return this.#poetry.join(', ');}
}

class Author {
    #name;
    #bibliography;

    constructor(name, instanceOfBibliography) {
        this.#name = name;
        this.#bibliography = instanceOfBibliography;
    }

    get name() {return this.#name;}
    get bibliography() {
        return `
        Prose: ${this.#bibliography.prose},
        Poetry: ${this.#bibliography.poetry}
        `;
    }
}

let OW = new Author('Oscar Wilde', new Bibliography('The Picture of Dorian Gray', 'Requiescat, The Garden of Eros'));

console.log(`${OW.name}: ${OW.bibliography}`);
```

#### Cohesion & Coupling

##### Cohesion:
- In computer programming, cohesion refers to the degree to which the elements inside a module belong together. In one sense, it is a measure of the strength of relationship between the methods and data of a class and some unifying purpose or concept served by that class. In another sense, it is a measure of the strength of relationship between the class's method and data themselves.

-  Cohesion represents the clarity of the responsibilities of a module.

![](https://ducmanhphan.github.io/img/design-pattern/core-oop/cohension-coupling/high-low-cohesion.png)

- If our module performs one task and nothing else or has a clear purpose, our module has high cohesion. On the other hand, if our module tries to encapsulate more than one purpose or has an unclear purpose, our module has low cohesion.

- Modules with high cohesion tend to be preferable, simple because high cohesion is associated with several desirable traits of software including robustness, reliability, and understandability.

- Low cohesion is associated with undesirable traits such as being difficult to maintain, test, reuse, or even understand.

- Cohesion is often contrasted with coupling. High cohesion often correlates with loose coupling, and vice versa.

- Single Responsibility Principle aims at creating highly cohesive classes.

Cohesion is increased if:

The functionalities embedded in a class, accessed through its methods, have much in common.
Methods carry out a small number of related activities, by avoiding coarsely grained or unrelated sets of data.

##### Coupling 

- Coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are; the strength of the relationships between modules. *How indipendent or interdipendent two classes/modules are.*

[Cohesion & Coupling](https://ducmanhphan.github.io/2019-03-23-Coupling-and-Cohension-in-OOP/)

- Coupling increases between two classes A and B if:

- A has an attribute that refers to (is of type) B.
- A calls on services of an object B.
- A has a method that reference B (via return type or parameter).
- A is a subclass of (or implements) class B.

###### In the composition examples, when the instance of the `Bibliography` class is created inside the constructor of the `Author` class, the `Author` class creation strongly depends on the implementation of `Bibliography` since the number of parameters given to it rely on the number of paramenters that the bibliography will need to be created.

<table>
  <thead>
    <tr>
      <th>Cohesion</th>
      <th>Coupling</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cohesion is the indication of the relationship within module</td>
      <td>Coupling is the indication of the relationships between modules</td>
    </tr>
    <tr>
      <td>Cohesion shows the module’s relative functional strength</td>
      <td>Coupling shows the relative independence among the modules</td>
    </tr>
    <tr>
      <td>Cohesion is a degree (quality) to which a component / module focuses on the single thing</td>
      <td>Coupling is a degree to which a component / module is connected to the other modules</td>
    </tr>
    <tr>
      <td>While designing we should strive for high cohesion. Ex: cohesive component/module focus on a single task with little interaction with other modules of the system</td>
      <td>While designing we should strive for low coupling. Ex: dependency between modules should be less</td>
    </tr>
    <tr>
      <td>Cohesion is the kind of natural extension of data hiding, for example, class having all members visible with a package having default visibility</td>
      <td>Making private fields, private methods and non public classes provides loose coupling</td>
    </tr>
    <tr>
      <td>Cohesion is Intra – Module Concept</td>
      <td>Coupling is Inter - Module Concept</td>
    </tr>
  </tbody>
</table>

#### DRY KISS YAGNI

- **Don't repeat yourself**: If you can separate and reuse a functionality that you use over and over again instead of writing it anew each time, maybe do that.
- **Keep it simple, stupid**: Unneccesary complexity must be avoided. Strive for simplicity in code design. Also, like, in general. (**WET** - Write everything twice.)
- **You aren't gonna need it**: Don't overthink future possibilities and protect your code from things that are unlikely to happen. You can't make futureproof code anyway.

![](https://miro.medium.com/max/1400/1*YCLo-nmjV6QRt5Vv3ecCTw.png)

#### [SOLID](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

