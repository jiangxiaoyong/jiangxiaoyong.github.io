---
title: "Personal Cloud Storage"
excerpt: "A full stack cloud storage web app using Java, Spring, Hibernate and MySQL"
header:
  overlay_color: "#333"
  teaser: /personalCloudStorage/welcome.png 

gallery:
  - url: /personalCloudStorage/welcome.png
    image_path: /personalCloudStorage/welcome.png
    alt: "placeholder image 1"
  - url: /personalCloudStorage/login.png
    image_path: /personalCloudStorage/login.png
    alt: "placeholder image 2"
  - url: /personalCloudStorage/mainPage.png
    image_path: /personalCloudStorage/mainPage.png
    alt: "placeholder image 3"
  - url: /personalCloudStorage/uploadPage.png
    image_path: /personalCloudStorage/uploadPage.png
    alt: "placeholder image 4"   
  - url: /personalCloudStorage/createNewFolder.png
    image_path: /personalCloudStorage/createNewFolder.png
    alt: "placeholder image 5"   

tags: 
  - SpringMVC
  - JAVA
  - bootstrap
  - HTML 
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

