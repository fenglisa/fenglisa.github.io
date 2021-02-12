---
layout: post
title:      "Back to Basics: JS"
date:       2021-02-12 19:08:29 +0000
permalink:  back_to_basics_js
---

### A second look at scope and hoisting


I recently earned the JavaScript assessment badge on LinkedIn, but going through it prompted me to take a closer look at some concepts that I didn't feel like I had a solid grasp on. Let's talk about **scope**.

But first, let's talk variables. We have `var`, `let`, and `const` in JS. `var` is function-scoped while `let` and `const` are block-scoped (more on that in a bit). `var` and `let` allow for reaasignment while `const` cannot be reassigned. However, unlike `var`, `let` cannot be redeclared. For example:
```
var greeting = "say Hi";
var greeting = "say Hello instead";
```
will result in `greeting` == "say Hello instead".

```
let greeting = "say Hi";
let greeting = "say Hello instead";
```
will result in "Uncaught SyntaxError: Identifier 'greeting' has already been declared" and `greeting` == "say Hi".

Since I started learning JS post-ES6 era, I was highly encouraged to never use `var` in my code and I didn't look too closely into why. Because I was so accustomed to just working with block-scoped variables, when the LinkedIn assessment posed questions using `var` instead of `let`, I knew something was up. 


##### Let's revisit scope. 
In the previous example using `let`, if the same variable was declared *in different scopes*, it would be considered two different variables and there would be no error. Remember that `let` is *block-scoped*, so that means the variable just needs to be declared in different *blocks* { }. 

**With `let` :**
```
let greeting = "say Hi";
   if (true) {
        let greeting = "say Hello instead";
        console.log(greeting)
    }
console.log(greeting)
```
results in the console logging:
```
say Hello instead
say Hi
```

However, since `var` is *function-scoped*, it is accessible and *redeclarable* anywhere within the function (or global scope if not within a function), regardless of which block it was declared in.

**With `var` :**
```
var greeting = "say Hi";
   if (true) {
        var greeting = "say Hello instead";
        console.log(greeting)
    }
console.log(greeting)
```
results in the console logging:
```
say Hello instead
say Hello instead
```

##### Hoisting
Even though all variable declarations are *hoisted*("moved" to the top of their scope before execution), only `var` is initialized with a value (== `undefined`) during the compilation phase. That means any attempt at using a `let` or `const` variable before it is declared will be met with a Reference Error. 

**With `let` :**
```
console.log(greeting)
let greeting = "say Hi";
```
results in ReferenceError:  greeting is not defined

**With `var` :**
```
console.log(greeting)
var greeting = "say Hi";
```
results in the console logging:
```
undefined
```
Because `var` is accessible and does not throw an error in this scenario, code using `var` will sometimes behave in unexpected ways and will be more susceptible to bugs down the road. 

All this to say, I clearly see why `let` and `const` are the more preferred declarations and I want to thank the developers who made this change happen!






