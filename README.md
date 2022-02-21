# begining-javascript
Highlights from Wes Bos course - Beginner Javascript



## **The Tricky Bits** *(Module 3)*

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

## **The DOM** *(Module 4)*

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
- .addEventListener('click', toggleRound) or .addEventListener('load', fucntion() {console.log()pic.naturalWidth} -> This event WILL WAIT UNTILL THE PIC IS LOADED.)
- .contains('yourClassName')

**Attributes**:
Anything provided to an element as additional info, ex: class='your-class' or src='your-path.html'.
They act most of them as getters and setters.


