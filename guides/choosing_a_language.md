# How to Choose a Programming Language
## For Chemists and the Chemistry-Adjacent

### Table of Contents

- [How to Choose a Programming Language](#how-to-choose-a-programming-language)
  - [For Chemists and the Chemistry-Adjacent](#for-chemists-and-the-chemistry-adjacent)
    - [Table of Contents](#table-of-contents)
    - [Introduction](#introduction)
    - [General Purpose Programming Languages](#general-purpose-programming-languages)
    - [Data Collection, Cleaning, Processing, and Visualization](#data-collection-cleaning-processing-and-visualization)
    - [Machine Learning and Artificial Intelligence](#machine-learning-and-artificial-intelligence)
    - [Systems Programming and Scripting](#systems-programming-and-scripting)
    - [Instruments and Devices](#instruments-and-devices)
    - [Numerical Computation](#numerical-computation)
    - [Web Programming](#web-programming)
    - [GUI Applications](#gui-applications)
      - [Distributing Applications](#distributing-applications)
      - [Desktop Applictions](#desktop-applictions)
      - [Mobile Applications](#mobile-applications)
    - [Conclusion](#conclusion)


### Introduction

If you are interested in programming,
but don't know where to start,
answering the question "What programming language should I learn?" 
is the first obstacle to overcome. 

This is an (opinionated, non-authoritative) guide 
to help people answer that question for themselves. 
The author will try to make their personal opinions 
and lack of knowledge clear as warranted. 
Corrections and additions to this guide are welcome!

This guide will mention the most commonly-encountered languages 
that are either particularly useful to chemists, 
or are particularly well suited for people just starting to learn programming.

Whatever language you choose, 
once you dive into it you will also learn tools, skills and habits 
that are not language-specific. 
If you spend some time learning one language, and decide to try another, 
you will have the pieces in place to pick up the next language 
and start working with it.

This guide is structured around the likely answers to that question:

**<p align=center>Why are you interested in programming?</p>**

### General Purpose Programming Languages

Most of this guide will be for people that already have some idea 
of what they want to do with their new coding superpowers.
However, maybe you just think coding sounds generally useful, 
interesting, or fun. 
If that is the case, 
the author's *opinionated* answer is:

**<p align=center>[Python.](https://www.python.org/)</p>**

Python has been described as being "the second-best language for everything".
In particular, it's a top-tier language for data processing and visualization, 
machine learning (ML), and artificial intelligence (AI).
There is a huge ecosystem of scientific and numeric packages for Python as well.

Plus, (in the author's opinion), Python is easy to pick up 
and start doing useful things with. 
The language is *expressive*, almost reading like "pseudo-code" at times. 
For example, let's say you wanted to tell the computer:

```text
"for each name in my list of guests: Amy, Bob, Cathy and Doug,
print "Hi, (name of guest!)"
```

This is what it would look like in Python:

```python
for name in ['Amy', 'Bob', 'Cathy', 'Doug']:
    print(f'Hi, {name}!')
```

In contrast, this is what it would look like written in c:

```c
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    char guests[4][10] = {"Amy", "Bob", "Cathy", "Doug"};
    for (int i = 0; i < 4; i++) {
        printf("Hello, %s!\n", guests[i]);
    }
    return EXIT_SUCCESS;
}
```
>#### When might "Python" not be the best answer?
>
>The following situations can be problematic with Python, to varying degrees.
>
>- Running on multiple CPUs ("multithreading"): 
  this is possible, but Python has the notorious 
  [Global Interpreter Lock (GIL)](https://www.python.org/) 
  that makes this cumbersome.
>- speed-critical applications: Python is a slow language. 
  However, it can interface with faster languages. 
  For example, the widely-used `numpy` libary for numerical computation 
  uses Fortran libraries "under the hood", 
  and its possible to write Python code 
  where the faster language is performing most of the work. 
  However, if you are designing a computer 
  to perform stock market micro-transactions so fast 
  that your speed is limited by how long the wire is 
  between your computer and the stock exchange across the street, 
  you don't want to be using Python.
>- creating cross-platform desktop applications 
  that you can distribute to non-programmer friends. 
  This is doable, especially for small applications,
  but can get tricky as your application gets more complicated.
  Third-party tools are required 
  to bundle your python code as a one-file application.
>- writing applications for mobile devices. VERY DIFFICULT. 
  Possible (e.g. with [kivy](https://kivy.org) or [BeeWare](https://beeware.org), but Here Be Dragons.

An honorable mention goes to 
[the Julia programming language](https://julialang.org). 
The author does not have Julia experience, 
and the Julia community is much smaller than the Python community. 
However, it is a multi-purpose language 
that seems particularly well-suited for scientific computing, 
data science and visualization, machine learning and numerical computation. 
It is also much faster than Python, if computation speed is a concern.

A final consideration is JavaScript (plus HTML and css), which is useful in many of the contexts listed later in this guide. 

### Data Collection, Cleaning, Processing, and Visualization

Python and [R](https://www.tidyverse.org/) are excellent choices. 

An advantage of R is that there is a 
"[tidyverse](https://www.tidyverse.org/)" of widely-adopted packages, 
where there is a clear favorite way to do something, 
such as make a plot or a web application. A disadvantage is that is focused on working with data, so e.g. you wouldn't write a desktop application in R.

Python has the advantage of being useful in many contexts beyond data science. However, you may find yourself spoiled for choice when selecting tools, e.g. what library to use for plotting graphs. 

Other considerations:

- Julia 
- [SQL(structured query language)](https://en.wikipedia.org/wiki/SQL): 
  If you find yourself needing to work with databases, adding some SQL knowledge on top of your preferred programming language will be useful. 
- See also 
  [this article on Codecademy](https://www.codecademy.com/resources/blog/data-science-languages/) 
  describing these and other options.

### Machine Learning and Artificial Intelligence 

You will find more ML/AI resources that use Python than any other language. There is a lot to learn in this field, so the author's suggestion is start learning using Python to get up to speed before considering another language.

### Systems Programming and Scripting

If your interest is working with the nuts and bolts of a computer system
(working with files and directories, scheduling automated tasks, etc.),
Python is a great place to start. 
There is a popular 
[book written about automating tasks with Python](https://automatetheboringstuff.com). 
It's a good resource for both learning Python and finding ideas for projects.

Whatever programming language you choose,
you will need to learn how to use the command line interface 
('CLI'; 'terminal'). 
On Unix-like systems (macOS; linux) this means learning bash 
or a closely-related variant 
(Macs recently switched from bash to zsh, but they are mostly the same). 
Windows comes with PowerShell, but you can install a bash CLI as well.

Basic commands such as navigating a directory, creating files and folders, 
and running your programs can be learned in minutes.
If you dig deeper, the command line can be extremely powerful.
As a motivational example, here is a one-line command that will: 
- recursively search through a tree of nested NMR data folders; 
- find the temperature each experiment was run at; and 
- save a .csv that lists all NMR jobs and temperatures:

```bash
$ grep -r "##\$TE=" --include="*acqus" . | cut -c 3- | sort | sed -e 's/:##\$TE= /,/' > T_pH7.csv
```

That may look incomprehensible, 
but it's composed from several individual bash commands 
that you would learn in any basic bash guide. 
With very little bash experience, 
the author could accomplish in one terminal command 
a task that would require many lines of Python or equivalent code.

Both Python and Bash are widely used for writing executable "scripts" 
to automate common tasks.

There is a large family of "curly-brace" languages 
that are all good "professional programmer" choices for system programming: 
c++, Go, Java, Rust, etc. 
The author's advice is to avoid languages that are so "low-level" 
that you have to constantly consider fussy things, such as:
- where and how variables are stored in memory and accessed; 
- how to manage memory allocation;
- determining "which one of these nine types of integers is best 
  to represent my number?". 

However, if you really want to learn programming 
from the viewpoint of a computer scientist or a software engineer, 
a language such as c/c++ will make you learn 
what goes on "under the hood" of your computer.

### Instruments and Devices

If you want to get started with devices, microcontrollers, 
and Internet of Things (IoT) projects, Python is a good choice. 
It's the default choice if you are working on a Raspberry Pi. 
Many controllers can be programmed with Python 
or a subset of Python (e.g. [CircuitPython](https://circuitpython.org)).

[Arduino microcontrollers](https://www.arduino.cc) use a variant of c++ for their programs, but Python is also supported (via [MicroPython](https://docs.arduino.cc/learn/programming/arduino-and-python)).

It's not possible to generalize across scientific instrumentation,
but you may find low-level languages like c being used. 

### Numerical Computation

Even though Python is a slow language, 
it can make use of libraries that run faster code 
(e.g. FORTRAN, c) "under the hood". 
An example of this is 
[the `numpy` library](https://numpy.org) for numerical computation. 
With optimization, Python can often be fast enough for your needs. 

There are libraries that can help speed up your Python code, 
e.g. by [implementing "just-in-time" compiling](https://numba.pydata.org) 
or [GPU acceleration](https://cupy.dev).
There is also a version of Python, 
[PyPy](https://www.pypy.org), that runs faster than standard Python. 

If your code needs to run faster than Python is capable of, here are some alternatives to consider:

- Julia 
- MATLAB is widely used by scientists and engineers, 
  but it's proprietary. 
  If your workplace has bought a license for it, 
  and you do a lot of numerical work (e.g. linear algebra), 
  it can be very useful. 
- You could consider the "curly-brace" languages such as c/c++, 
  but the learning curve will be steeper. 
  If others in your field use one of these languages, 
  it may be worth it.

### Web Programming

If your primary interest in things Web-related 
(creating web pages, webservers, online databases etc.), 
JavaScript (JS) is ubiquitous in Web programming. 
It is also a great choice for a first language to learn. 
It can be used for both "front-end" web development 
(writing JS/HTML/CSS code for display in a web browser), 
and in "back-end" development (setting up a web server). 
Most beginners will be interested in the front-end work of creating a website, and let a web hosting service take care of the back end.

Python is also a good choice, especially for back-end work[^1].
Popular web frameworks include Flask, Django, and FastAPI. 
For example, 
if you have data in a database
that you want to make available over the internet, 
you can use one of these frameworks 
to create a web API (Application Programming Interface) 
that will let people around the world access and use your data.

[^1]: A promising new development is PyScript, 
  first announced at PyCon US 2022. 
  PyScript is a Python interpreter plus some of the most popular libraries, 
  bundled together and compiled into Web Assembly language (WASM). 
  There are other languages also finding their way into the browser via WASM, 
  such as Rust.

If you are not programming in a language that is native to mobile devices
(e.g Swift for iOS or Java for Android),
another way to get your program onto users' phones
is to create a web application. 
Then, any device with a web browser would have access to your app.

### GUI Applications

If you want to create an application with a graphical user interface (GUI),
many languages will allow you to do this, including Python.
If your *primary* interest in programming 
is that you want to create a desktop or mobile application, read on.

#### Distributing Applications

Some desktop programs come bundled in a single file. 
For example, 
you might download the file and drag it to your Applications folder, 
and then double-click it to run. 
Other programs run an installer 
to set up the required files on your user's system. 
If you are not a professional programmer, 
the one-file app is probably easier, 
and certainly safer for your intended user.
However, some languages make bundling your program 
as a one-file desktop application easier than others. 

If you want to create a mobile application, 
you first have to consider if you want to target iOS, android, or both. 
Then, you have to consider the limitations of developing on that platform. 
For example, on iOS you will need to create a developer account. 
If you want other people to use your application on their iPhone, 
you'll need to pay Apple money and get a digital signature for verification.

#### Desktop Applictions

If you want to create an application 
that has the native look and feel of your favorite operating system 
(macOS or Windows), 
your main choices are Swift on macOS and C# ("C-sharp") on Windows. 
The author doesn't have much experience with these languages. 
However, C# and Microsoft's .NET platform make cross-platform 
and mobile apps possible as well, 
whereas Swift's primary focus is macOS applications[^2].

[^2]: The author has a bias against heavy investment in a language 
  that can depends on a parent company for its existence. 
  For example, Apple could decide that they're dropping Swift 
  as the preferred language for their platforms. 
  Java's corporate sponsor, Oracle, 
  has engaged in shady practices in the past, including 
  [update installer that would try to install unwanted applications ('bloatware' or 'crapware) on its users' systems](https://www.zdnet.com/article/a-close-look-at-how-oracle-installs-deceptive-software-with-java-updates/).
  Visual Basic 6 (VB6) was very popular, 
  allowing scientists, business people and hobbyists to create 
  their own Windows applications. 
  Microsoft's shift to the .NET platform 
  effectively orphaned any development of VB6 programs.
  Using one of these languages can still be the right choice for you,
  but go in with eyes open.

If you are also interested in web programming as well, 
[Electron apps written with JavaScript](https://www.electronjs.org) 
are a great solution. 
The author wrote this guide using Microsoft's VS Code, 
which is an Electron app. 
Other examples of Electron apps that you may be familiar with include: 
Discord, Dropbox, Slack, GitHub Desktop, and Microsoft Teams. 

Simple desktop applications in Python are not too difficult, 
but as the complexity goes up you may run into difficulties. 
You will need to choose a GUI framework and learn how to use it, 
and then you will need to use a tool to create the one-file application bundle. 
These applications basically copy an entire Python environment into the bundle, 
so a Python app tends to take up much more memory on a hard drive 
than a similar program written in a compiled language.

In the less-beginner-friendly category, Java and c++ are commonly used to write cross-platform applications. 

#### Mobile Applications

The author doesn't recommend first-time programmers learning a language focused on mobile development. That said:

- For iOS, Swift is the language of choice.

- For android:
  - Java is the historical choice
  - Kotlin has become very popular for android development
  - other c++-like languages are also supported

### Conclusion

The journey of a thousand miles starts with a single step.
This guide hopefully helps you take a step in the right direction.
Even if you decide that a programming language is not for you, 
hopefully your interest in programming is now kindled,
and the guide can help you retrace your steps and set out again. 😄