---
layout: post
title:      "Preventing Defaults Left and Right"
date:       2018-05-04 20:01:45 +0000
permalink:  preventing_defaults_left_and_right
---


So I know I say this every time I begin a Portfolio Project, and you would think by the 4th project I would assume that I am going to be pushed way outside my comfort zone and challenged to the point where finishing the project seems impossible, but then there always appears a small light at the end of tunnel when the flow of a project starts to click and you know you can finish this thing.

The "light at the end of the tunnel" appeared for me after exhausting the alotted Project 1:1's, attending numerous Project Prep and Jquery/AJAX related study groups, and skimming enough Stack Overflow Questions to publish a novel. Bottom line, this was a tough project. 

I think part of the reason I struggled with this project was because when I read through the description of the project and I saw that I would be building off my Rails App, I was relieved. I knew my Rails App Portfolio Project inside and out and I was happy to revisit familiar code. 

However, after closer investigation of the requirements for the project, I soon found out that adding Jquery front end to my rails app is essentially gutting my rails app of all the regular user flow and writing JavaScript functions that get my rails app to render the same content without a page refresh. 

Writing the skeletal code of each function is honestly easy. You know at some point you are going to have to: 
```
$('some_tag').on('submit', function(e) {
e.preventDefault();
}
```
This is bare bones the beginning of each function when you are trying to change what the rails app is currently doing (preventing the default action) and then within the function body, you then have to figure out what you would like to be happening instead. This could be listing out an index that normally is presented on a different page, submitting a form without a page refresh, or being able to click through each show page of an object. 

So as I said, the beginning of each function is easy. It's all the code in the middle and on the outside that made this project tough. 

My first issue I faced was not being able to hijack any buttons even though I had the `e.preventDefault();`. After doing some Stack Overflow reading, I found out this is due to turbolinks causing some things to load while not reloading other aspects of your code. To combat this issue I did the following:
```
$(document).on('turbolinks:load', function() {
  bindEventListeners();
})

function bindEventListeners() {

all of my js functions...

}
```

I had to use this in replacement of `$(document).ready`, and it fixed the ability to hijack links. 

While I faced many other issues and bugs throughout the project, I found that searching for similar issues online and looking through other finished projects code to be the most hopeful as I worked though these problems. This was by far the hardest project for me to date, but it was also the project in which I learned the most from. 

Check out my code [here!](https://github.com/mbalsamo2/best_dog_parks/tree/jquery)

React and Redux, here I come!

