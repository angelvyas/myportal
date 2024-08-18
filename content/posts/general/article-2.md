---
title: "Let's talk about different environments on my system."
date: 2024-08-18
draft:  false   
featured: false  
description: "My System"
author: "Angel Vyas"
tags:
    - Info
categories:     
    - General
---

Now let's talk about different environments, so on our system, we can  work on more than one O.S. if, like on my windows I have ubuntu. In case of Windows for installing a secondary O.S. there is a software known as WSL: which allows me to install a secondary O.S. on my primary operating system. 

Another example: Virtual Box. 

 

 

**Mounting of files:** 

There is a concept of mounting of files over two O.S., the one which is already there, and the one which we have installed. 

In easy language mounting can be understood like linking of address. 

When you install a secondary O.S. on your computer, WSL(in case of windows) provides certain space of the hard disk (Memory) to that O.S., where you can store your files while working on your secondary O.S., now if you want to  save your files of your secondary O.S. on your primary memory, then you can mount those files. 

In case of windows, WSL on default mount your secondary O.S. files on your local O.S., that's why you are able to see those files that you have saved on your secondary O.S., on your local. But if some files are not mounted, then you can mount by adding the files that you want to mount in the mnt file which exist there in your secondary O.S.  

 

 

 

**Why files that you store on Secondary O.S. not visible on your Primary O.S.?** 

if you have not mounted your secondary O.S. files then primary O.S. does not know the address of the files that you have saved in the secondary O.S. that's why files that you store on Secondary O.S. are not visible on your Primary O.S.. By mounting the files, you share the address of the files with the primary O.S. 

 

*One interesting thing to note is that:-* 

Hardisk is just a bundle of magnetic tapes, so let's say you have stored one file, means your saved file we'll get an address on the hard-disk and is saved there. But if you delete that file, then it's not like you have erased that data, since that's not possible, so how you have freed that space? 

The Answer is that by deleting a file, the address of that file is lost, and if you save another file on that location, then reprinting occurs over that already existed data there. That's why there is an option of backing up files even you have deleted the file, since by deleting it doesn’t means erasing the data, it simply means that address is lost, or have become free now for further use. 

 

**Now lets talk about conda:-** 

Conda is a software, which let us install different versions of python by creating different environments, 

If I want to work on different versions at one time, then conda let us download different versions of python by creating different environments,  

For example you're currently working on 3.1 and simulatneoulsy you want to work on 3.9 then you can by changing environments by a simple code which is: conda activate python 3.9😊 

 