---
layout: post
title: Conquering the Command Line
description: A brief guide to getting started on UNIX/Mac OS terminal
image: assets/images/starwarsterminal.png
permalink: command-line-basics
author: monica_powell
comments: true
---
<center><em>Output on Mac OS terminal after typing: **telnet towel.blinkenlights.nl**</em></center> <br>

<br>

When I was first introduced to the command line I really had to adjust to
navigating my computer in a black box with just text. So I avoided the command
line as much as possible. I was accustomed to the visual cues and feedback that
a computer usually provides. In many ways it felt like I was re-learning how to
use a computer via the command line.

Yet, since first learning how to navigate my computer using UNIX commands I’ve
learned that the command line doesn’t have to be a scary thing just because
there’s no visual feedback when typing a password in on the command line. As
security, nothing shows up as you type in your password to indicate that any
characters have been entered.

#### What is the command line?

The command line is a software that executes commands or instructions for a
computer to manipulate or interact with its file system.

### What is UNIX?

#### Why Use the Command Line?

* Faster to modify, navigate between files
* Able to install software as a superuser
* Can see hidden dotfiles<br> dotfiles are UNIX configuration files, they tend to
be files that are proceeded with a `.` and are hidden to normal users.<br> You
can [learn more about getting started with dotfiles in this
article](https://medium.com/@webprolific/getting-started-with-dotfiles-43c3602fd789)).

In order to get started on the command line you should navigate to your
applications and open the **Terminal** application.




![terminal-1.png](/assets/images/terminal-1.png#img-center)
Above is the Terminal Icon on Mac.

<br>
### Create a Basic Website Folder on the Command Line


![terminal-2.png](/assets/images/terminal-2.png#img-center)
<center><em>Folder structure of sample project</em></center> <br>

A folder with the above structure can be create on the command line by typing
the commands inside of an empty directory:

![empty-directory.png](/assets/images/empty-directory.png#img-center)
<center><em>We start inside of an empty directory!</em></center> <br>

* Make a directory (also known as a folder) called personal-website<br> `mkdir
personal-website`

![personal-website.png](/assets/images/personal-website.png#img-center)
<center><em>We’ve created a folder named personal-website</em></center> <br>

* Navigate to inside of the directory called personal-website<br> `cd
personal-website`
* create a directory, inside of the personal-website folder called assets<br>
`mkdir assets`

![assets-folder.png](/assets/images/personal-website.png#img-center)
<center><em>We’ve created a folder inside of personal-website to contain all of our assets</em></center> <br>

* Navigate inside of the assets folder which is inside of the personal-website
folder<br> `cd assets`
* create a directory, inside of the assets folder named images<br> `mdkir images`
* create a directory, inside of the assets folder named js<br> `mkdir js`
* create a directory, inside of the assets folder named css<br> `mkdir css`

![all-asset-folders.png](/assets/images/all-asset-folders.png#img-center)
<center><em>We’ve created folders inside of personal-website/assets to store our project’s
assets</em></center> <br>

![terminal-2.png](/assets/images/terminal-2.png#img-center)

Woops! We forgot to create an index.html file :(

We are in the assets folder and want an index.html file in our main
personal-website folder. Typing `cd ..` will move us out of the assets folder
and into the directory above which is personal-website. Now that we are in the
personal-website folder if we type `touch index.html` a blank index.html file
will be created.

![complete-directory.png](/assets/images/complete-directory.png#img-center)

### Some frequently used terminal commands are:

#### commands to navigate/manipulate the filesystem

**ls** - **list** the contents of a directory

**pwd** - **print working directory** for the terminal to display the directory you are
currently working on

**touch** - create or open a file without making any changes<br> very handy when
wanting to create empty files without leaving the command line

**sudo** - this allows you to run commands as a **super user**

**mv** - **move a file or directory** this can be used to move or rename a file by
updating the file path

**cd** - **change the current directory** you are working on so that you can
access files on a different part of the system<br> `cd` moves you to the root
directory (top level folder on computer — usually the current User)<br> `cd .`
current directory <br> `cd ..` navigates to directory two levels up

**mkdir** - **make** a new **directory** (or a folder)

#### **Commands to Install Software**

You can install some software from the command line using the following
commands:

* in Python `pip install <package name>.` <br> Pip is a software package manager
for Python.
* in JavaScript `npm install <package name>` <br> NPM is a package manager for
JavaScript pages.

#### Commands to Run Software

In order to run a script on the command line you need to provide a command
prompt and file name. Some examples are:

* in Java `javac filename.java` and then `java filename` compiles java projects
and then runs them.
* in Python` python filename` runs python scripts.

If you find you are repeating a lot of commands you can scroll through your
recent commands using the up/down arrows and edit them and re-run by navigating
to them and then pressing enter.

#### Additional Resources to Get Started with Command Line Prompts

* [MIT Terminus (interactive game to learn command
line)](http://web.mit.edu/mprat/Public/web/Terminus/Web/main.html)
* [Codecademy Learn the Command
Line](https://www.codecademy.com/learn/learn-the-command-line)
* [Learn Python the Hard Way’s Command Line Crash
Course](https://learnpythonthehardway.org/book/appendixa.html)

#### Decorating the Command Line

You can completely customize the colors and outputs on the command line to
better suit your visual and aesthetic needs.

I made my command line appear prettier by installing the theme Tomorrow Night. Check out
[this site](https://mindthecode.com/customize-the-terminal/) for instructions on installing the theme Tomorrow Night.


**A version of this article was originally published by Monica Powell on [FreeCodeCamp](https://medium.freecodecamp.org/conquering-the-command-line-f85f5e46c07c) on December, 5th, 2017 **
