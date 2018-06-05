---
layout: post
title:      "Reactin' to this Redux"
date:       2018-06-05 14:26:56 -0400
permalink:  reactin_to_this_redux
---


Whoa. 

I think everything up this point was honestly childs play in comparison to this project. It is the final project for a reason. It was by far the project that required the most Project 1:1's, study groups, google searches, and just time. Time that was necessary to figure out what state really is and how to access components within containers. Time to get my Raills API and React Frontend to be playing nicely together. Just, lots of time. 

It took me a few days to just get my fetch request to send ANY information back from my API. Turns out setting up your database correctly is important, it's even more important to understand what is needed within a fetch request. For example:

```
export function submitBook(formContent) {
  return (dispatch) => {
    dispatch({ type: 'SUBMITTING_BOOK' });
    return fetch(`http://localhost:3001/books`, {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({book: formContent})})
      .then(resp => resp.json())
      .then(book => dispatch({ type: 'SUBMIT_BOOK', book: book}))
  }
}

```

This is the fetch request I used to submit a newly created book. The ```dispatch({type: 'SUBMITTING_BOOK'})``` is telling the store that it will be receiving information shortly, and to basically get ready. The fetch request itself accesses my BooksController to actually create the new book. It took quite a while for me begin to understand how my rails API and React were interacting but this is one of the BIG points of contact. Within my fetch request I have to specify that this is a POST request, because I am wanting to create a new object, not just retrieve already created data. The ``` body: JSON.stringify({book: formContent})})``` is the code that tells the request request to send the information at JSON. 

And of course we have a couple of ```.then``` which are necessary because of the asynchronous nature of JavaScript. I need to wait until the fetch request is able to complete before telling the request that what I want back is JSON, and also to then access my bookReducer to work with the data it is receiving. 

So as you can see, there is a lot of knowledge that is wrapped up in just a few lines of code. Traveling through the (what seemed like) endless files to figure out how each file was talking to every other file was easily the toughest part of this project, but I think I am finally starting to get a better grasp of the React, Redux flow.

While my project isn't too flashy yet, I can honestly say I am proud of what is it. I am even more excited to continue to add more components (users, authentication, genres, and more).
