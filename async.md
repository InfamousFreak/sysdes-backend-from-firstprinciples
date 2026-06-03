# ASYNC
**ASGI : Asynchronous Server Gateway Interface, **standard specification that allows python webservers and web frameworks to talk to each other asynchronously, 

allows python to build hihgly concurrent applications, real time chat apps, streaming ai interfaces, and fast apis ( pun intended ), 

wsgi ( web server gateway frameworks ) used by django and flask, (**strictly synchronous, single threaded and sequential )**

**THE WSGI PROBLEM : **when a requst comes to wsgi server, it locks up entire execution thread, if the app needs to call a slow db or wait 10 secs for an llm api to respond, entire thread sits idle and blocked, cannot handle any other incoming user requests until that single task finishes

**THE ASGI SOLUTION : **asgi completely removed this bottleneck, allowed a single server thread ot process 1000s of requests concurrently, if req #1 is waiting for an external database or an AI model to stream text, asgi server instantly pauses it, switches over to handle req 2, loops back to req the millisecond the data arrives.

Core Differences: WSGI vs. ASGI

| Feature                  | WSGI (Older Standard) | ASGI (Modern Standard) |
| Execution Style   | Synchronous (Block and wait). | Asynchronous (Non-blocking / concurrent). |
| WebSockets         | No native support (Requires messy hacks). | Native support out-of-the-box. |
| HTTP Streaming  | Poorly suited for long-lived connections. | Native support for streaming (e.g., streaming LLM text). |
| Best Frameworks | Flask, Django (traditional). | FastAPI, Litestar, Django Channels. |


**USE CASES OF ASGI IN MODERN TOOLS : **

- **streaming llm responses : **text stream word by word, real time streaming relies on server sent events or websockets, both require an ASGI backend to run efficiently w/o crashing under traffic
- **real time data pipelines : **asgi handles persistent bidirectional connections like websockets perfectly, makes it go to standard for live chat applications, that need to push instant updates to frotnend dashboard
- **maximising server hardware : **as asgi does not waste tiem waiting around on idle conns, require significantly less ram, to handle the same amount of traffic as traditional wsgi

ASGI FRAMEWORK : fastapi, asynchronous and realtime
ASGI SERVER : uvicorn and hypercorn are actual excution engines that run code on server machine, listen for incoming traffic and manage asynchronous loops



CORE WSGI Architecture : single threaded event loop -> wsgi servers also handled concurrency, just that very inefficiently, spawning massive amounts of opersting system threads or processes, if 500 users waiting on slow llm apis, 500 threads idling in memory, crashes the server.

ASGI : uses single thread, non blocking event loop, (python *asyncio)*
- instead of new thread for every user, asgi processes all reqs inside a single hyperefficient loop
- like a garry kasparov playing 50 chess gms

**The mechanics : Coroutines and *yield***

Under wsgi architecture, funcs are rigid blocks, once 1 func starts running, controls the gpu till it explicitly returns an output.

asgi relies on coroutines (declared by *async def ) *: co-routines have a magical property, **they can voluntarily pause themselves and yield control back to the event loop.**

_now as the function hits a io bound op and waits for an llm.call() response, it freezes the local state and step aside, **now the event loop ( the orchestrator ) instantly uses the exact same cpu power to handle a brand new incoming req. **_

- now when the respnonse for llm.call has been received, the event loop wakes the frozen function up and finishes its execution

## Data structure : Asynchronous Dictionary Passing

Wsgi passes data as a single, static string/env dictionary, server reads the request, hands the dic to django/flask, waits for single response string back, ***makes persistent data streams impossible.***

ASGI re-engineered this to 2 decoupled, asynchronous comm channel : 

- connection scope : dic containing static metadata about the incoming connection

- **2 async callbacks (*receive ***& ***send) : ***this the secret sauce, instead of waiting for the single data payload, the asgi framework and web server talk to each other continously via 2 async functions : (*receive()) : allows the app to *stream incoming data from the client asyncly 

  (*send()*) : allows the application to push data fragments back to client at any time


Concurrency driver  : Multi threading (wsgi), single threaded event loop (asgi)
Func exec : run to completion (blocking), suspend and resume (await)
IO handlign : cpu sits idnel during network requests, switches tasks during network requests
Data flow : single request in, response out, but asgi has continuous receive and send data streams



             