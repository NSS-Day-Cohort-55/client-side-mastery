# Daily Journal Semantic HTML and Layout

Use your wireframe as a guide to create the HTML for your daily journal. 

## Project Directory and Initial Files
Use the terminal to create the following directories and files.
1. Create a new sub-directory in your `workspace` directory named `daily-journal`.
1. In that directory, create an `index.html` file.
1. Create a sub-directory named `scripts`. This directory will contain all of your future JavaScript files.
1. Create a `styles` sub-directory and within it, create a `main.css` file.

Once those are created, in your terminal make sure you are in your root directory (`pwd`) and open Visual Studio Code with the `code .` command. Once it launches, you are ready to start coding.

### Boilerplate HTML Code

Open your `index.html`. Visual Studio Code provides many shortcuts and can write boilerplate code for you, which you can customize for your needs. Just type in the letters `html` and the Intellisense context menu appears. Choose the "html:5" item to get some boilerplate HTML.

* Inside the `<head>` tag, create a new line, type in `link` and choose the "link:css" item. Change the href to `styles/main.css`
* Within the `<head>`,  be sure to give your page a `<title>`.

## HTML Layout

Refer to your wireframe and write semantic HTML for the page.

* Start broad with `<header>`, `<main>` and `<footer>`.
* Get more specific with `<section>`, `<article>`, and `<form>`. (Don't worry about the details of the form - you will build that out below).
* Get more specific with `<h2-h6>`, `<p>`, and `<a>`.
* Continue this process until you block in the page with all of the details from your wireframe.


## Build the Journal Form

You are going to use the `form`, `fieldset`, `label`, `input`, `textarea`, `select`, and the `option` elements to build your form.

The first step is to create a date field.

![date field creation](./images/MArcqtbyj6.gif)

Then create an `<h2>` element above the form containing the text _Daily Journal_.

Save your file. Go to the terminal. Type in `serve`. Then view the page in Chrome. Be sure to open your dev tools to ensure you aren't viewing a cached version of the site. Refresh the browser if you need to.

You should see something like this.

![date field in action](./images/Qy2gJq5gv8.gif)

## Create the Remaining Fields

Now create the rest of the fields using HTML elements. When you are done, the form should look similar to this.

![](./images/daily-journal-basic-layout.png)


## Column Layout with Flexbox

Use the `display: flex`, and `flex-direction: column` CSS properties to change your form to look like this.

![](./images/P5FPNsVInT.gif)


Update the `README.md` file to include your wireframe. `add`, `commit` and **`push` your project to Github.**

##
## UI/UX Challenge
** This is an optional challenge once you meet MVP.

### Best Practices for Form Design
Take a look at [Best Practices for Form Design](https://uxdesign.cc/best-practices-for-form-design-ff5de6ca8e5f) and refactor your Daily Journal to include best practices for form design.
