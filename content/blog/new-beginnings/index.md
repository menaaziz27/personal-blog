---
title: Hoisting in javascript
date: "2020-12-21T23:46:37.121Z"
description: Hoisting in a very popular concept in javascript which every javascript developer should grasp it well.
---

# **Introduction**

Whenever you run your code, javascript parses it first before execution .. during the parsing phase the parser reads code line by line to check for any errors and stops execution if there's any, and if there's no errors javascript interpreter begins to move (hoist) all the functions and variables declaration to the top of our code .. so in this way we can use variables and function before declaring it in our code.

## _**So what is hoisting?**_

It's when javascript interpreter moves all the functions and variables declaration to the top of our code before execution, so regardless of whether their scope is global or local they are all moved to the top (the top of their scope).

<!-- when you run your code, javascript *parses* it first before excution. -->

<!-- *__Note:__*
Only the actual declaration is hoisted, and any initialization or assignment are left where they are. -->

#### Variable hoisting :-

- Using var </br>
- Using let and const </br>

### 1️⃣ Using _var_

```javascript
language = "javascript"

console.log(language)

var language
```

_output_

```javascript
javascript
```

Before execution javascript's interpreter hoist all variables declaration to the top of our code, and for **var** variables during compile phase it hoist the variable to the top of the code and initialize it to **undefined** .. this value lasts undefined untill the javascript interpreter hits the line of the assignment (evaluation) of the variable.

So keep in mind that javascript see the previous code during compile phase like this .. <br>

```javascript
var language = undefined

language = "javascript"

console.log(language)
```

_output_

```javascript
javascript
```

So let's see another example where javascript comes with unexpected output 😄

```javascript
console.log(language)

var language = "javascript"
```

_output_

```javascript
undefined
```

In this snippet, during the compilation phase javascript's interpreter hoists the 'language' variable to the top and initializes it with undefined, and before console.log() came before the actual initialization, javascript logs undefined to the console.

**So javascript see it like**

```javascript
var language = undefined // hoisted and auto initialized to undefined

console.log(language) // undefined

language = "javascript" // language = 'javascript'
```

So now if we tried to run the following

```javascript
console.log(language)

var language = "javascript"

console.log(language)
```

_output_

```javascript
undefined
javascript
```

As you might expect, the second log() function logs the actual value because during the excution, the interpreter hits the actual initialization before it logs the value to the screen.

the following snippet is gonna make it clear a bit

```javascript
console.log(myAge)

var myAge = 21

function foo() {
  var myAge = 44

  console.log(myAge)
}

foo()
console.log(myAge)
```

_output_

```javascript
undefined
44
21
```

again every variable declaration are getting hoisted to the top of their scope .. so the outer variable is getting hoisted to the top of its scope (global scope) and the inner variable is getting hoisted to the top of its scope (local function scope), so the first log is undefined because it's hoisted and auto initialized to undefined by the interpreter .. now after the execution of _foo_ function the inner variable is getting hoisted to the top of the function scope and initialized to 44 before logging it so it logs 44 to the console.
now the last line logs the value of the variable declared in its scope(in this case global scope) so it prints 21 on the screen.

### 2️⃣ Using _let and const_

```javascript
console.log(age)
let age = 21
```

```javascript
ReferenceError: Cannot access 'age' before initialization ❌
```

## **the question here, are let and const variables not hoisted?** 👀

the answer is they are getting hoisted too, but not initialized .. so that is the main difference between let and const vs var variables. So keep in mind that all varaibles are hoisted in javascript however var variables is getting initialized to undefined but let and const not initialized at all during compilation.

**let and const variables only get initialized when their evaluation during the runtime .. let's see how.**

```javascript
console.log(name)
let name
```

Error ❌

```javascript
ReferenceError: Cannot access 'name' before initialization
```

this example clarify how javascript behaves during the compilation of let variables, it hoists the variable but never initialize it during the compilation phase, so during the runtime javascript don't recognize the variable and throws an error.

so let's try the reverse ..

```javascript
let name
console.log(name)
```

_output_

```javascript
undefined
```

so now you know that during the compilation phase **let** is hoisted but never initialized, so in the execution phase the interpreter initializes **let** variables to undefined (until it's evaluated to its actual assignment in the program).
that's why it logs _**undefined**_.
_So during the compilation phase it's hoisted but not initialized & during the execution phase let is initialized to undefined if there's no assignment statement reached by the interpreter_.

### **it differs a bit in the case of const**

the difference between let and const is during the execution phase .. when **let** being initialized to undefined however const throws an error and never initialized by the interpreter.

```javascript
const x;
console.log(x)
```

Error ❌

```javascript
Missing initializer in const declaration
```

Here javascript hoist const variable during compilation, but in the execution phase when the interpreter hits the declaration statement '**const x;**' it never initialize it .. that's why it throws an error when we try to log its value.

Ok, that's it for this blog, hopefully I could help 😄
Thank you for reading!
