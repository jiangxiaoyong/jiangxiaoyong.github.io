---
title: "Multiplayer Online Battlee"
excerpt: "Online battle game build by clojure in functional reactive programming"
header:
  overlay_color: "#333"
  teaser: /personalCloudStorage/welcome.png 

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

File hosting service, which allows people store and synchronise file on the cloud, such as Dropbox, google Drive and OneDrive, bring convenience to people's life.
 However, when using cloud storage service, people have to worry about capacity and security issue. So it's time to create my personal cloud storage
  service that have the same functionality as Dropbox while I do not need to facing those issues mentioned above.

## Project Description 

 It's my personal cloud storage service, which allows me uploading, downloading and managing different type of files on the cloud.

 It is hosted on Amazon [EC2](https://www.google.com), here is [Git Repo](https://github.com/jiangxiaoyong/Personal-Cloud-Storage)

{% include gallery caption="Screenshots of welcome page, signin page, main page, upload file page and create new folder page." %}

## Features

 * Enable uploading, downloading and deleting different type of documents, such as text, images, audio and video files
 * Enable creating folder to organize and manage files
 * Enable uploading multiple files at a time
 * Enable user authentication by username and password 
 
## Technologies Stack

### Front end user interface

HTML5, CSS, Bootstrap and Javascript

### Back end server

Java, Spring, Spring security

### Persistent Storage

Hibernate, MySQL 

