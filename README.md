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
|6  | [What is callback hell?](#what-is-callback-hell) |
|7  | [How to handle call back function?](#how-to-handle-call-back-function) |
|8  | [What is API?](#What-is-API) |
|9  | [Why does a REST API should be stateless?](#Why-does-a-REST-API-should-be-stateless) |




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


**[⬆ Back to Top](#table-of-contents)**

4. ### [How to create custom event emitter?](#how-to-create-custom-event-emiter)
    Creating customer event emitter is a lot easier than we are thinking. Lets start creating a custom event emitter

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

5. ### [Create a basic server?](#create-a-basic-server)

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

6. ### [What is callback hell?](#what-is-callback-hell)
    A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

    NodeJs / Javascript is desigend to be non-blocking, for that we have callback functions. But callback inside callback becomes very challening to manage. This creates a triangle pattern in code view. This is known as callback hell.

        const myFunction = () => {
            setTimeout(() => {
                console.log("level 1");
                setTimeout(() => {
                    console.log("level 2");
                    setTimeout(() => {
                        console.log("level 3");
                        setTimeout(() => {
                            console.log("level 4");
                            setTimeout(() => {
                                console.log("level 4");
                            }, 1000);
                        }, 1000);
                    }, 1000);
                }, 1000);
            }, 1000);
        }

    From the example as you can see, we are calling functions inside another continuously creates a callback hell.

**[⬆ Back to Top](#table-of-contents)**

7. ### [How to handle call back function?](#how-to-handle-call-back-function)

    To get rid of callback hell, **promise** was introduced in ES6, and later on in ES8 **async await** method has been introduced.

    By using **promise chain** or **async await** we can solve collback hell issue.

    * Promise Chain

            promise1(data).then(data => {
                return promis2;
            })
            .then(res => {
                return promise3;
            })
            .then(() => {
                console.log('all done!');
            })
            .catch(err => {
                console.log(err);
            });
    Ase you can see instead of triangle code, promise chain is a flat expression of code, which is a lot easier than callback.

    * Async Await
            const asyncFunc = async ()=>{

                const data_1 = await promis1;

                const data_2 = await promise2;

                await promise3;

            }
    Async method is lot easier than both promise chain and callback hell

**[⬆ Back to Top](#table-of-contents)**

8. ### [What is API?](#What-is-API)

    Api Stands for **Application Programing Interface**, which basically talk between two softwars applications.

**[⬆ Back to Top](#table-of-contents)**

9. ### [Why does a REST API should be stateless?](#Why-does-a-REST-API-should-be-stateless)

    **State** means an inital data storage which keeps updateing on the user interaction or for any changes in the application. If in any api end point, we want to move to next page (in case of pagination), a state need to be maintained in server side, which will have the initial value of current page. So mainting this kind of operation on server side is very complex or bad idea. That's why Rest APis should be stateless.

    * with state

            // api
            Get  /users/nextPage

            // State on Server
            nextPage = currentPage + 1;
            send(nextPage);

    * Without state / stateless
            
            //api
            Get /users/6

            //Web Server
            send(6)



**[⬆ Back to Top](#table-of-contents)**



