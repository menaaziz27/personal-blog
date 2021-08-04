---
title: What the heck is optional chaining in javascript ?
date: "2021-04-02T23:46:37.121Z"
description: The optional chaining operator (?.) enables you to read the value of a property located deep within a chain of connected objects without having to check that each reference in the chain is valid.
---

So I came up with an interesting javascript feature today and wanted to share it with y'all!

## the chaining operator (?.)

this operator provides a way to simplify the referencing to a property of a nested object when it's possible that this property may be undefined or null.

### alot of theory ? let's dive into examples

```javascript
let nestedObject = {
  name: "whatever",
  firstObj: {
    getHere: "can you reach me ?",
  },
}

let nestedProperty = nestedObject.firstObj && nestedObject.firstObj.getHere
console.log(nestedProperty)
// expected output: can you reach me ?
```

Here we're checking of the existence of the property (**firstObj**) first and if it exists the right hand would be evaluated, hence the nestedProperty would be the value of (**getHere**) property.
So that was without the chaining operator and it's kinda painful .. let's see what it looks like with our chaining operator.

```javascript
let nestedObject = {
  name: "whatever",
  firstObj: {
    getHere: "can you reach me ?",
  },
}

let nestedProperty = nestedObject?.firstObj?.getHere
console.log(nestedProperty)
// expected output: can you reach me ?
```

As you noticed it evaluates the same result .. so you should read the expression from left to write as "is there any object calls **nestedObject** ? if there's, check please if it has a nested property called **firstObj** ? and if exists return me the **getHire** value and if not return me **undefined** " so with the operator we type a less of code, clean and readable lines .. notice that of there's no **nestedObject** it will return immediately **undefined** and the rest of the expression is not gonna be evaluated.

## let's see the previous example without the operator

```javascript
let nestedObject = {
  name: "whatever",
  firstObj: {
    getHere: "can you reach me ?",
  },
}

let nestedProperty
if (
  nestedObject.firstObj.getHere !== null ||
  nestedObject.firstObj.getHere !== undefined
) {
  nestedProperty = nestedObject.firstObj.getHere
}
```

this snippet behaves the same as it's previous one .. but here we're typing a lot of code and there's some repetitions.

## optional chaining with function calls

If we used the operator with function that is not exists the expression immediately return **undefined**.

```javascript
let course = {
  professor: "Dawn",
  category: {
    name: "development",
    details: {
      showName: function () {
        console.log(course.category.name)
      },
    },
  },
}
let undefinedValue = course.category?.details?.NotExistingFunction?.()
console.log(undefinedValue)
// expected output: undefined
```

we're checking the **_course_** object if it has **_category_** property ? if yes check for the **_details_** prop if yes check for the **_NotExistingFunction_** and because it's not exist the expression returns undefined.

## What if there's a property with the same name of the function ?

```javascript
let course = {
  professor: "Dawn",
  category: {
    name: "development",
    details: {
      showName: "it's a web development course!",
    },
  },
}
let undefinedValue = course.category?.details?.showName?.()
console.log(undefinedValue)
// exprected output: TypeError: course.category?.details?.showName is not a function
```

In this case a _TypeError_ exception will be raised.

Well, that's it for this article 😄
for more info [check MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
