**For Each**: 

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
