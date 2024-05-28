---
title: 'GIT - Global Information Tracker'
date: 2024-24-05
draft:  true   
featured: false  
description: "GIT - Global Information Tracker"
thumbnail: "/posts/git/images/git.png"
featureImage: "/posts/git/images/git.png" 
shareImage: "/posts/git/images/git.png"
author: "Angel Vyas"
tags:
    - Git
categories:     
    - General
---

Git is a distributed version control system that tracks versions of files.

<!--more-->

First let's take a look at different `Version Control Systems`, so we have mainly have two types of Version Control System namely Centralized version control and Distributed version control.

## Centralized Version Control System (CVCS)

In a centralized version control system (CVCS), also known as a centralized source control or revision control system, a server acts as the main centralized repository which stores every version of code. 


## Distributed Version Control System (DVCS)








Let's say we have a server and several clients connected to it. The workflow is same in both the systems, the client pushes changes to the server and after pulling the latest updates and server will manage the project. 

In **Centralized Control System**. The issue at hand is that every client depends entirely on the server for everything, including history, commit IDs, and code, which is stored on the server and not shared with any of the clients. Means if the server collapse, the entire project would fail as well. 

In contrast, the **Distributed Control System** shares all of the history, commit IDs, and code with its clients, so that  if the server collapsed the clients can still have the complete history and code of the project , means the project is not collapsed ,the clinets can push the data now to a new server.
 The conclusion is that the project is more safe in distributed control system.

example for *Distributed Control System*:- Git, Mercurial, etc.

example for *Centralized Control System*:- Subversion, Team Foundation Source, etc.



# WHAT IS A REPOSITORY?
In version control systems, a repository is a data structure that stores metadata for a set of files or directory structure.

# VARIOUS METHODS TO RUN GIT COMMANDS:-
1. The command line.
2. Code editors and I.D.E. (editors like VS studio has inbuilt basic git commands )
3. Graphical User Interface(For example:- Github Desktop which is a free version.)

## ADVANTAGES OF USING COMMAND LINE FOR GIT OPERATIONS:-
GUI Tools have their own limitations like, they are not always available.

### SETTINGS THAT WE CAN SPECIFY FOR GIT AT THREE DIFFERENT LEVELS NAMELY, USER, SYSTEM AND GLOBAL ARE;-
1. Name
2. E-mail
3. Default Editor
4. line ending

### The Heirchial order is as follows:-
User>system>global

> **NOTE**:- These settings are important since every time you made a commit, it is stated that who made that commit so, if user details are not mentioned then system details are used, and if system details are not given then global details are used as the commit id.