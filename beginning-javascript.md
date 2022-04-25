# begining-javascript
Highlights from Wes Bos course - Beginner Javascript

## Content: 

1. [The Tricky Bits](#the-tricky-bits-module-3)
2. [The DOM](#the-dom-module-4)
3. [Events](#events-module-5)
4. [Logic and Flow Control](#logic-and-flow-control-module-7)
5. [Data Types](#data-types-module-8)

## The Tricky Bits *(Module 3)*

**Closures**: is the ability to access to a parent level scope from a child scope, even after the parent function has been closure.

```javascript
function sayHi(greeting = ''){
  const gretting = 'Hi'
  
  return function sayName(name){
    return `${greeting} ${name}!`
  }
}

const myGreeting = sayHi('Hey');
console.log(myGreeting('folks!')) // This logs Hey folks!

```




**Hoisting**: Two things are hoisted in JS, which means that are accesible even before where they are declare:
- var variables.
- regular functions (not anonymous function, as arrow functions)

Example:


```javascript
sayHi(); // it logs hello

function sayHI() {
   console.log('hello')
}
```

# The DOM *(Module 4)*

The DOM (Document Object Model) is the start base for every framework.

- window: is a global scope in the browser. Where all our global variables are stored and everything about the current open browser.


**Element Selectors**:
- querySelector().
- querySelectorAll().

```javascript
const header = document.querySelectorAll('h2')

// document selects all the h2 tag elements in our html file
```

```javascript
const items = document.querySelectorAll('.item')
const paragraphs = header.querySelector('p')

//selects every <p> tag the inside item class.
```
**Elements**:
Is a tag on the page.
When we select an element with query selector it returns an object with a lot of props that we can use as *getters* or *setters*.

- getters: pulls tha data out of that object.
- setters: update the content in an element.

```javascript
const items = document.querySelectorAll('.item')
const paragraphs = header.querySelector('p')

paragraph.textContent = "I'm a paragraph tag element"; -> // textContent is an example of a setter, there are many more.

//selects the <p> tag and overwrite the content.
```

**Classes**:

- .classList // selects all the classes in your html document.
- .add // .add('nice') Adds a new class.
- .remove //
- .toggle // .toggle('round') add the round class when it's false and remove whhen it's true
- .addEventListener('click', toggleRound) or window.addEventListener('load', fucntion() {console.log()pic.naturalWidth} -> This event WILL WAIT UNTILL THE PIC IS LOADED.)
- .contains('yourClassName')

**Attributes**:
Anything provided to an element as additional info, ex: class='your-class' or src='your-path.html'.
They act most of them as getters and setters:
- .setAttribute('alt', 'cute pup') it's the same as pic.alt = 'cute pup'
- .getAttribute('alt')

**Create Elements/HTML**

1. createElement():
- document.createElement() // This cretes an element in memory

```javascript

const paragraph = document.createElement('p');
paragraph.textContent = 'I'm a paragraph';
paragraph.CllassList.add('special');

```

- .appendChild(); // Needed to insert the nodes (elements or piece of text) in our html file.


```javascript

const myDiv = document.createElement('div');


const paragraph = document.createElement('p');
paragraph.textContent = 'I'm a paragraph';
myDiv.appendChild(paragraph) // inserts the paragraph into the div element.

document.body.appendChild(myDiv); // The one with document.body.appendChild() should be at the end of the appends to not cause a lot of renders.

```

2. insertAdjacementElement(*position, element*):

```javascript


const heading = document.createElement('h2');
heading.textContent = 'I'm a heading';

myDiv.insertAdjacementElement('beforebegin', heading) // inserts the paragraph into before the div element.

```

3. innerHTML. Adds HTML elements using backticks string and you can interpolate variables too inside the strings.

```javascript
const item = document.querySelector('.item')
const name = 'Peter'

item.innerHTML = `<h1>Hey ${name}! I'm a title</h1>`
```


# Events *(Module 5)*

**Event Listeners**

Elements on the page emits events, when they are clicked, hovered, dragged for example. When you interact with them.

1. addEventListener(*event, callBack function*) // callBack function is a reference to a function, we are not triggered that function, the browser for example could do it, when there is a click event. You can pass anonymus functions too as a second parameter.

```javascript
function handleClick() {
  console.log('It's clicked!')
}

const item = document.querySelector('.item')
item.addEventListener('click', handleClick) // callBack function, one of the benefits is you can reuse the handleClick function in other .addEventListener() you declare and don't repeat code.

```

1.1. Select many elements.

```javascript
const manyButtons = document.querySelectorAll('button.save')

manyButtons.forEach(button => {
  button.addEventListener('click', handleClick)
}); // When we use an arrow function inside the event listener then we can not unbinding it cause it's an anonymous function..

//This allows us to every single element has been bind individually.
```

2. removeEventListener(*event, callBack function*). Same addEventListener but to stop the event.

```javascript
item.removeEventListener('click', handleClick) // habndleClick is a reference to the original function.
```

**Events - Targets, propagation, bubbling and capture**

- The event object: Object files in with useful user information. Example. If we have three buttons, how do I know which one was clicked?

*How?*

We modify our call-back function to pass in the parameter event (it does not matter how we call it as long is the first parameter of our function)

```javascript
const item = document.querySelector('.item')

item.addEventListener('click', function(event) {
  console.log(event)
})

```

In the event we have access to the *target* prop:

```javascript
const button = document.querySelector('.item')

button.addEventListener('click', function(event) {
  console.log(event.target) // Logs the button that was clicked.
})

```

The difference between *.target* and *.currentTarget* is that .currentTarget refers to the specific element where the user has clicked, is the one that fired the event. Example: an icon inside the button, or the text.

But at the same time, you are clicking also in the button and at the same time you are clicking on the window, and in the browser, etc, etc -> this is wrapping two concepts which are **propagation and bubbling**

**Bubbling up and capture down:**

[More info about this phases](https://www.w3.org/TR/2003/NOTE-DOM-Level-3-Events-20031107/events.html#Events-phases)

If we want to stop the event from bubbling up we have a method:

```javascript
event.stopPropagation() 
```
The event.stopPropagation works also for capture down.

- The .addEventListener() accepts three arguments:
  - first: the type of the event, 
  - second: the function or callback,
  - third: a new object filled with options.

In that last parameter, the options object we can pass the prop capture set to true and the event is fired from outside to inside, capture down which means in the opposite way. Bubbling up and capture down.


```javascript
const button = document.querySelector('.item')

button.addEventListener('click', function(event) {
  console.log(event.target) 
}, {capture: true}) // Indicates to start propagation from outside to inside, which means from the browser to the window, to the button element, to the icon.

```

**Some extra tips:**

- Prevent default: the method ```.preventDefault()``` is used when you want to prevent the default thing to happen.
- The best way to grab element from a form is given to the input the property name, example:

```javascript
<input type='text' name='name'>
<input type='email' name='email'>

const name = event.currentTarget.name.value;
const email = event.currentTarget.email.value;
```

- Diference between button and link:
   - Links are used to change the page. Ex: Breadcrumb links.
   - Buttons are used for actions that happen inside the application. Ex: Save or Follow button.
   
   Example: using an ```<a href='#'>Save</>``` to save something is not a good practice.
   
   
 # Logic and Flow Control *(Module 7)*

**BEDMAS:**
Order of operation in which Javascript runs:

- B: brackets go first, in this case -> parenthesis.
- E: exponents. (example: ```2 ** 10```)
- D: division.
- M: multiplication.
- A: addition.
- S: substraction.

```javascript
const age = 10 * 5 - 2; // 48, multiplication goes first.

const age = 10 * (5 - 2); // 30. brackets goes first.
```


**If statements:**

```javascript
const age = 15;

if (age > 18) {
  console.log("You can drive")
  
} else if (age < 18) {
  console.log("You can't drive")
  
} else {
  console.log("You can drive")
}

// If the first if condition it's true the rest of the if else, and else are not going to be reached.

```

```javascript

if (age > 18) {
  console.log("You can drive")  
} 
if (age < 18) {
  console.log("You can't drive")
} 
if (age === 18) {
  console.log("You can drive")
}

// This way every if statement is going to be checked.

```
**Operators:**

- One single equal: set the value. `Ex: age = 10;`
- Two equals: compare the value is the same. `Ex: age == 10; // true` **But** careful with this because this: `Ex: age == '10';` is also true, that is why is always recommended to use triple equals.
- Not equals: `Ex: age !== '10' // true`
- OR: `Ex: name === 'Sam' || name === 'Kelly'`
- AND: `Ex: if (name === 'Sam' && name === 'Kelly') console.log('Cool name!') // if one of then it's false, it's going to return false` 

**Truthy and Falsy:**

- Number 0: Falsy, when you run a 0 is equal to false.
- Number 1: Truthy, when you run it will return true.
- Number -10: Truthy, if 0 is falsy all the rest of the numbers are truthy.
- Undefined: Falsy.
- Null: Falsy.
- NaN: Falsy.
- Empty string: `''` is falsy.
- A string: `'Hello'`is truthy.
- A string of zero: `'0'` is truthy. (A string of anything is truthy, even a string with a space `' '`)
- Empty array: `[]` is truthy. But `[].length() returns 0, then is false`
- Empty object: `{}` is truthy. But `Object.keys({}).length() returns 0, then is false`

**Coercion:**

Is when we forced a value of a different type, like a string or a number, or an object, or anything that is not a Boolean and we coerced into a true Boolean.

```javascript
const name = 'John';
!!name // With the two bangs in front of it we forced the string to be a boolean value.

const emptyString = ''; // Falsy value.
!emptyString; // Returns true.
!!emptyString; // Returns false.
```

The truthy and and falsy values that if we want to coerced them into real true or false values we can do the same with them as in the above example. A single bang will give you the opposite of what they are.

**Ternary:**
A simplier/quickier way to declare an if/else statement.

```javascript
const count = 0;

const word = count === 1 ? 'item' : 'items';

console.log(`You have ${count} ${word} in your cart`)
```
Can be used with functions:

```javascript
const showAdminBar = () => console.log('Show admin bar')
const isAdmin = true;

isAdmin ? showAdminBar() : null // Is always needed to have the else value, even if we don't want to return nothing.
```

Another shorter way if we don't need the else value is: 

```javascript
const showAdminBar = () => console.log('Show admin bar')
const isAdmin = true;

isAdmin && showAdminBar() // This will check if the first condition is true or false, if true run the function, if false not.
```
**Intervals and Timers:**

- setTimeOut: is a methos that taskes two arguments:
   - a callback.
   - number of miliseconds to run it after.

```javascript
setTimeout(console.log('runnning'), 500)
```

```javascript
const farewell = () => console.log('bye')

console.log('hello')
setTimeout(farewell, 500)
console.log("I'm Sara") // This log will run before the setTimeout, this is why JS is synchronous, won't wait for that line.
```
- setInterval, takes the same arguments as setTimeout, the difference is that keep running over the amount of time passed in the second argument. Run a function repeatedly, starting after the interval of time, then repeating continuously at that interval.

- clearTimeout/clearInterval: in case we need to clean the timer. Just needs the reference saved in a variable:
```javascript
const interval = setInterval(() => console.log('bye'),  0,01)

clearInterval(interval);

```
 # Data Types *(Module 8)*
 
 ## Objects:
 
 Everything in Javascript is an object. An object allow us to group properties (keys and values).
 
 **Important:** Objects are used where the order of the properties does not matter. Usually is in the same order as you declare them but is not guaranteed. For example in a different browser could be order differently.
 
 To add a new property or overwrite an existing one in an object you can use
 1. The dot notation:
 
```javascript
const myObject = {
  name: 'Darren', 
  age: '35',
}

myObject.telephone = 123456789; 
myObject.age = 34;

```

2. Square backets:

```javascript
const myObject = {
  name: 'Darren', 
  age: '35',
  'cool': true, 
}

myObject['age'] = 34; // to reference a property with square backets we need to include strings.

// We can not use dot notation to manipulate the 'cool' prop, that's another case where we need square backets.
```

If you want to avoid changing values in an object you can use the `Object.freeze()` method:

```javascript
const myObject = {
  name: 'Darren', 
  age: '35',
}

const myFrozenObject = Object.freeze(myObject)

```

If we want to delete a property from the object we can use `delete`:

```javascript
const myObject = {
  name: 'Darren', 
  age: '35',
}

const deleteProp = delete myObject.name;
deleteProp // true
```

**Optional chaining:**

If we want to check if a key exists we can use question mark operator, this way it won't throw an error if the prop does not exist:

```javascript
const myObject = {
  name: 'Darren', 
  age: '35',
  telephone: {
    home: 123456,
    mobile: 987654,
  }
}

myObject?.telephone?.home // 123456.

```
