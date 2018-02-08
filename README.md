![cf](https://i.imgur.com/7v5ASc8.png) 02: Scope, Context, and Functional Array Methods
======

## Resources
* JavaScript Scope and Context
  * [MDN: Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
  * [MDN: var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
  * [MDN: let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
  * [MDN: function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
  * [MDN: arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
* Functional Array Methods
  * [MDN: Array.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
  * [MDN: Array.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
  * [MDN: Array.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
  * [MDN: Array.reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

## Submission Instructions
* Work in a fork of this repository
* Work in a branch on your fork
* Write all of your code in a directory named `lab-` + `<your name>` **e.g.** `lab-susan`
* Open a pull request to this repository
* Submit on canvas a question and observation, how long you spent, and a link to your pull request

## Feature Tasks
### Scope and Context
Given the code blocks below, answer the set of questions below. Please copy the
questions to your lab directory in a file called `ANSWERS.md`.

Explain how hoisting allows the `printGreeting` function to be called before
where it's actually written in the file.

```js
printGreeting();

function printGreeting() {
  console.log("isn't JavaScript wonderful?");
}
```

Explain why this function called `printGoodbye` can't be executed until after
it's actually written in the file.

```js
printGoodbye(); // this one won't execute!

const printGreeting = () => {
  console.log("That's all, folks!");
}

printGoodbye();
```

### Implement forEach/map/filter/reduce
Manually implrement the functional programming functions `.forEach`, `.map`,
`.filter`, `.reduce`. Put them in one module called `fp` that you can import
and use in other modules.

#### Function Descriptions
* `.forEach` - executes a function for each item in a collection. Returns nothing.
* `.map` - turns one list into a new list by passing each element through
  the callback function and saving each result in the new list.
* `.filter` - takes all the elements in a list and returns a new list
  filtered down to only elements that pass some test defined by the
  callback function.
* `.reduce` - takes all the elements in a list and reduces them down
  to a single value, starting from some initial value.

#### FP Module
Create a NodeJS module in the `lib/` directory named `fp.js` that exports an
object.

* Create functions called `forEach`, `map`, `filter`, and `reduce`.
* Each function should accept two parameters:
  * An array of elements
  * A reference to a callback function
  * (`reduce` actually accepts an additional parameter too.)
* Define each function using ES6 lexical arrow function syntax.
* Do not use any third party librarys in the FP module.

```js
// array: an array of elements
// cb: a callback function
const myFunction = (array, cb) => {

}
```

* `fp.forEach` should have the function signature `(array, callback) => undefined`
* `fp.map` should have the function signature `(array, callback) => Array`
* `fp.filter` should have the function signature `(array, callback) => Array`
* `fp.reduce` should have the function signature `(array, callback, initialState) => value`

## Testing
#### FP Module Tests
Create a NodeJS module in the `test` directory named `fp.test.js` that
asserts the correctness of the fp module.

* Use Behavior-driven Development `describe` and `test` methods to define
  descriptive tests and increase readablity
* Each `test` callback should aim to test a small well defined feature of a function
* Write tests to ensure the fp module functions returns the correct results
  when invoked with valid arguments

#### Example Usage
```js
const array = [1, 2, 3, 4, 5];
fp.forEach(array, el => console.log(el)); // prints 1 2 3 4 5 across many lines
    fp.map(array, el => el * 2);          // returns [2, 4, 6, 8, 10]
 fp.filter(array, el => el % 2 === 0);    // returns [2, 4]
 fp.reduce(array, (a, b) => a + b, 0);    // returns 15
```

#### Example: Wait, What Does Reduce Do?
Reduce a list of numbers to one number representing their sum. Start a
running value at 0. Now continually add each single number to the running
value. It all reduces down to one number: the total sum of all the numbers
together.

```js
let numbers = [1,2,3,4,5];
let sum = fp.reduce(numbers, (runningValue, number) => runningValue + number, 0)
```

Reduce a budget and a collection of expenses down to how much money is left
by starting a running total equal to the budget, then continually subtracting
each budget item from the running total. The list of expenses reduces down to
just one number: the money left in the budget.

```js
let beginningBudget = 100;
let expenses = [12, 43, 18];
let budgetRemaining = fp.reduce(expenses, (remainingBudget, singleExpense) => {
  return remainingBudget - singleExpense
 }, beginningBudget)
```

