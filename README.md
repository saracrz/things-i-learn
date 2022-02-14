# begining-javascript
Highlights from Wes Bos course - Beginner Javascript



## **The Tricky Bits** Module 3

**Closures**: is the ability to access to a parent level scope from a child scope, even after the parent function has been closure.
function sayHi(greeting = ''){
  return function sayName(name){
    return `${greeting} ${name}!`
  }
}

const myGreeting = sayHi('Hey');
console.log(myGreeting('Jerome'))
2.  Hoisting: Two things are hoisted in JS, which means are accesible even before you have declare them:
var variables.
regular functions (not anonymous function, like arrow functions)
Example:
sayHi(); // it logs 'hello'

function sayHI() {
   console.log('hello')
}
