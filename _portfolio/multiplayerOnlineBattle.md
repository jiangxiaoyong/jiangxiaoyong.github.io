---
title: "Multiplayer Online Battle"
excerpt: "Online battle game build by clojure in functional reactive programming"
date: 2017-01-20
header:
  overlay_color: "#333"
  teaser: /jchat/jchat-chat-page.png 

gallery:
  - url: /jchat/jchat-home-page.png
    image_path: /jchat/jchat-home-page.png
    alt: "placeholder image 1"
  - url: /jchat/jchat-signup-page.png
    image_path: /jchat/jchat-signup-page.png
    alt: "placeholder image 2"
  - url: /jchat/jchat-chat-page.png
    image_path: /jchat/jchat-chat-page.png
    alt: "placeholder image 3"
    
tags: 
  - clojure
  - clojurescript
  - functional programming
  - reactive programming
  - FRP
  - HeroKu
---

## Motivation

Chatting software are so popular today benefited from fast growing internet technologies.
It's a good try to create a chatting software for my family, my friends and me, without worry some issues like
service availability and message security. So that's why I start to create this chatting web app and take is as good opportunity to explore, learn and practice
some current interesting technologies at 2016. My understanding of software structure and programming skill are deepened and improved by create this project.

## Project Description

It's a full stack real time chatting web app that enable chatting between multiple users, storing chatting history and adding friends.
The functionalities are similar to Facebook messenger in terms of user experience.
Here is the [live demo](https://www.google.com/) and [Github Repo](https://github.com/jiangxiaoyong/JChat) 

{% include gallery caption="Screenshots of welcome page, signup page and chatting page." %}

## Project Features
This chatting web app supporting following features:

* Enabled chatting between multiple friends
* Enabled caching both online and offline chatting records
* Enabled adding friend by user email address
* Enabled showing alert of unread message
* Enabled signup and signin
* Enabled authentication by username and password
* Enabled password encryption

## Project technologies stack and use cases
The technologies used by creating this web app and corresponding usage as described below:

### Front end
  * React.js
      * create stateless components of user interface, and compose them to form lager complicated component 
  * Redux
      * Predictable state container for react.js stateless components and manager data flows and propagation of change of entire front end web client
  * webpack
      * A module bundler and automation of task runner. It provides codebase splitting into an on demand loaded chunks 
        ,extracting common shared chunk, converting ECMAScript 6 syntax into cross browser compatible format and hot module replacement for this web app
  * ECMAScript 6
      * It provides many syntax sugar and modules feature to organize modules and their dependencies
  
### Back end
  * Node.js
      * Served as http server and handle websocket connections via javascript library Socket.io
  * Redis
      * A high performance NoSQL in-memory data structure store, it is used as PUB/SUB messages broker, and cache of messages and session
  * MongoDB
      * A document-oriented NoSQL to store user information, like username, password, email address and friends list 
  
### Development and deployment
  * Docker
      * A super easy to use contianerization platform to build, ship and run web app. This web app use total three containers, one container for
      each node server, redis and mongoDB NoSQL database
  
## Project architecture

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/images/jchat/jchat-architecture.png" alt="">
  <figcaption>Architecture overview of this chatting web app</figcaption>
</figure> 

## System design

### User Interface of web client

The front end user interface is build by leveraging React.js and Redux. Thanks to functional programming paradigm encouraging by React.js and Redux,
the state management, propagation of change and data flow become so easily predictable and maintainable. The development and debug tremendously benefit 
from the concept of immutable state and pure function of functional programming. This enable me to write less error prone code and easy to test code.
Redux embrace the idea of separating of presentational and container components:

* presentational components
  * They describe how things look. These are normal stateless React component, you give the state, they always show the same results. 
    These components must not retain internal state. They are pure functional transforms of their input.
* Container components
  * They describe hwo things work. Compared to presentational components, they are stateful, and their job is to hook up the app's state to React stateless components. 
    They manipulate and plugin whatever data into reusable React stateless components. Actually they are wrapper of React components, 
    and React components can be reused in different stateful components.
    
In addition to functional programming, the development of this web app also benefit from another idea of one way data flow.
During development and debugging, where are current data located and where will they flow to are clear visible and predictable.
 
### Data routing at server side

The server build by Node.js, which intrinsically is good at handling intensive high volume of IO operations. Chatting app is an ideal use case.
This app use Node.js and socket.io to asynchronously handel websocket connections.

Redis control the routing of messages by leveraging Redis PUB/SUB feature. Users subscribe its own user id when connecting to node server,
friends publish their messages to this specific user id, this can guarantee the receiver can always successful receive messages send from friends by this simple mechanism.
Redis also used as cache of chat records. The node server will push each message received to Redis no matter receiver online or offline. These cached messages
will be popped when user login, so they can see their chatting history even when they offline.

### Persistent data

MongoDB provides semi-structured data format to store user information like username, password and friends list. The JSON like semi-structured data format are easy to read
and query compared to relational database that need a lot of table join operations. MongoDB support rich queries, no complex join and easy to scale. That's why MongoDB
is one of the most favorite NoSQL database especially in era of big data and distributed computing.

### Wrap up

Embracing functional programming in front end development is amazing and excited way of problem solving, especially in the development of massive interaction
between users and user interface. Functional programming is more expressive than object-oriented or imperative programming. I will leverage the idea of functional programming 
throughout my future programming tasks whenever possible on my initiative.