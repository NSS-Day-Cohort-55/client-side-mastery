## Functions that Give Back

In the introduction, you invoked a function that had a single parameter so that you could fill up a car's gas tank with any specified number of gallons. The function itself defined a very basic task that just wrote a message to the console. This is usually not the case.

Most of the time, functions actually give you something back after the task is complete. This is because software developers use functions to define transformation or calculation tasks. That sounds fancy, but it's not.

Here's a simple example.

## Half the Number

Sometimes your brain just forgets all the math that it learned in high school and college. Finding what half of a number is sometimes beyond your capabilities, especially if you haven't had coffee yet.

You decide to write a function that performs the task for you. A little Math Minion.

You tell the minion what number needs to be provided. That's a parameter.

```js
const findHalf = (scaryNumber) => {
	// Use the slash character to divide in JavaScript
	const half = scaryNumber / 2
}
```

So far, the minion did its job, but it never told you what the end result is!!

Bad minion.

You need to provide instructions to the minion to tell you what the answer is. You use the **return** keyword for that.

```js
const findHalf = (scaryNumber) => {
	// Use the slash character to divide in JavaScript
	const half = scaryNumber / 2

	// Tell me the end result
	return half
}
```

Now when the task is complete, the minion will hand you the end result of its hard work. It **returns** something to you. When a function returns a value, you must store that value in a variable. Remember that variables store values, including ones that functions return.

```js
const returnedNumber = findHalf(42)

console.log(returnedNumber)

> 21
```

## Write this Down. Read it Often.

There's a mantra that you need to remember when working with functions. It will save you heartache in the future.

**If a function returns a value, you must store that value in a variable**

You will practice this mechanism many times because this flow of data and syntax is not natural to understand or remember. It is, however, crucial to build into your muscle memory until it does make sense.

**If a function returns a value, you must store that value in a variable**

## Practice: Cut into Pieces

### Setup

```sh
cd
cd workspace
mkdir functions-parameters
cd functions-parameters
touch main.js
```
OR, you can use the `mg` and `simplehtml` commands from the terminal chapters. It's your choice. There are many ways to solve problems, even ones as simple as "I need to create a new project." Quick thought exercise while we're on the subject -- why might you use one way of creating a project over the other? What are the pros and cons of each? Take a moment to write down your thoughts. It's a super simple problem, but thinking about which approach to creating a new project you want to use will prepare you for much bigger problems abd decisions down the line. Bonus points if you bring this up in the next live coding session and ask the instructors if you can discuss your thoughts on this. 

However you get your files ready to roll, finish setup with a quick `code .` Once VS Code starts, open the `main.js` file and follow the instructions below.

### Instructions

Here is some starter code for a function named `quarterValue`. Add it to `main.js`.

```js
const quarterValue = () => {


}

// Invoke the function and store the return value


// Log the return value
console.log()
```

It will work very similarly to the `findHalf()` function shown above. What you need to do is complete the following tasks:

1. Define a parameter that will hold the value of the original number.
2. Divide that number by 4
3. Return the quartered number
4. Store the returned number in a variable
5. Plug that variable into the parenthesis for the `console.log()`
6. When you run the code, you should see the answer in the console.

### Helpful hints

You can expand the hints below if you are stuck and don't know what to do. Make sure you try a few times and fail, and then talk with your teammates before looking at the hints.

<details>
    <summary>Hint: Defining the parameter</summary>

    const quarterValue = (startingNumber) => {


    }

    // Invoke the function and store the return value


    // Log the return value
    console.log()
</details>

<details>
    <summary>Hint: Dividing by 4</summary>

    const quarterValue = (startingNumber) => {
        const quartered = startingNumber / 4

    }

    // Invoke the function and store the return value


    // Log the return value
    console.log()
</details>

<details>
    <summary>Hint: Returning the new value</summary>

    const quarterValue = (startingNumber) => {
        const quartered = startingNumber / 4

        return quartered
    }

    // Invoke the function and store the return value


    // Log the return value
    console.log()
</details>

<details>
    <summary>Hint: Invoking with an argument</summary>

    const quarterValue = (startingNumber) => {
        const quartered = startingNumber / 4

        return quartered
    }

    // Invoke the function and store the return value
    const result = quarterValue(256)

    // Log the return value
    console.log()
</details>

<details>
    <summary>Hint: Logging the result</summary>

    const quarterValue = (startingNumber) => {
        const quartered = startingNumber / 4

        return quartered
    }

    // Invoke the function and store the return value
    const result = quarterValue(256)

    // Log the return value
    console.log(result)
</details>

> NOTE: Of course you noticed that this is a whole new project in a new directory ( `functions-parameters` ) with its own set of files. You know what that means. Time to initialize a new git repo ( `git init` ) and prepare your code for pushing to Github. You know the drill by now. If not, review the git chapter again and give it a shot. Still intimidated by git and Github? Run right at it, not away from it. You will be using git every day. Now is the time to practice it and ask for help!
