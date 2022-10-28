# Javascript Arrays:

Documntation for the [execute program](https://www.executeprogram.com/courses) Javscript Arrays methods.

## Content: 

1. [ForEach](#forEach)
2. [Stack](#Stack)
3. [Slice](#Slice)

## ForEach: 

Executes a function once for each element in an array

```javascript

const nums = [1, 2, 3];
let sum = 0;
nums.forEach(num => {
  sum = sum + num;
});
sum; // returns 6.
```

```javascript

const people = [
  {name: 'Cindy'},
  {name: 'Dalili'},
];

const names = [];
people.forEach(person => {
  names.push(person.name);
});

names; // ['Cindy', 'Dalili']
```

We can modify the array's elements during the forEach.

```javascript

const people = [
  {name: 'Ebony'},
  {name: 'Fang'},
];

people.forEach(person => {
  person.name = person.name.toUpperCase();
});

people[0].name; // 'EBONY'
```

The callback function can reference, and even modify, variables defined in outer scopes. In the next example, the callback function modifies the `result` variable.

The second argument to forEach's callback is the item's index.

```javascript


const names = ['Gabriel', 'Hana'];
const userIDs = [10, 11];

let result = '';
names.forEach((name, index) => {
  result += name + userIDs[index];
});

result; // 'Gabriel10Hana11'
```

Functions are values in JavaScript, so we can pass them in other ways as well.
For example, we can put the function in a variable, then pass the variable to forEach. 
The following examples define our forEach callback function in different ways, but they all have the same effect.

```javascript

let sum = 0;
const addToSum = n => sum += n;
[1, 2, 3, 4].forEach(addToSum);
sum; // 10;
```

## Practice
This function should return true when some of the numbers are positive. Currently it's broken: it always returns false. 
Modify the function by using the `sawPositiveNumber` variable already declared. Set it to true when a positive number is encountered. Then return it at the end of the `hasPositiveNumbers` function.

```javascript
function hasPositiveNumbers(numbers) {
  let sawPositiveNumber = false;
  numbers.forEach(n => {
    if (n > 0) {
      return true;
    }
  });
  return false;
};


[
  hasPositiveNumbers([]),
  hasPositiveNumbers([-2, -1, 0]),
  hasPositiveNumbers([-1, 0, 100]),
  hasPositiveNumbers([50]),
];

GOAL: [false, false, true, true]

```



**Hint**: We tried to return true inside the forEach callback. But the callback's return value is simply thrown away, so that doesn't work.



## Stack: 

We can add elements to the end of an array with **push**

```javascript
const a = [1, 2];
a.push(3);
a;

// Result: [1, 2, 3]
```

**push** returns the array's length, including the newly-pushed element.

```javascript
const a = ['a', 'b'];
a.push('c');

// Result: 3
```

**pop** is the opposite of push. It removes the last element from the array.

```javascript
const a = [1, 2, 3];
a.pop();
a;

Result: [1, 2];
```

**pop** returns the element that was removed.

If the array is empty, **pop** returns **undefined**, because there's nothing to remove. This mirrors the way that array indexing works: if we ask for any index of an empty array, we get undefined.

**push** and **pop** does not return a new array, instead they change the array itself each time they are called.

```javascript
const a = [1, 2, 3];
a.pop();
a.pop();
a;

Result: [1];
```

## Slice: 
Copying arrays is its most common use, however, sometimes we need to access to a part of an array. It takes an argument **begin**, which is the index to start from.

```javascript
[1, 2, 3, 4, 5].slice(3);

Result: [4, 5];
```

It can take a second argument, end. It slices all elements from begin up to end, but not including end.

```javascript
[10, 20, 30, 40, 50].slice(1, 3);

Result: [20, 30];
```

If the begin index is past the end oth array we get an empty result. 
For example if our array has indexes 0 and 1: [10, 20], what is in indexes 2 through 3? Nothing, so the slice of those indexes are empty:

```javascript
[10, 20].slice(2, 3);

Result: [];
```

With no arguments, will slice all elements of the array. This copies the original array, like this if you modify the copy the original array remains the same, and if you modify the original array the copy stays the same.

```javascript
const originalArray = [10, 20, 30];
const copy = orig.slice();
copy[0] = 1;
originalArray;

// Result: [10, 20, 30];
```
