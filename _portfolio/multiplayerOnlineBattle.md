---
title: "Multiplayer Online Battle"
excerpt: "Online battle game build by clojure in functional reactive programming"
date: 2017-01-20
header:
  overlay_color: "#333"
  teaser: /multiplayerOnlineBattle/gaming.png 

gallery:
  - url: /multiplayerOnlineBattle/login.png
    image_path: /multiplayerOnlineBattle/login.png
    alt: "placeholder image 1"
  - url: /multiplayerOnlineBattle/gameLobby-idle.png
    image_path: /multiplayerOnlineBattle/gameLobby-idle.png
    alt: "placeholder image 2"
  - url: /multiplayerOnlineBattle/gameLobby-ready.png
    image_path: /multiplayerOnlineBattle/gameLobby-ready.png
    alt: "placeholder image 3"
  - url: /multiplayerOnlineBattle/gaming.png
      image_path: /multiplayerOnlineBattle/gaming.png
      alt: "placeholder image 4"
    
tags: 
  - clojure
  - clojurescript
  - functional programming
  - reactive programming
  - concurrent programming
  - FRP
  - HeroKu
---

## Motivation

Concurrent programming play an important role no matter building reactive front end user interface or high-throughput back end.
There are several different technique which allow developer to write synchronous code while still enjoying asynchronous flow, such as future, promise and event/callbacks.
However, there technique perform well at one shot notification, code will mess up again and out of control when events nested within each other, e.g. callback hell.
Even thought promise are able to flatten callback hell somehow, however still insufficient to handle event-driven system.

Besides, state management is another difficult task to deal with especially in concurrent and parallel system in object oriented or imperative programming paradigm. 

Fortunately, functional reactive programming solve concurrency problem from another perspective compared to imperative programming, [elm](http://elm-lang.org/) is one of the 
noticeable solution in FRP, inspired from pure functional programming language [Haskell](https://www.haskell.org/).

[Communicating Sequential Process](https://en.wikipedia.org/wiki/Communicating_sequential_processes) is one of the most prominent way to describe communicating pattern 
of interaction in concurrent system. CSP theory heavily influence the design of Google Go programming language, which handle concurrency based on message passing via channel.
Inspired by Go, Clojure implements CSP in it's core.async library. 

* `go routine` are cheap to create so you can have hundreds of thousands of them, and the runtime will multiplex them into a thread pool.
These lightweight process run concurrently and dead simple to achieve a higher degree of concurrency. 

* Channels are the first-class citizen, meaning you can pass them as arguments to functions as well as the return value of functions. Each asynchronous `go routine` communicate
through message passing via channel.

The idea implemented in core.async library plus the concurrency model and immutable data structure provided by clojure make concurrent asynchronous programming become easy and fun.

Functional programming paradigm combined with reactive asynchronous data stream allows developers to write maintainable and less error prone code in declarative way than traditional imperative way.
 
This project mainly serves to get more practical experience in functional reactive programming, and consolidate my understanding of concurrent asynchronous programming. 

## Project Description

The ambitious of this project is to support different players from all over the world are able to join together in an online battle arena to challenge each other in real-time 
playing flappy-bird in multiplayer version. After simple login by username, player join a game lobby, that lists all players with current status, like idle, ready or gaming. 
The game will be fired after all players indicating status ready. All players will be loaded in game world, so players will see each other as one of the flappy-bird controlled by corresponding player.
Player will see current score after successfully pass each pillar in the game world.

* [live demo](https://thawing-reef-68533.herokuapp.com/) 
* [Github Repo](https://github.com/jiangxiaoyong/multiplayer-online-battle) 

{% include gallery caption="Screenshots of login, game lobby idle, game lobby ready and campaign." %}

## Project Features
This online game supporting following features:

* multiple players challenge each other from all over the world in real-time
* players are able to see each other in the game world
* scoring
* game lobby lists all players with corresponding status, like idle, ready and gaming
* game lobby shows player join and player leave
* enable player login

## Project architecture

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/images/multiplayerOnlineBattle/architecture.png" alt="">
  <figcaption>Architecture overview of whole system</figcaption>
</figure> 

## System design

### Front end

Functional reactive programming was chosen as the architectural style to build front-end. Clojurescript enable to program in functional way with pure function no side effect 
and immutable data structure. Rx works great for event-heavy frontends and apps. It provides reactive programming in asynchronous data stream in extended observer design pattern.
It's **one way data flow** in user interface inspired from React.js, that make the system easy to reason about and debug.

#### view

Reagent as one of the React.js wrapper in Clojurescript provides a way to write efficient React components. Combined with build-in immutable data structure, the performance
of writing user interface in clojurescript might faster than user interface build by native React.js

#### Reactive JS

Here is absolutely right place to all asynchronous data stream in reactive programming. Game control, like keyboard events, events from user interface 
and all game events from WebSocket are all go through the module of reactive. **By programming in reactive, the code are able to write in declarative way than imperative, which means 
we are not giving a sequence of instructions to execute, we are just telling what something is by defining relationships between streams. Tell what to do instead of how to do it 
is the core idea in functional reactive programming. By reactive programming, control flow elements such as if, for, while and callback-based that typically expected from a JavaScript application 
can be eliminated completely**. That's so impressive.

#### Controller

Events for game lobby or actual game are filtered and categorized feed into controller. All controller need to do just mutating states belong to game lobby or actual game world according 
to game logic. Thanks to concurrency model provided by clojure/script, mutation are thread safe credited to persistent data structure and state/identity separation. Developers are 
able to easily write concurrent multi threads program without using lock and worry about dead lock, live lock, race condition and starvation.

#### Game state

A map storing all states regarding game lobby and actual game world. Again, no worry about mutation in this shared resource among multiple threads.
UI view will render new view based on latest state.

### Back end

Back end are constructed by Clojure in functional programming paradigm. Building system is like evaluating math expression and focusing on data flow in pipeline.

In order to achieve game synchronization and ensure consistency among multiple players, client-server model with lockstep has been utilized as the synchronization mechanism,
which also was used by Warcraft 3. All clients send command message, like keyboard pressing or mouse clicking to central server, and server broadcasting command messages from
command message buffer to all clients 20 times per second to achieve game synchronization.

There are other synchronization mechanism for online multiplayer game, like pear-to-pear lockstep, with each computer exchanging information with each other in a fully connected mesh topology.
Please check referencing resources.

#### Game synchronization

At least there are three different game synchronization mechanism are candidates for building this game:

* Pear-to-Pear Lockstep that exchange command message betwwen players
* Client-Server Lockstep that broadcasting whole game states at each turn
* Client-Server Lockstep that broadcasting only command message at each turn

The limitation of first approach is that in order to ensure that the game plays out identically on all machines it is necessary to wait until all player’s commands for that turn are received before simulating that turn. 
This means that each player in the game has latency equal to the most lagged player.

The mechanism of second approach is that all clients modify a shared state stored in central server, and server broadcasting the shared state to all clients at each turn.
It's good for turn-based game. However, the limitation of second approach for game that consist of thousands of units is that it's too large to broadcasting entire game states among  millions of clients

The third one has been us exploited as the synchronization mechanism. The basic idea is to abstract the game into a series of turns and a set of command messages when processed at 
the beginning of each turn direct the evolution of the game state. 
For example: move unit, attack unit, construct building. All that is needed to network this is to run exactly the same set of commands and turns on each player’s machine starting from a common initial state.

In terms of this game, clients upload their command message to central server, which will buffered all command messages from all client within each turn.
There are twenty turns per second. The server will broadcasting buffered command messages to all connected client at 20 times per second.

## Referencing resource

#### Functional programming

* [Functional Programming brief introduction](http://janfan.github.io/chinese/2015/05/18/functional-programming.html)
* [Functional Programming for JavaScript People](https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504#.w2y07jcyf)
* [SegmentFault 技术周刊 Vol.16 - 浅入浅出 JavaScript 函数式编程](https://segmentfault.com/a/1190000007784565)

#### Reactive programming

* [The introduction to Reactive Programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)
* [Reactive Programming in JavaScript With RxJS](https://dzone.com/refcardz/rxjs-streams)

#### Clojure

* [The Unofficial Guide to Rich Hickey's Brain](http://www.flyingmachinestudios.com/programming/the-unofficial-guide-to-rich-hickeys-brain/)
* [Understanding Transducers](http://elbenshira.com/blog/understanding-transducers/)
* [core.async examples](https://github.com/halgari/clojure-conj-2013-core.async-examples/blob/master/src/clojure_conj_talk/core.clj)
* [community-driven documentation site](http://clojure-doc.org/)

#### clojure server

* [Dockerizing a Clojure, Compojure, and HTTP Kit Web Application](https://wtfleming.github.io/2014/11/29/dockerize-clojure-compojure-http-kit-web-application/)

#### Clojurescript

* [CSP and transducers in JavaScript](http://phuu.net/2014/08/31/csp-and-transducers.html)
* [JavaScript玩转Clojure大法](https://blog.oyanglul.us/javascript/clojure-essence-in-javascript-transducer.html)
* [Understanding Transducers in JavaScript](https://medium.com/@roman01la/understanding-transducers-in-javascript-3500d3bd9624#.o42thu8ic)
* [TRANSLATIONS FROM JAVASCRIPT](http://himera.herokuapp.com/synonym.html)
* [为什么 ClojureScript 很重要](https://segmentfault.com/a/1190000003008500)
* [ClojureScript: JavaScript Interop](http://www.spacjer.com/blog/2014/09/12/clojurescript-javascript-interop/)
* [ClojureScript-Syntax-in-15-minutes](https://github.com/shaunlebron/ClojureScript-Syntax-in-15-minutes)
* [Immutable 详解及 React 中实践](https://github.com/camsong/blog/issues/3)
* [jumping-from-html-to-clojurescript](https://github.com/shaunlebron/jumping-from-html-to-clojurescript)
* [Using JavaScript libraries in ClojureScript](http://lukevanderhart.com/2011/09/30/using-javascript-and-clojurescript.html)

#### network game design

* [What every programmer needs to know about game networking](http://gafferongames.com/networking-for-game-programmers/what-every-programmer-needs-to-know-about-game-networking/)
* [游戏中的网络同步机制——Lockstep](http://bindog.github.io/blog/2015/03/10/synchronization-in-multiplayer-networked-game-lockstep)

### Wrap up

It's impressive to learn the idea and concept behind clojure/script. like functional programming, persistent data structure, separation of state and identity and its concurrency model.
Besides, my understanding of asynchronous programming has been further consolidated by learning clojure core.async and reactive programming.

Channels are the first-class citizen and message passing via channel allow developer write asynchronous code but still maintain synchronous readability in concurrent programming.
Treating everything as asynchronous data stream allows to write declarative code and eliminate control flow elements, like if for while and callback, that is tell what to do instead of 
hwo to do. This approach is really powerful and efficient to write maintainable code for event-driven program.