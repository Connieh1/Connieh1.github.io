---
layout: post
title:      "Using Fetch in a Javascript SPA"
date:       2020-07-22 23:34:02 -0400
permalink:  using_fetch_in_a_javascript_spa
---


In my Javascript Single-Page Application, this-happened, I made two "GET" fetch requests and one "POST" fetch request. It is a simple application where users can submit posts in a variety of subjects.

The posts 'get' fetch request is structured as follows:

```
function getPosts(){
  fetch(url)
  .then(response => response.json())
  .then(posts => {
    posts.data.forEach(post =>{
      let newPost = new Post(post, post.attributes)
      document.querySelector('#post-container').innerHTML += newPost.renderPostCard();
      })
    })
	}
```


Alternatively:

```
function getPosts(){
  fetch(url)
  .then(function(response){
    return response.json()
  }).then(function(posts){
    console.log(posts);
    posts.data.forEach(post =>{
      let newPost = new Post(post, post.attributes)
      document.querySelector('#post-container').innerHTML += newPost.renderPostCard();
    })
  })
}
```


The posts "post" fetch request is structured as:

```
function postFetch(title, description, subject_id){
  fetch(url, {
    //Post request
    method: "POST",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify({
      title: title,
      description: description,
      subject_id: subject_id
    })
  })
  .then(response => response.json())
  .then(post => {
    const postData = post.data
    let newPost = new Post(postData, postData.attributes)
    document.querySelector('#post-container').innerHTML += newPost.renderPostCard();
  })
}
```

Javascript fetch requests have evolved from XMLHttpRequests, and makes loading data from the server without reloading the page easier. A fetch returns a promise, which contains a response. If all goes well, you will have some data that you may then access, based on how it is structured. If not, you will be presented with a nice error! I really enjoy using js fetch, and plan to get quite a bit more practice using it. 


This project has been fun, and has a lot of room for growth. I may revisit it someday.

[this-happened](https://github.com/Connieh1/this-happened-frontend)

