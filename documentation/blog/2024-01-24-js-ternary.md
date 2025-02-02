---
title: How to Use the JavaScript Ternary Operator
description: We expound on the use of JS Ternary Operator with examples of what it is, how it works and discuss the best practices.
slug: javascript-ternary-operator
authors: abdullah_numan
tags: [javascript]
image: https://refine.ams3.cdn.digitaloceanspaces.com/blog/2022-11-15-js-ternary/social.png
hide_table_of_contents: false
---

**_This article was last updated on January 24, 2024 to add more detailed information and implementation of JavaScript Ternary Operator_**

## Introduction

This post is about the Ternary Operator in JavaScript. We discuss what the ternary operator is and how it works. We go over some examples demonstrating when and why to use it and how it compares to other JavaScript control structures like `if/else`, `if/else if/else` and `switch`. We also learn about some of the best practices while using JS Ternary Operator.

Steps we'll cover:

- [What is JavaScript Ternary Operator ?](#what-is-javascript-ternary-operator-)
- [How JS Ternary Operator Works](#how-js-ternary-operator-works)
  - [What are Truthy/Falsy Values ?](#what-are-truthyfalsy-values-)
- [When to Use the JS Ternary Operator ?](#when-to-use-the-js-ternary-operator-)
  - [JavaScript Ternary Operator: A Shorthand for `if/else`](#javascript-ternary-operator-a-shorthand-for-ifelse)
  - [Using the JavaScript Ternary Operator to Test a Function's Truthiness](#using-the-javascript-ternary-operator-to-test-a-functions-truthiness)
  - [Handling Nullish Values with JS Ternary Operator](#handling-nullish-values-with-js-ternary-operator)
  - [JavaScript Ternary Operator: When The Return Value Rules](#javascript-ternary-operator-when-the-return-value-rules)
  - [Chaining Ternary Operators in JavaScript](#chaining-ternary-operators-in-javascript)
- [JavaScript Ternary Operator Best Practices](#javascript-ternary-operator-best-practices)

## What is JavaScript Ternary Operator ?

The Ternary Operator in JavaScript is a conditional control structure that checks for the return value of an expression and executes a block of code based on whether the value is truthy or falsy. It then returns the return value of the executed block.

The JavaScript Ternary Operator is also referred to as the Conditional Operator.

## How JS Ternary Operator Works

The Ternary Operator in JavaScript is denoted by the question mark: `?`. It is called so because it takes three operands:

1. The conditional expression that returns either `true` or `false` based on a check that evaluates to either [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) or [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).
2. The block of code which should be executed if the conditional check returns `true`.
3. The block that should run if it returns `false`.

The syntax for the JavaScript Ternary Operator looks like this:

```ts
conditionalExpression ? exprIfTruthy : exprIfFalsy;
```

As we can see, the Ternary Operator places the conditional expression before the `?` and accepts the executable expressions as two other operands that are separated by a colon, `:`.

If the `conditionalExpression` evaluates to a truthy value, `exprIfTruthy` is executed. If it evaluates to a falsy value, `exprIfFalsy` is executed.

### What are Truthy/Falsy Values ?

In JavaScript, a **truthy** value corresponds to a value that is considered equivalent to `true` had that been converted to a Boolean. This is another way of saying "this thing exists". All values in JavaScript are truthy if they do not evaluate to or are not defined to be **falsy**.

A falsy value is a value that is casted as `false` when it is converted to a Boolean. In JavaScript, the following values are coerced / converted to `false`:

`false`, `0`, `-0`, `0n` `""`, `null`, `undefined`, `NaN` and `document.all`.

Expressions that evaluate to anything other than these are considered **truthy**.

## When to Use the JS Ternary Operator ?

We use the JavaScript Ternary Operator when we need to control execution flow between two paths based on a conditional check that returns a Boolean.

A simplest example involves testing the value of an expression stored in a variable to see whether it exists or not, and then pursue an execution path based on the outcome. If it exists, we do relevant stuff and return it; if not, do some other relevant stuff and return that. The below code shows how:

```ts
// Example

const student = "Abd";
const welcomeStudent = student ? `Welcome, ${student}!` : "Welcome, Guest!";

console.log(welcomeStudent); // Welcome, Abd!
```

In the above snippet, `student ?` tests to see if `student` is truthy. The value from this conditional test is used to decide the value of the stored variable, `welcomeStudent`. In other words, we are using the conditional operator to control the value of `welcomeStudent` based on the value of `student`.

Notice that the return value of the executed block following the check is returned as the operator's return value. That allow us to store it in `welcomeStudent`.

### JavaScript Ternary Operator: A Shorthand for `if/else`

The Ternary Operator is a concise alternative to `if/else`. For example, we could have written the above control flow like this:

```js
const student = "Abd";
let welcomeStudent;

if (student) {
  welcomeStudent = `Welcome, ${student.name}!`;
} else {
  welcomeStudent = "Welcome, Guest!";
}

console.log(welcomeStudent); // Welcome, Abd!
```

Notice how the ternary operator used previously helped avoid using the above procedural `if/else` flow. The Ternary Operator made the code more readable, reusable and the logic easier to follow.

### Using the JavaScript Ternary Operator to Test a Function's Truthiness

The ternary operator can also be used when we need to test the return a value of a function. As in the `welcomeStudentTernary` function below:

```ts
// With if/else
const welcomeStudent = (student) => {
  if (student) {
    return `Welcome, ${student}!`;
  } else {
    return "Welcome, Guest!";
  }
};

console.log(welcomeStudent("Abd")); // Welcome, Abd!
console.log(welcomeStudent("")); // Welcome, Guest!
console.log(welcomeStudent(null)); // Welcome, Guest!

// With ternary operator
const welcomeStudentTernary = (student) => (student ? `Welcome, ${student}!` : "Welcome, Guest!");

console.log(welcomeStudentTernary("Abd")); // Welcome, Abd!
console.log(welcomeStudentTernary("")); // Welcome, Guest!
console.log(welcomeStudentTernary(null)); // Welcome, Guest!
```

Again, it provides conciseness. And goes well with arrow functions.

### Handling Nullish Values with JS Ternary Operator

Notice how the nullish arguments are being considered in both cases. With just a few characters added, the Ternary one-liner offers more convenience to an efficient developer who doesn't want to waste lines for dealing with nullish logic.

### JavaScript Ternary Operator: When The Return Value Rules

It is important to notice that with the Ternary Operator, we are only interested in the return value of the conditional check as well as those of the two execution blocks. Side effects are less important.

For example, the Ternary Operator would not be useful for us had being polite or yelling was important to us:

```ts
const welcomeStudent = (student) => {
  if (student) {
    console.log("First YELL!");
    return `Welcome, ${student}!`;
  } else {
    console.log("Be composed and polite.");
    return "Welcome, Guest!";
  }
};

console.log(welcomeStudent("Abd"));
// "First YELL!"
// Welcome, Abd!
console.log(welcomeStudent());
// "Be composed and polite."
// Welcome, Guest!

// With ternary operator
const welcomeStudentTernary = (student) => (student ? `Welcome, ${student}!` : "Welcome, Guest!");

console.log(welcomeStudentTernary("Abd")); // Welcome, Abd!
console.log(welcomeStudentTernary("")); // Welcome, Guest!
```

In the case when they are more important, we should be using `if/else` statements, as in `welcomeStudent`. So, the JavaScript Ternary Operator is useful in cases when the return value of the expressions matter more. This is a major distinction between the usage of `if/else` and the Ternary operator in JavaScript.

### Chaining Ternary Operators in JavaScript

We can chain ternary operators to emulate a `if/else if/else` control structure or a `switch` statement:

```ts
// With if/else if/else
const grade = (mark) => {
  if (mark > 100) {
    return;
  } else if (mark > 80) {
    return "A";
  } else if (mark > 70) {
    return "B";
  } else if (mark > 60) {
    return "C";
  } else if (mark > 50) {
    return "D";
  } else {
    return "F";
  }
};

console.log(grade(100)); // A
console.log(grade(1000)); // undefined
console.log(grade(10)); // F

// With chained ternary operators
const grade = (mark) =>
  mark > 100 ? undefined : mark > 80 ? "A" : mark > 70 ? "B" : mark > 60 ? "C" : mark > 50 ? "D" : "F";

console.log(grade(100)); // A
console.log(grade(1000)); // undefined
console.log(grade(10)); // F
```

Here, we chained an additional conditional operator into the third operand at each level.

## JavaScript Ternary Operator Best Practices

Many developers do not prefer chained ternary operators like the one above because multiple conditional checks hurt readability and maintainability. Instead of chaining ternary operators, using plain `if/else if/else` or `switch` statements are recommended when there are multiple paths in a control flow.

So, here are some best practices:

- Use the JavaScript Ternary Operator when there are only two paths in the control flow.
- Use the JS Ternary Operator consistently.
- Avoid using chained Ternary Operators as they make the code difficult to read and maintain.
- Use a JavaScript Ternary Operator with arrow functions as they also produce good one-liners.
- In the case complex conditional checks are involved, use parentheses to properly implement the logic. This also improves readability and maintainability

## Summary

In this post, we expounded on the use of the Ternary Operator in JavaScript. We acknowledged its importance in writing concise code, especially in situations that involve a conditional check and two execution paths.

We saw with examples that the JS Ternary Operator is a good alternative to `if/else` and is preferable when the return values of the expressions matter more than side effects. We covered a case where it is useful for storing the value returned from evaluating primitives across the execution path as well as one where the same is done after executing a function.

We also encountered an example that shows JavaScript Ternary Operators can be chained to emulate `if/else if/else` and `switch` blocks, but the recommended way is to avoid chaining multiple Ternary Operators. We learned about other best practices such as using it consistently in situations where there are only two paths in the control flow, with arrow functions and with parentheses when needed.
