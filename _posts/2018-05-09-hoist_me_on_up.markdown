---
layout: post
title:      "Hoist Me On Up"
date:       2018-05-09 20:21:28 -0400
permalink:  hoist_me_on_up
---


Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (whether that be global or local). 

In my previous blog post, I talked at length about the different types of variables (`let`, `var`, and `const`), how each behaves, and the different types of scope. Read that post [here](https://mbalsamo2.github.io/scopin_for_variables) to make sure you have a good understanding of the types of variables before trying to understand hoisting.

So as I said above, hoisting is this slightly weird thing that JavaScript does that moves your variables declarations to the top of it's scope. The reason behind why this is happens is because of JavaScripts two-phase engine nature. JS engine does a once over of your code during the "compilation" phase which stores declarations and invocations in memory. When the JavaScript engine goes over your code the second time during the "execution" phase, it then reads through your code line by line, as you would hope. However, because of this two phase nature, variables always appear declared before they are assigned. This is what it means by "hoisting". Your variables are "brought to the top" of the scope because of the first phase. Notice I put "brought to the top" in quotes, because in actuality, your variables are not moved at all, it's just that some of your code is evaluated before other parts. 

```
function waterBottle() {
  return "It's a Nalgene";
}

// compilation phase
waterBottle();

// execution phase 
function waterBottle() {
  return "It's a Nalgene";
}
```

Now this might not sound that bad, but it can create some weird outcomes depending on where you declare/assign your variables within your code. Because of this nature, it is important to always declare and assign your variables at the top of its scope.

```
function danceMoves () {
  console.log(twist);
 
  var twist = 'I'm twisting!';
 
  return twist;
}
 
danceMoves();
// LOG: undefined
// => "I'm twisting!"
```

In this example, you will see that the console logged out undefined. This is because even though the JS engine stored the variable declaration `twist` in its memory during the compilation phase, it does not know about the value it was assigned ("I'm twisting!"), until the execution phase. Because of this, when you attempt to `console.log(twist)`, that variable has yet to be assigned since it comes before the variable declaration/assignment line of code. However, we are able to return the value of `twist` at the end of the function because once we get to the return line at the end of the function, `twist` has already been declared and assigned.    

So as I said above, the best way to avoid this type of behavior is to declare/assign your variables at the top of it's scope. In the case of the above example we would just have to move around the one line of code to become:

```
function danceMoves () {
  var twist = 'I'm twisting!';
	
	console.log(twist);
 
  return twist;
}
 
danceMoves();
// LOG:  "I'm twisting!"
// => "I'm twisting!"
```

By declaring and assigning the variable at the top of its scope (in this example it would befunction or local scope, so at the top at the function) we can now `console.log(twist)` and `return twist`.

The real issue here, however, is once again `var`. As I stated in my previous post, `var` gives programmers a little too much power without any consequences (aka errors). The problem with `var` in the first example is that it allowed us to use the variable before it was defined. If we use `const` or `let` in that example instead of `var`, then we will get a meaningful error instead of logging out `undefined`.

```
function danceMoves () {
  console.log(twist);
 
  let twist = 'I'm twisting!';
 
  return twist;
}
 
danceMoves();
// ReferenceError: twist is not defined
```

`const` and `let` fix the issues we have when `var`, so besides always declaring and assigning your variables at the top of their scope, always avoid using `var` whenever possible!
