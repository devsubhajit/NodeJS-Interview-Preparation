**Note:** This repository is specific to NodeJS.

### Table of Contents

| No. | Questions |
| --- | --------- |
|   | **NodeJS Fundamentals** |
|1  | [What are the outputs for "x = 10" and "var y = 20" in node cli?](#what-are-the-outputs-of-below-codes-in-node-cli) |
|2  | [What is event loop in nodejs?](#what-is-event-loop-in-nodejs) |
|3  | [What is event emitter?](#what-is-event-emitter) |
|4  | [How to create custom event emitter?](#how-to-create-custom-event-emiter) |
|5  | [Create a basic server?](#create-a-basic-server) |




## &nbsp;
## &nbsp;

## Answers

1. ### [What are the outputs for "x = 10" and "var y = 20" in node cli?](#what-are-the-outputs-of-below-codes-in-node-cli?)

    Whenever we declare a variable without **var/let/const** this got directly assigned to the global object. Like for node, whenever we are typing **x=10**, basically we are typing **global.x = 10**.

    But when we type **var x = 10;** this will first hoisted with the initial value ***undefined*** that's why it returns undefined.

**[⬆ Back to Top](#table-of-contents)**

2. ### [What is event loop in nodejs?](#what-is-event-loop-in-nodejs)
    Nodejs has a **Chromes V8** engine in its heart and **Libuv** to provide **threads**.
    Like Javasscript NodeJs is also **single threaded**. So all the execution context goes through the Call Stack, which is LIFO (Last in first out). 

    Now from the above information, its quite obviou that if codes are syncronised then there is a changes of code blocking as nodejs is single threaded.

    To solve this, NodeJs has the Event Loop mechanism, which performs all callback functions, any api/ promises/ timer functions goes to the callback queue and message queue (in ES6 promises goes to ES6 Job queue) from call stack, and while these APis are performing, nodejs doesn't block the call stack and continues it's executions. Now the event loop basically checks the call stack, if it is empty then event loop takes the task from callback queue and pass it to call stack. 

    This way nodejs doesn't block the execution context and this is known as Event Loop.

**[⬆ Back to Top](#table-of-contents)**

3. ### [What is event emitter?](#what-is-event-emitter)
    In javascript, which runs on browser, has many events which is interacted by user, such as, click, double click, keypress, etc. Similerly in backend in nodejs, there is a module **events** which allow us to create similar system. This module has a class EventEmitter which offers us to crate custom events as well.

        const EventEmitter = require("events);
        const myEvents = new EventEmitter();

        // function constructor way
        myEvents.on("start", ()=>{
            console.log("Event started!")
        })
        myEvents.emit("start");
        // class constructor way
        class Sales extends EventEmitter {
            constructor(){
                super();
            }
        }

        const salesEvent = new Sales();
        salesEvent.on('sale',stock=>{
            console.log(`${stock} stocks has been sold`);
        })
        salesEvent.emit('sale', 10)



**[⬆ Back to Top](#table-of-contents)**

4. ### [Create a basic server?](#create-a-basic-server)

        const http = require("http");
        const server = http.createServer();

        server.on('request',(req, res)=>{
            console.log("Reqest accepted");
            res.end("Request Accepted!")
        })    

        server.on('close',()=>{
            console.log("Server has been closed");
        })

        server.listen('8080', '127.0.0.1',()=>{
            console.log("Server started on port 8080")
        })

**[⬆ Back to Top](#table-of-contents)**
