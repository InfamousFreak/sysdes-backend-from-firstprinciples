## Real time ICU monitoring system : 
## Python : 
python is a high level, general purpose, interpreted programmign language, core philosophy  **: code readability matters.**

foundational backbone of modern software development

why python ?
- human readable syntax : plain english and clean visual indentation
- interpreted nature : executes code line by line, no time wasting compiling entire program before running it, testing and debugging incredibly fast
- massive standard library out of the box, inbuilt tools for handlign text processing, file management, internet protocols, basic mathematics without installign extra software
- cross platform : exact same script run seamlessly on windows, macos and linux and cloud servers


**a. Dominates machine learning and agentic ai frameworks**
b. **Syntax simplicity**
c **Massive ecosystem, millions of libraries for any task imaginably**

- default lang of ML, llm NN and agentic orch, built on python
- langgraph also natively written in python
- **Hosts a registry called the Python Package Index** ( PyPI), high chances anything u need to do, be it scrape a website , build a web application, analyze a spreadsheet, connect to llm api, build game, someone has already written highly optimized package for it that we can install with a single command
- backed by tech giants


# Why FastAPI?

modern, high perf web framwwork for creating APIs, with python. Specifically built to handle comm btw frotnend, mobile app, ml model, and database.

near best industry practice over django and flask

- blazing fast perfomance : fastest python frameworks available, speeds comparable to node and go, achieves by ASGI, ks of concurrent server requests simulatenously w/o slowing down
- native async support : has built in support for python await and async keywords, allwos the server to activate asgi, 
- automatic interactive documentation : fan favourite, the second we write code, fastapi automatically generates /docs, instantly test live api endpoints directly from browser, no tools like postman
- fastapi built directly on top of pydantic : data validation on top, before ever processing it


**SO FAMOUS DUE TO 3 reasons : **
- **AI backend standard : **ideal for deploying llm and rag apps
- reduces bugs by 4-% using type hints and auto docs
- powers major tech


## Websockets 
provide a permanent 2 way connection between a user browser and a server over a single tcp connection, allow data to flow instantly in both dirs w/o delay of traditional web requests

**WHAT ARE THEY?**
- persistent link : a conti connection that stays ope until closed by either party
- bi directional : both client and server can send messages at any time independently
- full duplex : data flows simul in both directions over 1 channel
- real time ; ideal for live chats, multiplayer games and finances

**How they work?**

HTTP handshake request -> 101 switching protocols ( connection upgraded ) -> bi directional -> data frames ( persistent tcp tunnel ) -> close frame -> close acknowledgement

**How do they do what they do?**
- the handshake : client sends a standard http request asking to upgrade the conn
- protocol switch : server replies with an HTTP 101 switching protocols
- tcp tunnel : http protocol is discarded leaving the raw tcp socket open
- data framing : data is broken into tiny packets called frames with minimal overhead
- unlike http : messages skip heavy headers, cookies and auth checks after setup 

**Overhead : **any extra data, time or processign power required to completea task that does not include the actual message being sent, **for eg: **envelope stamp, address lines on physical letter :, necessary to deliver the letter, but not included in the message inside

HTTP Overhead : in traditional http, every single msg requires a heavy wrapper, every time we send a chat message, browser attaches : 
- headers : text strinsg detailing the browser type, lang and content format
- cookies : identification data sued to track your session
- security tokens : repeated proof of who i am
extra data adds a lot of storage or memory, which is thrown away in websockets, by the help of data frames, which **reduces the wrapper to the absolute bare minimum**

**WHY MINIMAL OVERHEAD?**
 
- tiny headers : 1000 bytes long text headers and overhead, scrapped, websoc frame uses a binary header that is 2 - 10 bytes long
- no cookies : server already knows who we are cause conn stayed ope frm the start
- almost the entire network packet consists of my actual message

Why matters ?
- when the overhead minimal, massive amounts of bandwidth saved and reduce lag

WEBSOCKETS

**Data framing done by **breaking your msg into a sequence of structured binary packets called frames. websocket protocol automatically handles this by wrapping your raw data in a highly optimised header

anatomy of a websocket frame 
- websocket frame uses bits and bytes to transmit info

**scikit-learn **

widely used python lib, provides simple and efficient tools for ml and predictive data analysis
- serves as standard gateway for developers and data scientists turning from basic data anaylysis to ml

why used?

scikit learn handles traditional ml tasks out of the box, built on top of python's core scifi computing packages, numpy, scipy and matplotlib, allowing : 
- clean data : prepare scale and normalzie messy raw datas
- train models : ru algos for classific (spam detection), regression (house price prediction), clustering (customer segregation)
- evaluate accuracy : split data into training/ testing sets and score model performance 


**why choose scikit ?**
dominates trad ml, 3 main pilars : 
- unified api : forced every ml algo touse the same intuitive code layout
- ml requires lot of steps before actual prediction : scikit learn pipeline utility chains all data-preprocessing steps and the final algorithm into a single, clean object, eliminates leaking bugs into testing data

- optimised for cpu and trad data : explicitly optimised for tabular data, (like excel or sql db), running on standard computer processors (cpus), written in heavily optimised c, making it incredibly fast and lightweight for datasets that fit inside a computer's memory

scikit learn : mostly for basic ai ml algos and tabular data, xgboost (for extreme speed )

**FLUTTER : **
free open source sdk, created by google for building beautiful natively compiled apps for mobile, web, desktop and embedded devices from a single codebase

- allows devs to write code once and deploy it everywhere, instead of hiring multiple for diff platforms, a single dev can use flutter to target both platforms, uses dart language : 
- complex ui design
- state management : tracking user inputs, logisn and app data flow
- hardware access : conncting to device cameras, gps and bluetooth

**while cross platform has existed for years, flutter r**evolutionised industry cause of 3 specific architectural breakthroughs : 

- bypasses the native platform ui (canvas engine) : trad frameworks like react native act as bridge for translating code into phone's native buttons and switches, which slows things down and causes apps to look diff on older phones

- flutter does not use phone's ui for components at all, acts like a high performance video game engine and draws every single pixel, button and animation into blank screen canvas, allows : 
                          - flawless 120hx perf with 0 fram edrop or lag
                          - total ui consistencty app looks excat same on phoen android iphone or browser

- everything is a widget : uses deeply nested declarative ui structure, where abs every thng - from a layout grid, text label,  padding space,  touch gesture, **is a widget**. Allows extreme consistency and makes ui compostiion predictable

- true stateful hot reload : flutter's compiler injects updated source code files into the running dart virtual machine in under a second, **and does this WITHOUT LOSING THE APP STATE. if we **are 5 screens deep into testign and want to change color of button, color changes instantly and we dont even move on the app.

  **DOCKER : **
open source platform that packages softwares into lightweight isolated units called **containers, **bundles an app's source code together with all the specific libs, config files and dependencies it needs to run, ensuring it works perfectly on any computer. 

- solves the classic " works perfectly on my computer ", before docker, moving an app from dev laptop to testing server and then to cloud provided, **frequently** caused crashes due to subtle differences in operating systems, softwar everisosn and system settings, **docker** completely eliminates that isue by locking the env to a standard container. 

docker's global dominance to 3 key architectural advs : 
- containers vs virtual machines : before dockekr isolating apps required vms, and vms are heavy and each one must bundle full copy of a guest os, virtual hardware drivers, and system files. Takes gbs and mins to boot up.

- docker containers share the host's computer os kernel instead of creating a new one, multiple containers run as isolated processes directly on main os, **this architecture yields masisve benefits : **
                              - size : containers are mbs instead of gbs
                              - speed : containers boot up instantly in millisecs, just like regular app
                              - efficiency : can run dozens of docker containers on a laptop that would crash running 3 vms

- immutable image layer system : docker images are built using a real only, layered file system, every instruction is a config file (dockerfile) creates a new layer : 
                              - if u update app's code but nothing changes, docker only downloads or uploads the tiny layer containing code change
                              - layers below it (like the os baseline or db drivers) are cached and reused instantly, making deployments incredibly fast

- standardized infrastructure as code : docker allows u to define ur entire infra in a simple text file (dockerfile), this turns ur environment setup into code that can be tracked in git, peer-reviewed, and automated. Anyone on ur team can download the file, run 1 command, and have an exact copy od the production server running locally in secs. 





 





