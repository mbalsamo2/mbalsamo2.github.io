---
layout: post
title:      "Scopin' for variables"
date:       2018-05-09 19:00:41 -0400
permalink:  scopin_for_variables
---


To quote a Flatiron School Lesson:
> Scope is a ubiquitous concept in programming and one of the most misunderstood principles in JavaScript, frustrating even seasoned engineers. Not understanding how scope works will lead to pain.

So it may come as no surprise that after completing the JavaScript curriculum, I still didn't have quite the grasp I would have hoped to have on scope.

In short, scope is how accesible a variable is. In JavaScript there is local and global scope. 

Before getting too deep into scope, you also have to make sure you understand the types of variables.

 `var` was the original way to declare a variable, but as JavaScript grew, so did the bugs that lerked with var. `var` allows you to reassign and redeclare a variable as many times as you like:
 
 ```
 var bob = 'friend';
 
 var bob = 'enemy';
 ```
 
Here we declared a variable bob twice and assigned it different values, but no error will be thrown. 

`var` also allows a programmer to declare a variable without assigning it a value. 

```
var tomorrow;

tomorrow = "Thursday";
```


To combat these issues, JavaScripters created `const` and `let`. `let` is similar to `var` in way you can still declare a variable without assigning it a value, and you can also change the value of the variable, however, you can only declare a variable with `let` once:

```
let dog = "Mowgli";
 
dog = "Lucy";

let dog = "Lola";
 //=> Uncaught SyntaxError: Identifier 'dog' has already been declared
 ```
 
 `const` on the other hand does not allow a programmer to reassign the variable, and the variable has to be assigned at the time of the declaration:
 
 ```
 const iceCream;
 //=> Uncaught SyntaxError: Missing initializer in const declaration
 
 const iceCream = "Chocolate Chip";
 
 iceCream = "Peanut Butter"
 //=> Uncaught TypeError: Assignment to constant variable.
 ```
 
 Ok, so now we have a better grasp on the types of variables...but what about scope?
 
 So we have global scope which is when variables are assigned outside of a function:
 
 ```
 var movie = "Black Panther";
 
const cereal = "Cheerios";
 
 let weather = "Sunny";
 
 movie;   // "Black Panther"
 cereal;   // "Cheerios"
 weather; // "Sunny"
 ```
 
 However, once we declare variables inside of a function, their scope is no longer global, it is "function scope" or "local scope" it has scope that is local to that function.
 
 ```
 function tomorrow() {
  const outside = "rainy";
 }
 
 outside;
 // Uncaught ReferenceError: outside is not defined
 ```
 
 Now at first you may be confused because clearly you declared and assigned the variable `outside` but since it's scope is local, within the function, you can only call on that variable within that function. Once you are outside the function, you are back within global scope land and do not have access to that variable. 
 
If we wanted to return "rainy" we would have to return the variable within the function, and then invoke the function:

```
  function tomorrow() {
   const outside = "rainy";
	 return outside
 }
 
tomorrow();
 // "rainy"
 ```
 
 The one caveat is when you forget to delcare your variables with `const`, `let`, or `var`. If you do this, then regardless if your variable is inside a funciton or not, the scope if global.
 

