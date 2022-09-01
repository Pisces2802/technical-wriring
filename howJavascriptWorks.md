### Javascript  Is  A  Synchronous 
### Single-Threaded  Language 
### That  Can  Be  Non-Blocking.

👋 This is the first part of an introductory article on how Javascript executes our code behind the scenes. If you have been familiar with javascript for a while (or not), you would most likely have come across the statement above and if you haven't, consider yourself informed 😎. 

Personally, it took me a while to wrap my head around the *single-threaded* and *non-blocking* concept of Javascript as a programming language 😕. To fully understand how codes are being executed, you need to understand how Javascript was designed to run. 

This will greatly help in fixing bugs, writing cleaner and easy-to-understand code, and also help new developers in their development journey. I will try as much as possible to simplify the concepts in this article to be easily understood. You might need to refer to it over again for it to stick, all you need is a heart willing to learn and a smile on your face 🙂

 **What is a program?**

A program has to do 2 things.

* Allocate Memory
* Parse and Execute

*Allocate memory* : This means that a program should be able to store values as variables.
```
var variable = "value"
```

*Parse and execute*: A program should be able to run commands passed to it, this includes executing functions and other operations based on the values in the memory.

```
function printValue(a) {
    console.log(a);
}
printValue(variable) // value
```
Javascript can effectively run these operations because of the Javascript engine, and in the Google Chrome browser, it's called the **V8 engine**. The **V8** engine reads the code we write and changes it to machine-executable instructions for the browser which then adds functionality to our page. 

The Javascript engine has 2 major parts which are:

* Memory Heap
* Call Stack

*Memory heap*: This is where the memory allocation occurs.
*Call stack*: This is where our codes are executed and it also shows where we are in the program.  

Javascript being a single-threaded language simply means it has just one Call stack used in executing the instructions in the program. The Call stack has a FILO *First in Last Out* structure of execution. Since Javascript is single-threaded, it means it reads our code line by line in a specific order (from top to bottom).

If you have had some experience with javascript you might begin to wonder *If Javascript is a synchronous single-threaded language, how then do we perform asynchronous operations?* 

Though that's presently out of the scope of this part, performing asynchronous operations is possible due to the web API that's part of the browser which makes up the **Javascript Run-Time Environment**. We will talk more about this in the sequel. 

Every execution of code in Javascript occurs in an **Execution Context**
* The Global Execution Context (window)
* The Functional Execution Context.

*The Global Execution Context* is the first context that is created immediately after the page is loaded even before any line of code is run. 

```
var name = "David";
```
the variable `name` is parsed and stored on the window Object in *key: value* pair.


![variable_name.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992194642/Ypf4YwvLM.png align="left")

![window_name.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992216980/IzeyKE0Uc.png align="left")


`name` is added to the window Object

```
function myName() {
    alert("My name is David");
}

```

![myName_function.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992255136/zH3vq8wJ-.png align="left")

![window_myName.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992275877/-b8MEC9ym.png align="left")

 we can also see that `function name` is on the window object in a *key: value* pair.


 *The Functional Execution Contest* is only created when a function is invoked or called by `()`.

 ```
 function myName() {
    debugger;
   var name = "David";
    alert(`My name is ${name}`)
}

myName(); //My name is David
 ```
By putting a `debugger` in our function body, we're able to pause the function execution and step over at will to see the `local` section and the *Call stack* in our browser. 

`name` is a local variable to the function `myName` and it won't be on the Global Execution Context which is the **Window**.

![functionalExecContest.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992322655/kTigWJ3Zk.png align="left")

We can see in the highlighted part that immediately after the `myName` function was invoked, the function was pushed on the *Call Stack*


![callstack.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661992346489/fQoJL7FZR.png align="left")

And after the invocation of the `myName()` function, it is *popped* off the call stack.


Javascript code execution happens in 2 phases, the **Memory Allocation phase** and the **Code Execution Phase**

We will take another example for better understanding.

```
var number = 5;

function multiply(num) {
    var result = num * num;
    return result;
}

var multiplied = multiply(number); 
```
**Memory Allocation Phase**

The first thing that Javascript does is to allocate memory to all the variables and functions on the page ie it reads the page from the top to the bottom (depending on the Execution Context the thread of execution is).

#### Global Execution Context

| Memory                    | Thread of Execution |
|---------------------------|---------------------|
| number: undefined         |                     |
| multiply: { ...function } |                     |
| multiplied: undefined     |                     |

* The first line is `var number = 5` number is stored as a *key* and a special placeholder `undefined` is appended as the *value* in this first phase.

* In the second line, we have `function multiply () {}` the whole function body is stored also as a *key: value* pair. The *key* is the function name `multiply` and the *value* is the whole function body. 

* Always remember that only a **function invocation** or a **function call** can allow Javascript to enter a function. Have a mental image that the curly braces `{ }` is a gate to the function body and an invocation is a key to the function. 

* The third line is also a variable and will be stored as a *key: value* pair with the variable name `multiplied` as the *key* and `undefined` as the value.
Note that we are in the *Global Execution Context* during this phase.

**Code Execution Phase**
In this phase, this is when Javascript allocates the values to the variables and also invokes functions that create a new *Executional Context* and perform specific operations in our code base. The code is also read from top to bottom. 

| Memory                  | Thread of Execution |
|-------------------------|---------------------|
| number: 5               |                     |
|                         |                     |
| multiplied: multiply()  |                     |

* Our code is read again from top to bottom, `5` is appended to `var number` as the *value*.

* The second line is skipped because we can't enter the function body because it hasn't been called yet.

* Now this is where the magic happens, there is a function invocation in the next line `var multiplied = multiply(number)`.

Any time we see the parenthesis `()` in Javascript, two major things happen. 

1 A Functional Execution Context is created.
2 The function is pushed unto the Call Stack.

`Multiply()` being a function invocation then creates a new *Functional Execution Context* and then we repeat the same process of
*Memory Allocation* and *Code Execution* reading from top to bottom. 
 
 #### Functional Execution Context
In this phase, we will only be concerned with the content of the `function multiply() {}` because the invocation `multiply()` has now given us access through the gates `{ }` into the function body. 

As we know by now we have the *Memory Allocation Phase* where memory is allocated to the variables and functions inside the `multiply` function, this also includes the *parameter* `num` because it is local to the `multiply` function. 

**Memory Allocation Phase**

| Memory            | Thread of Execution |
|-------------------|---------------------|
| num: undefined    |                     |
| result: undefined |                     |

* `undefined` is appended as a placeholder for variable `num`.
* `undefined` is appended as a placeholder for variable `result`.

**Code Execution Phase**
We will be repeating the process of reading the lines of code from top to bottom in the `function multiply` and executing them.

| Memory     | Thread of Execution |
|------------|---------------------|
| num: 5     | 5 * 5               |
| result: 25 |  = 25               |

* `num` which is a *parameter* local to the `function multiply` is allocated with the value of `5` which is passed as an *argument* to the function invocation `multiply(number)`

* `number` is the variable that was stored in *Global memory* on the windows object. `number` is the argument that was substituted for `num` as the parameter.

* The local variable `result` stores the evaluated value  of `num * num` which is `5 * 5 = 25` in the *Functional Execution Contest* (local memory).

The keyword `return` being the last line in the `function multiply` body does something very interesting. 

It simply means returning the result of the computation in that function body to the Execution Context where the function was invoked which in our case is the *Global Execution Context* where variable `multiplied` was stored in memory. 

The value `25` would now be replaced with the placeholder `undefined`. so `var multiplied = 25`.

When Javascript encounters the `return` keyword in the *code Execution Phase* of our program,

1 The *Execution Context* is deleted. 

2 The function is popped off the *Call Stack*. 

3 The control of that function with its result (which can be of any data type including a function) is transferred to the *Execution Context* where the function was invoked. 

In our case, it was to the variable `multiplied` in the  *Global Execution Context* other times, it could be to another *Functional Executional Context* depending on how deep into the program we are.

I know this is a lot to take in, but it gets easier after a while, just make sure you reference this article as often as you can. In the subsequent text, we will be looking at the **non-blocking** part of Javascript. 

For us to vividly get the picture, we need to understand the other parts of the Javascript run-time environment that makes asynchronous programming possible.

I do hope you have at least gained some basic insight into how Javascript executes our code, Thank you for your time, and good luck in your journey. Remember, *it is a marathon and not a sprint*.

I will appreciate your feedback through [Twitter](https://twitter.com/SIRchievous/) 
 [GitHub](https://github.com/Pisces2802) 














