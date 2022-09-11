👋 Hello guys! What if I told you `console.log()` is not a part of javascript? 😲 or that `setTimeout()` or `alert()` aren't part of javascript as well? 🤯 I can see the gape in your mouth and the askance in your countenance at the moment which is understandable, that was how I felt as well when I initially realized it. 

This article is a sequel to [part 1](https://devdave.hashnode.dev/how-javascript-works-behind-the-scenes-part-1)  of the workings of the javascript engine. 

We will be talking about the *non-blocking* and the *asynchronous* part of javascript, I mean we will be looking behind the scenes to see how javascript which is a *synchronous single-threaded language* runs *asynchronous* operations.   

From the [previous article](https://devdave.hashnode.dev/how-javascript-works-behind-the-scenes-part-1), we saw how javascript runs our code in a synchronous manner from top to bottom. This is because javascript has only one call stack which it uses to execute the code. 

Imagine we had to load our tweets to the UI (user interface) in a synchronous manner, the javascript engine will read and parse the code line by line and when it gets to the line of the tweet request, the page will be non-responsive to clicks because we have to wait to get the data from an external source before other lines of code can resume execution. That doesn't seem like a very good user experience, right?


![javascript run-time environment.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662597117946/ZC-5cgRKO.png align="left")

The image above is a pictorial representation of the javascript run-time environment. From our previous article, we can identify the *Call Stack* and the *Memory heap* and their functions in running our code synchronously (line by line, top to bottom). The other parts are the:

### Web APIs
### Callback Queue
### Event Loop

We will run a short example below by simulating an asynchronous code execution with the `setTimeout()` function.


```
console.log("first");

console.log("second");

function printName() {
    console.log("My name is David");
}

setTimeout(printName, 2000);

console.log("End of the program");

```

Judging by our synchronous programming knowledge, in what order do you think the code above will be executed?

let's take this step by step.

first of we are in the Global Execution Context (window environment), and our code will be read from top to bottom in order to allocate memory to variables and function bodies in the *Memory Allocation Phase* 

`function printName() {....}` would be stored in a *key: value* pair with the function name *printName* as the key and *undefined* as the value. Now the Code Execution phase. `console.log("first")` being a function invocation will be pushed on the Call stack and a *Functional Execution Context* will be created.

 The string value *first* would be logged to the screen, the console would be popped off the Call stack, and that function execution context would be gone. 

`console.log("second")` would go through the same process of getting pushed to the Call stack and also creating a *Functional Execution Context* and log the string value *second* to the screen, the function will be popped off the call stack and the function execution context gone.

We will skip the `function printName() {....}` line because it hasn't been invoked and we do not have access to the gate `{ }`

Now something interesting is happening, we have a `setTimeout()` function with a *callback function* and a *timer* inside of it.

from our rudimentary knowledge of the javascript engine and how it works, we know that the javascript engine does not have a timer attached to it, which means that the javascript engine itself is not equipped to schedule the execution of operations. 

This is where the **Web APIs**, **Callback queue**, and the **Event loop** comes in. Now back to the first statement of this article, `console.log()`, `setTimeout()` are part of the Web API that helps us in executing asynchronous operations in javascript

This makes up the *javascript run-time environment* in the Web API, we have a timer that helps in scheduling executions of function that is measured in *milliseconds*. 

So `setTimeout(printName, 2000)` means execute the `printName` function in 2000 miliseconds (2 seconds) BUT continue running the other code in our program. 

This is where the **non-blocking** part comes in. Take 2 seconds to store the `printName` function in the Web API land but in the meantime, **DO NOT BLOCK THE THREAD OF EXECUTION** in our program because javascript doesn't wait for anyone.

So the question now is *where is `printName()` sent off to? and how do we get our result back into the *javascript land*

Hence the behavior below


![async_setTimeout_example.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662597490153/mGXeMnuGJ.png align="left")

`setTimeout()` itself being a function is also pushed to the Call stack and a function execution context is created but it's immediately shipped to the Web API environment with the *timer* attached to it, meanwhile, our code continues to run in javascript land nonetheless. Immediately after the timer is exhausted, the function `printName` is pushed onto the **Callback queue**.

The **Callback queue** unlike the **Call stack** has a data structure of FIFO *First in First out*. It is a queue, just like a conventional queue at the store, it's on a first-come, first-served basis. 

So function `printName` is queued for execution in the  Web API land (callback queue) looking to get back into javascript land. So how does this transition occur?

This is where the **Event Loop** comes into action to save the day. The loop has only one job and this job is to monitor the call stack to see if there is any function waiting to be executed.

 Let's say we had 100 lines of code after our `setTimeout()` function, as long as they are synchronous, javascript will keep executing them allocating memory, pushing to the call stack, and creating functional execution context (which is its major job).

Immediately after the call stack is empty, the **Event loop** will keep monitoring to check if we have any function in the call stack and if we have any function in the callback queue, if the stack is empty, the function in the queue will be pushed to the call stack.

 Which in our case is the function `printName` and we will go through the same process of creating a functional execution contest and then log the string value `My name is David` to the console. Which explains the behavior above. 

Now you might ask, *What if we set our timer to 0?*, will it change the behavior of our code? let's see that in action.

```
console.log("first");

console.log("second");

function printName() {
    console.log("My name is David");
}

setTimeout(printName, 0);

console.log("End of the program");

```

![async_setTimeout_example2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662597511150/XghhLN2cR.png align="left")

Voila! It doesn't matter, right? we will still go through the same *Web API* --> *callback queue* --> *event loop* --> *call stack* process, only this time with 0 milliseconds timer in the web API land. So if we had hundreds or thousands of lines of synchronous code to run, javascript will wait for no one until it's done with its tasks.

I know this can be a lot to take in, it took me a while as well. I do hope you've got some introductory insight 💡 into how **javascript is a synchronous single-threaded language that can be non-blocking**. 

Thank you for your time, and good luck in your journey. Remember, *it is a marathon and not a sprint*.

I will appreciate your feedback through [Twitter](https://twitter.com/SIRchievous/) 
 [GitHub](https://github.com/Pisces2802) [linkedin](https://www.linkedin.com/in/david-olaleye-960435166/)

