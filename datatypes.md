

In every generic human language, there are parts of speech and rules that guide the usage of such. In the English Language, for example, we have parts of speech like *Nouns*, *Pronouns*, *Verbs*, *Adjectives*, etc. The English Language as a human language is used for communication, while **Javascript as a higher level programming language is used to add functionality to web pages** ie *It makes user interaction with the web page possible*. 

In This article, I will be going over the major Data Types in Javascript which can also be referred to as **values**.
This write-up is beginner friendly and an introductory insight to data types for anyone new to the Javascript world. Below are the 7 major Data Types in Javascript.

* Number
* Bigint
* String
* Boolean (logical type)
* null
* Object
* undefined

## Number

The **number** data type is like a generic number we are all familiar with for basic arithmetic operations like multiplication `*`, division `/`, addition `+`, and subtraction `-`. *Number* can either be **floating point number** (decimals) or **integer** (whole numbers)

```
let number = 5;
let floatingNumber = 1.234;

let addition = 5 + 5;
console.log(addition) //10
```
we can perform any arithmetic operation on numbers and have their results stored in a variable to be used anywhere else in our code base.
Aside from conventional numbers, we have 3 unique numerical values which are
`infinity`, `-infinity`, `NaN`.

* `infinity` results when we divide a number by 0 which is greater than any numeric value

```
console.log(1 / 0) //infinity
```

* `NaN` This stands for *not a number* it results when you try to perform an incorrect arithmetic operation. for example when we try to divide a *string* with a *number* 

```
console.log("word"/5) //NaN
```


## Bigint

**Bigint** is a way to represent whole numbers in computer programming that are larger than **253-1** or **-(253-1)** for negatives.
integers greater than **253-1** can not be stored in the *number* type so Bigint was created to accommodate this change to numbers with unconventional lengths.

A *Bigint* value is added by appending `n` to the end of the integer.

```
const bigInt = 1234567890123456789012345678901234567890n;
```

you might begin to wonder about the practicality of applying the Bigint value in the wild, though it's not regularly used and you may never encounter them in a code base but they can be used for cryptography or microsecond-precision timestamps which are outside the scope of this tutorial.


## String

**String** are basically characters in javascript, just like a string of alphabets makes up a word in the English Language, a string is a combination of characters, although for beginners the name sounds counter-intuitive, always remember that *strings* in Javascript are characters. A *string* can also be empty `" "` or `''`.

*string* can be denoted in 3 different ways.

```
let string1 = "javascript"; //double quotes
let string2 = 'javascript'; //single quotes
let string3 = `javascript`; //backticks
```

*backticks* are really powerful in javascript because it allows us to interpolate values, by wrapping them in 
`${…}` 

```
let name = "David";
let phrase = `My name is ${name}`
console.log(phrase) //My name is David

console.log(`The sum is ${1 + 2 }`) //The sum is 3
```
There is basically no functional difference between the *single quotes* `' '` and the *double quotes* `" " ` it all boils down to personal preference and style.  


## Boolean (logical type)

A javascript *boolean* represents either one of two values. **true** or **false**.

**true** resulting in *yes*
**false** resulting in *no*

**boolean** values are very effective in toggling eg *turning a switch on or off*, *displaying a drop-down or a hamburger icon or not*
Note that everything with a value results in *true* and *false* if there is no value.

```
console.log(5 > 4) //true

let isNameAString = true;
console.log(isNameAString); //true

let isUserValid = false;
console.log(isUserValid) //false
```
values can also be set to either *true* or *false*


## Null

**Null** is a special value in Javascript that denotes *empty*, *nothing*, *unknown value*.

```
let name = null;
console.log(name) //null
```
`name` is intentionally absent, *null* is the intentional absence of any value.


## Objects

**Objects** are special data types in Javascript that are used for storing the collection of values (which can be of any data type) in a `{key: value}` pair. *keys* in objects can also be referred to as *properties*. In javascript, other data types are called *primitive values*, while objects are referred to as *reference values*. 

```
let human1 = {
    firstName: "David",
    lastName: "Olaleye",
    isAnEngineer: true,
    legs: 2,
    children: null
}
```

The code above is an example of an *object literal* syntax. Objects are very complex data types and going deeper is outside of the scope of this tutorial. An object is one of the major building blocks of **Object Oriented Programming**
 
Object properties can also be assigned.

```
human1.firstName = "Mike"
console.log(human1.firstName) //Mike
```
In the example above, we set the `firstName` property of the human1 object from string`"David"` to the string `"Mike"` using the **. notation**. This can also be done with the *square bracket notation* below

```
human1["firstName"] = "Ed";
console.log(human1["firstName"]) //Ed
```


## Undefined

**undefined** is another special data type in javascript that denotes that a value is not assigned.
In javascript, a value can be declared and assigned later. 

```
let name;
console.log(name); //undefined 
```
The name variable above was declared but not assigned with a value.

```
name = "David"
console.log(name) //David
```
The name variable above has been assigned a *string* value `"David"`.

### Note:
We can assign `null` to a value if it is *unknown* or *empty* but it is not advisable to assign `undefined`
to a value explicitly. *undefined* is specially reserved for unassigned values as a default. 

## Wrapping Up
In this article we covered the major data types we have in javascript. Although this is meant to be beginner friendly, as you go on in your web development career, you will begin to learn about these data types in depth (caveat, trade-offs, and best practices). I do hope you have gotten some sort of introductory insight in this article, Thank you for your time, and good luck in your journey. Remember, *it is a marathon and not a sprint*.

I will appreciate your feedback through [Twitter](https://twitter.com/SIRchievous/) 
 [GitHub](https://github.com/Pisces2802) [Linkedin](https://www.linkedin.com/in/david-olaleye-960435166/)
