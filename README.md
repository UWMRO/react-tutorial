# React Tutorial

This tutorial is designed to introduce you to [React](https://reactjs.org), a JavasScript library for building user web interfaces (web apps). You don't need to know anything about HTML, CSS, or JavaScript to follow it, but you'll need to learn a bit about those to continue working with React. The last section of the tutorial includes references for further reading.

## Prerequisites

You only need three things to run this tutorial: [NodeJS](https://nodejs.org/en/) (a JavaScript runtime engine), [npm](https://www.npmjs.com) (a package manager for JS), and [Git](https://git-scm.com).

Overall, we recommend that you follow [these instructions](https://github.com/UWMRO/Instruments/wiki) to set up your environment, but here's the TL;DR.

### Windows

If you are not installing WSL (not really needed for this example, but maybe recommended long-term) just download [NodeJS for Windows 64-bit](https://nodejs.org/en/download/) and [Git for Windows](https://gitforwindows.org) and install them normally. NodeJS for Windows includes `npm`. After that, open a `PowerShell` terminal as administrator and issue `npm` and `git`. If you get some lists of commands and no obvious errors, you should be good to go.

If you want to install WSL, follow [these instructions](https://learn.microsoft.com/en-us/windows/wsl/install) and install the Ubuntu distribution from the Microsoft Store. Once WSL is installed, open Ubuntu and follow [these instructions](https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl) to set up nvm, NodeJS, and npm. Do not install them using `sudo apt install`; that doesn't seem to work well. Ubuntu should come with Git installed so you don't need to do anything there.

### Linux

We'll assume you installed Ubuntu, but it should be easy to find the equivalent instructions for other distributions. Ubuntu comes with Git already installed, so you just need to install NodeJS and npm. Open a new terminal and write `sudo apt install -y nodejs npm`. After that completes, run `node` and `npm` to confirm they were installed correctly.

### macOS

macOS should include a reasonably recent version of Git. You can install NodeJS and npm from [here](https://nodejs.org/en/download/) (download the macOS Installer). After installing it, open a terminal and confirm that the `node` and `npm` commands work.

Alternatively, you can install [homebrew](https://brew.sh) and in a new terminal do `brew install node`.

## Cloning the tutorial

Open a new terminal (or PowerShell in administrator mode) and navigate to the location in your drive where you want to clone the tutorial repository. Then write

```console
git clone https://github.com/uwmro/react-tutorial
```

You will get a new directory `react-tutorial` with the contents of this repository. Since you won't be committing to it, you don't need to fork it (but feel free to!)

## Directory structure

The files in this example are a simplified version of a termplate generated with [Create React App](https://github.com/facebook/create-react-app). CRA is a boilerplate for creating React webapps easily.

The directory structure should look like:

```console
react-tutorial
├── README.md
├── node_modules
├── package.json
├── package-lock.json
├── .gitignore
├── public
│   ├── favicon.ico
│   └── index.html
└── src
    ├── App.css
    ├── App.js
    ├── index.js
    └── AUEG_Logo.png
```

Let's have a look at each one of those files:

- `README.md` is this very same text you're reading now!
- `node_modules` may not exist right now, but will appear once you run `npm install`. It contains the libraries needed to run this application (as defined in `package.json`).
- `package.json` defines lots of parameters for this JavaScript project. Among others it defines the name of the application, version, what scripts we can run, and the dependencies. You won't need to modify it for this tutorial, but it's an important piece of every JS project. [Here](https://docs.npmjs.com/cli/v9/configuring-npm/package-json) is some additional documentation.
- `package-lock.json` is a registry of the specific packages and their versions that are necessary to run this application. It's generated when `npm install` runs using the dependencies defined in `package.json`. It can be removed and will be regenerated next time `npm install` is run, but it's a good idea to commit it so that all developers working on the same application use the same installation.
- `.gitignore` is a list of files that will be ignored for `Git` purposes.
- `public` contains the HTML part of the application. For React apps that's usually very simple and here we only have two files: `index.html` is the barebones entry point for HTML, and `favicon.ico` is the small icon that will appear if you save the page. Note that `index.html` has a `<div>` element with `id='root'`. That will be the entry point where the JS code inserts the actual content.
- `src` is where all the JavaScript code must go, and where the real magic happens. The entry point is `index.js`, which just grabs the `root` div element and inserts the contents of `App.jsx`. `App.jsx` is a special kind of JavaScript called [JSX](https://reactjs.org/docs/introducing-jsx.html), which mixes JS and HTML. We'll talk about it a bit more later. `App.css` is a [Cascade Style Sheet](https://www.w3schools.com/css/) file that contains style descriptors that we'll use in `App.jsx`.

## Step 1: install and run the app

**Goal:** install and run the application.

In this step we'll just install and run the app without any modifications. For that, go to a terminal and navigate inside your `react-tutorial` directory. Then install the necessary dependencies with

```console
npm install
```

(this may take a minute or two and after it you should have a `node_modules` directory). Then run the app with

```console
npm start
```

This command compiles the JS code and runs a process that serves your application on a certain port (usually 3000). It also looks for changes in the source code and, if found, recompiles the code and updates your webapp automatically. After a minute or two you should see something like

```console
Compiled successfully!

You can now view react-tutorial in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.86.2:3000

Note that the development build is not optimized.
To create a production build, use npm run build.

webpack compiled successfully
```

(note that the `On Your Network` IP will be different). It should also automatically open a new window in your browser with the tutorial webapp. If that doesn't happen, try opening a new window yourself and navigate to `http://localhost:3000`. At that point you should see the AUEG logo rotating slowly. If you don't see that, repeat the process or ask for help.

## Step 2: add a new link

**Goal:** add a new static JSX component to the webapp.

First, open the project directory in your favourite editor and navigate to `App.jsx`. If you're familiar with JavaScript this file may look funny. It's a JS file, and contains a JS function, but it also has what looks like HTML code. This is actually a [JSX](https://reactjs.org/docs/introducing-jsx.html) file (thus the extension). In JSX JavaScript functions can return HTML tags and elements without treating them as strings. What's more, JSX HTML elements (called **components**) are actually JS functions, and their properties are actually function arguments. This makes JSX extremely powerful because HTML can now be handled in a programmatic way, and it's one of the strengths of React.

The `App` component returns all the HTML elements we see in our webapp. Among them there's a link to the React documentation (the `<a>` component). Let's add a new link to the MRO website. To do that add this code before the existing `<a>` component.

```html
<a
    className="App-link"
    href="https://sites.google.com/a/uw.edu/mro/"
    target="_blank"
    rel="noopener noreferrer"
>
    MRO website
</a>
```

Once you save the file, if you were running the app, you should see the change in your browser. If you weren't running the server, do `npm start`.

The component we added is a simple [<a> tag](https://www.w3schools.com/tags/tag_a.asp) with a few options: the `href` indicates where we want the link to point; `target="_blank" rel="noopener noreferrer"` opens it in a new window; and `className` tells it to use the `App-link` style class defined in `App.css`, which sets the colour.

If you've written HTML and CSS before, you'll be wondering why `className` and not `class`. The reason is that `class` is a reserved word in JS (remember we're actually writing JS!) and that could cause problems. Also, JSX generally uses cameCase syntax, so attributes like `border-color` become `borderColor`.

## Step 3: create an external component

**Goal:** create a component and use it in `<App>`.

So far we haven't taken too much advantage of the fact that JSX components are actual JS functions. Let's move one of the JSX components to its own function to highlight that fact.

In `App.jsx`, before `function App()` add the following code:

```jsx
function AUGELogo() {
  return <img src={logo} className="App-logo" alt="logo" />;
}
```

This is a JS function that returns an `<img>` component with the AUEG logo, and uses the `App-log` CSS style which makes it rotate nicely. Since this function returns an HTML component, the function is itself a JSX component and can be used like `<AUEGLogo />` (the `/>` is a shorthand for when a component doesn't have children).

Now let's replace the line `<img src={logo} className="App-logo" alt="logo" />` inside `function App()` with `<AUEGLogo />`. If you save the file the webapp should still show the rotating logo.

It may look as if we haven't done anything, but in reality we have made the AUEG `<img>` component a reusable element that we can use anywhere we want without having to repeat code. That reusability is one of the core tenets of JSX and React.

## Step 4: add a state

**Goal:** understand how React states work.

In this step we'll try to understand one of the most important concepts in React: [states](https://reactjs.org/docs/state-and-lifecycle.html).

Let's first get our example going and then we'll look into it. First, add this import at the top of `App.jsx`

```js
import React from 'react';
```

This will allow us to use some of the React functions and tools. Next, replace the `AUEGLogo` function with

```jsx
function AUGELogo() {
  const [direction, setDirection] = React.useState('normal');

  const handleClick = () => {
    if (direction === 'normal') {
      setDirection('reverse');
    } else {
      setDirection('normal');
    }
  };

  return (
    <div onClick={handleClick}>
      <img
        src={logo}
        className="App-logo"
        alt="logo"
        style={{ animationDirection: direction }}
      />
    </div>
  );
}
```

Now we save `App.jsx` and if you go to your browser and click on the rotating logo, that should change the direction of the spin. Every time you click, the direction will change.

Ok, now let's try to understand the code. First, we added this line

```js
const [direction, setDirection] = React.useState('normal');
```

[useState](https://reactjs.org/docs/hooks-state.html) defines a new state `direction` and gives it the initial value `'normal'`. It also returns a function that we can use to change that value, `setDirection`. These names are arbitrary by it's customary to call the setter function `setState`.

Why not to define a simple JS variable like `let direction = 'normal'`? One of the critical things that React does for us is to manage the lifecycle of our webapp. That means that it will re-render the application when something changes, and it does it smartly enough that it only re-renders those elements that have changed. But that comes at the cost of the developer not knowing when a component is going to be re-rendered. When that happens, normal JS variables are reset to their initial value. If we want to be sure a variable keeps its value after a re-render, we need to define it as a state and change its value with its setter function.

Next we added the line `style={{ animationDirection: direction }}` to the `<img>` component. `animationDirection` defines the direction in which the logo will spin, and we are tying that to the value of the `direction` state. If the `direction` state changes, React will re-render the component to match the new value.

We have also added a `<div onClick={handleClick}>` wrapping the `<img>` component. A `<div>` is just a container in HTML. To the `<div>` we added an *event listener* `onClick` pointing to the `handleClick` function. That event will be triggered when the user clicks on the image. There are many types of event, for things like pressing a key, making a change to a form, etc.

Let's have a look at the `handleClick` function that will be called when we click on the image:

```js
const handleClick = () => {
if (direction === 'normal') {
    setDirection('reverse');
} else {
    setDirection('normal');
}
};
```

This is an arrow function, and is another way in JS to define a function. This function in particular doesn't receive any arguments. When it runs, it checks the value of the `direction` state. If it's equal to `'normal'` it changes its value to `'reverse'` by calling the setter function. Otherwise it sets the value back to `'normal'`. In practice this function switches the value of `direction` between normal and reverse every time it's called, which translates in our logo changing its spinning direction.

### A note on hooks and functional components

If you've read the state documentation linked above you'll have seen that React components can also be defined as classes. Without going into details ([here](https://reactjs.org/docs/hooks-intro.html#motivation) is React's own motivation), it's usually preferred to define components as functions and use [hooks](https://reactjs.org/docs/hooks-intro.html) to handle states, effects, etc.

## Step 5: adding effects

**Goal:** learn about `useEffect` and add an effect when a page loads.

Along with states, the other most commonly used React feature are side effects. Effects are actions that happen when a page loads or when a state changes its value. They can be used to create logical cascade reactions to an event. Side effects can be created by using the [useEffect](https://reactjs.org/docs/hooks-effect.html) hook.

Let's change our `AUEGLogo` component to

```jsx
function AUGELogo() {
  const [animationState, setAnimationState] = React.useState('unset');

  React.useEffect(() => {
    setTimeout(() => {
      setAnimationState('App-logo-spin infinite 20s linear');
    }, 5000);
  }, []);

  return (
    <div>
      <img
        src={logo}
        className="App-logo"
        alt="logo"
        style={{ animation: animationState }}
      />
    </div>
  );
}
```

If you save the file and refresh the page, the logo should not move for 5 seconds, and the it should start spinning again.

We are setting the value of the `animation` property with `style={{ animation: animationState }}` and tying it to the value of the `animationState` state. The initial value of the state is `unset`, which disables the animation.

We also added an effect with

```js
React.useEffect(() => {
setTimeout(() => {
    setAnimationState('App-logo-spin infinite 20s linear');
}, 5000);
}, []);
```

which changes the value of `animationState` after 5 seconds. It does that by using the JS function [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout) which runs code after an interval.

Note that we added a `[]` at the end of the `useEffect` function. This tells the effect to only run once when the component is rendered for the first time, and not in subsequent re-renders. It's also possible to have an effect run when certain states changes, in which case the states would go inside the square brackets.

## Step 6: your own component

In this final step, you must modify the `AUEGLogo` component by adding a button to it. When that button is clicked the direction of the rotation should change (or you can add any kind of [animation](https://www.w3schools.com/css/css3_animations.asp) you want). Remember to do this by using states.

## Additional resources

For the next steps with React you'll need to learn a bit of JavaScript, HTML, and CSS. Here are a few resources to get you started. In general, look for tutorials for JavaScript ES6 or above: it's a much clearer language and you won't need to deal with legacy code that uses older versions of JS.

- A [good JavaScript tutorial](https://www.tutorialspoint.com/es6/index.htm). Here is [another one](https://www.w3schools.com/js/js_es6.asp).
- An [HTML tutorial](https://www.tutorialspoint.com/html/index.htm).
- A [CSS tutorial](https://www.w3schools.com/css/). CSS can be really intimidating, and you don't need to learn a lot about it for most projects. Just try to understand the basics and Google the rest.
- The [React documentation](https://reactjs.org/docs/hello-world.html). Pay special attention to the hooks section.
