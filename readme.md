# React: Practice, Paradigms and Principles

---

## Learning Objectives

* Differentiate between Object-Oriented Programming and Functional Programming paradigms
* Explain how React incorporates principles of Functional Programming
* Identify state in a React app
* Define the role of Container components and when to use them
* Utilize React's PropTypes to validate data passed into our components
* Use jQuery to make AJAX calls in a React app
* Explain the ways to add styles to a React app

---

## Framing (20 minutes / 0:20)

In today's class you're going to get practice building a React app that's more complex than yesterday's simple blog example. When building an app like this, it's important to keep certain development practices and paradigms in mind so that we write maintainable code.

### F.I.R.S.T. Components

Building in React is a fundamental shift from how we have developed previously. Throughout this course, we've focused on an object-oriented paradigm.

<details>
  <summary>What does it mean to follow an OOP paradigm? What are the benefits/pitfalls of using OOP?</summary>

  > Encapsulation (of a sort). An object is a wrapper for behavior and data. It's a logical, helpful way to organize data. But it can be hard to maintain when dealing with a large number of objects.

</details>
<br/>

<details>
  <summary>In what way do we encapsulate our code in React?</summary>

  > Through components that define the structure, styling and behavior of a UI element. Furthermore, data flows independently through components.

</details>
<br/>

A React component is built to expect an input and render a UI with it. More importantly, a (well-structured) component only receives data specific to its purpose. For example, our `Post` component from the blog example will only receive `title`, `author` and the like as inputs -- nothing else.

While this doesn't sound too groundbreaking, it is very different from the OOP principles we've gotten used to. This is because React follows a more **functional** approach to programming. A component will never behave differently depending on what input is passed into it. In other words, in a React component, **the same input will always produce the same output**.

You can build an app in a lot of ways, but if you want to look at some of the best practices, we can talk about what a component should be: **F.I.R.S.T.**

#### Focused

Components should do one thing and do it well. One thing that's hard to adjust to in React coming from an OOP background is packing too much information into a component.

> Think back to the Post component from yesterday's class.

#### Independent

Components should increase cohesion and reduce coupling. Behavior in one component should not impact the behavior of another. In other words, components should not rely on one another.

> But they should compliment one another, just like our Comment component did for Post in yesterday's class.

#### Reusable

Components should be written in a way that reduces the duplication of code.

> We could have nested yesterday's Comment in a component other than Post.

#### Small

Ideally, components should be short and condensed.

#### Testable

Because the same input will always produce the same output, components are easily unit testable.

> If you're interested, [Ava](https://www.npmjs.com/package/ava) is a popular testing library for React.

## State (10 minutes / 0:30)

So why do we follow all these principles? If not, it is easy to lose control of our application's state.

<details>
  <summary>What do you we mean by a React component's "state", in the context of yesterday's class?</summary>

  > The properties of a component that change as the application runs. As opposed to .props, which are immutable.

</details>
<br/>

So we've talked about `.state` at a more granular level. But now we're asking what it means for an application to have a singular "state" at a given point in time.

So what is this "state"? The organization and flow of data in an application at any point in time.

Let's think of states in terms of a game: Pokémon.
* **Q:** What can you say about the player when a new game starts?

> 0 Pokemon. We're stuck in Pallet Town (City #1). Professor Oak is around.

What about when the game ends?

> 150 Pokemon. 8 gym badges.

It's easy to think about this in terms of a game, because there is a clear idea of a beginning, end and states that reflect progress in between. You can attribute very specific data to all of these states.

<details>
  <summary>So we know an application can have different states. But how do we transition in between them?</summary>

  > Events.

</details>
<br/>

You can think of your React application as a state machine. It receives user interaction as input and what we receive as output is a UI that reflects a brand new state.

---

### Group Activity: Identify States while using Google (10 minutes / 0:40)

> 5 minutes exercise. 5 minutes review.

With the idea that state transitions are caused by events in mind...
* Visit Google's homepage.
* From there, interact with Google so that you arrive at different states.
* Keep a running list of these states.
* Think critically about whether a visual change corresponds to a state change or not.


---

## Break (10 minutes / 0:50)

---

## Exercise: React OMDB

For this exercise, we are going to be building a React app from scratch that serve as a movie browser application, allowing users to enter a search term, and view results of movies via the OMDB api.

Please note, the desired outcome is for you to take a look at the solution and from there devise your own implementation. However, if follow along belong below for a step by step walkthrough of how to build out the demoed solution.

---

### You Do: Map Out React OMDB (10 minutes / 1:00)

> 5 minutes set-up and exercise. 5 minutes review.

Fork and clone the React OMDB repo.

```bash
git clone git@github.com:ga-wdi-exercises/react-omdb.git
cd react-omdb
git checkout solution
npm install
npm start
```

Now visit `http://localhost:8080` in the browser. You should see the final version of the  OMDB React application.

Spend two minutes playing with the application. As you're doing that, make note of the following...
* How would you divide what you see into React components?
* What different states can you detect in the application?

---

### Initial Setup (10 minutes / 1:20)

#### [See walkthrough here](./react-setup.md)

---

#### Step 1: [Set up a `HelloWorld` Component](https://github.com/ga-wdi-exercises/react-omdb/commit/f1f4c044ea56754b2b43cc5699a260f221178171) (5 minutes / 1:25)

To kick things off, let's add a HelloWorld component to make sure things are all wired together.

**Actions**:
- `npm install` the dependencies you'll need
- Create and configure your `.babelrc` file
- Create and configure your `webpack.config.js`file
- In your app directory create and configure your `index.html` file
- In your app directory create and configure your `index.js` file to render a HelloWorld component
- Start Webpack and make sure everything is working

**Q**. What dependency do we need to load in whenever we want to create a component definition?

> A: React

**Q**. What method do we call on our `React` instance to define a component?

> A: `.createClass()`

**Q**. What is the one method that every React component must have defined?

> A: render

**Q**. What is the syntax for rendering an application's root element?

```js
ReactDOM.render(
   <MyRootElement />, // some component
   document.getElementById("app") // some div
 )
```

---

#### Step 2: [Adds Home UI](https://github.com/ga-wdi-exercises/react-omdb/commit/17002daa0c2834079c7ef0a29b54e01524004e8a) (5 minutes / 1:30)

Great, now that we know React is working, let's refactor that HelloWorld component to serve as our app's Home component.

**Actions**
- Create a Home component that outputs an `<h1>` and a container `<div>` element
- Render that component to the DOM

> **NOTE:** The solution separates components into different files. Each of these files `module.exports` the component definition. This is a good way or organizing a React application, but not the only way. You are welcome to keep all component definitions in a single `index.js` file as well.

**Q**. Why do you think we have to use the `className` syntax when defining class attributes for our elements?

> A: `class` is a protected keyword in React/JSX

**Q** How would you summarize the Home's component's responsibility?

> A: This will be our application's root element, the parent in which we will nest the rest of our child components. In charge of render what the user sees on initial page load

**Bonus**: Add a logo and initial layout

---

#### Step 3: [Adds Search UI](https://github.com/ga-wdi-exercises/react-omdb/commit/c0391fe057d1fe8ba76bdf4e137a2a7b255a4837) (20 minutes / 1:50)

Ok, we now have a proper header on the page and our Home component setup, but our movie browser app is lacking the ability to search for movies...let's change that!

We are going to construct a Search component and render that later on as a child in the Home component.

**Actions**

First...
- Create a new file for your Search component
- Define a Search component that renders a search form
- Load (or `require`) the Search file in the Home file
- Render the Search component in the Home component

Then...
- Define your Search component's initial state
- Define a function that will update the Search component's state with the search query when the user submits the form
- Use an event listener to attach this function to your form
- Wire up your form's button to log whatever is in the input field when the button is clicked

> **HINT:** Start small - just focus on getting the UI, then worry about wiring up the button so you are logging the search term

**Bonus**
- Utilize `onChange` in your search element to set the state on every change equal to the value of the input


**Q**. What method do we need to define in order for our component's state to be set when it is first rendered?

> A: `getInitialState()`

**Q**. What value(s) should we include in our Search component's initial state?

> A: Search query.

**Q**. What is an example of explicit state mutation in React?

> A: `this.setState()`

**Q**. How might we use / what is the importance of `onSubmit`?

> A: they are examples of built in event handlers that we must supply a listener callback function to

**Q**. Why do we have to prevent the default behavior of our form submission event in our handler?

> A: In order to prevent the event firing a page refresh and thus losing our app's state

---

### Check-in / Break (15 minutes / 2:05)

---

### Container Components

When building in React, it's important to keep in mind some of the principles of what a component should be. According to React's developers, React components should be FIRST: focused, independent, reusable, small, and testable. In order to help keep components slim, a good practice is to move as much of the business logic surrounding a component's state to a container component.

If you're using React correctly, you're going to notice you have a lot of components that simply take in some data via props and output some UI - that is, components with just a render method. The reason for this is because a really great paradigm to get used to is separating your components into container components and presentational components, with presentational components optionally taking in some data and rendering a view.

---

#### Step 5: [Move Search logic to a Container component](https://github.com/ga-wdi-exercises/react-omdb/commit/fd5e170ca89424aac2501865d8de7e4ced9a0b7d)

Let's look at our Search component, right now, even without worrying about querying the API or displaying the results, our component is starting to get a little heavy due to all our code relating to state. This is a good sign that we have an opportunity to refactor, and move the logic out of the "presenter" component, and into a "container component"

**Actions**

- Refactor your Search component so that it only renders a UI based on passed in data. You will refactor your state-related methods into a separate "container" component...
- Create a new file for and define your SearchContainer component
- This SearchContainer component should handle the business logic for your app's state (i.e., the methods removed from your initial Search component)
- Load the file containing the Search component in the SearchContainer file
- SearchContainer's `render` method should only render a Search component. SearchContainer's methods and query value (the search term) should be passed into Search via `.props`. [Reference this diff if you need help](https://github.com/ga-wdi-exercises/react-omdb/commit/fd5e170ca89424aac2501865d8de7e4ced9a0b7d)

**Q**. What is our end goal in refactoring our Search components

> A: To make Search a purely presenter component, who's only job is to take data from props and render a view

**Q**. What is the importance of the props passed down to our Search component?

> A: We are passing down functions to handle user input and when a user submits a search, as well as the actual user query

---

### Prop Types

If you've come to JavaScript from a strictly typed language you've most likely missed the assurance that types gives you. Some, however, feel like a strictly typed language is too demanding and prefer something a little more laid back. PropTypes in React are the middle ground in terms of type-checking properties that are passed to your components.

PropTypes are great for finding bugs in our components but another useful feature is their ability to add documentation to a component. When we look at a well written component, we can look at the render method to figure out what it's going to look like and we can look at its PropTypes to figure out what it needs to accept to render properly.

---

#### Step 6: [Adds PropTypes to Search](https://github.com/ga-wdi-exercises/react-omdb/commit/adb1cafc3761d59582ae7e2e9f898fbf0378caf7)

With our latest refactoring, we now are using a container component to handle the logic relating to our app's search functionality, and we then pass the necessary data and functions down to our presenter component. Because of this shift, the values that we pass down via props become a lot more important and therefore we need a way to enforce that we are getting the values we expect, and that they are the right type.

Let's add some PropTypes definitions to our Search component:

**Actions**
- Define a variable called `PropTypes` equal to `React.PropTypes` right after you load in React
- Set a property on your Search component equal to an object. Each of its keys will be the name of one of your component's `.props`The corresponding values will be the `PropTypes` declarations.

> **NOTE:** Refer to the [docs](https://facebook.github.io/react/docs/reusable-components.html#prop-validation) for PropTypes syntax.
>
> **HINT:** PropTypes syntax can get a little weird. Functions are referred to as `func`, while booleans are `bool`.

**Q**. What is adding PropTypes similar to the Rails world?  

> A: Active Record validations

**Q** How can you assure that a certain prop is passed down?

> A: By adding the `.isRequired` property to our type definitions

**Q** What is another benefit we get as developers by adding PropTypes definitions to our components?

> A: It adds a layer of documentation to our code. We can look at a component, view its render method to see the UI it will output, and then look at the PropTypes to see the data values in needs to render

---

#### Step 7: [Rendering Hard-Coded Results](https://github.com/ga-wdi-exercises/react-omdb/commit/11efb9ffc6efc3d221151ab997d591f5805b663a)

Great now that we have better organization and security in our code, let's work to get results to render after a user searches. In order to do this, we will need to keep track of the state of a user's search (i.e., have they clicked "search" yet or not?).

Continuing to build on the theme of small achievable wins, let's start by only worrying about rendering some hard-coded movies.

**Actions**
- In a new file, define a results component that will take in a collection of movie objects and render each individual movie's title and poster - you can represent the latter with a URL string
- Refactor your SearchContainer component to include state relating to whether or not a user has searched
- In the SearchContainer file, load in the file containing your Results component
- If a user has searched, instead of rendering the Search component, render a Results components for which the hard-coded movie data is passed in as `props`
- Make the Home header link to root

**Q.** What should the data type of the value that represents whether a user has searched or not be?

> A: A boolean. Think of this as an "on-off" switch.

**Q.** What Javascript tools can you use to dynamically render different UI's from a component. In other words, how can I change what is rendered depending on whether the user has searched or not.

> A: By wrapping different return statements in a conditional block. If the user has searched, render this. If not, render that.

**Q**. Where does `.map` come from?

> A: it's a native method for collections in Javascript. It behaves exactly like the Ruby enumerable `.map`

**Q**. If you had to guess, what's the importance of supplying each individual result `item` with a `key` attribute?

> A: This allows React to keep track of each unique dynamically render child element. The key is treated as the unique identifier and is important in how React  passes data to the child.

---

### AJAX w/ React

Because React was developed originally to support view rendering, React does not come with support for `AJAX` calls out of the box. In order to make an ajax request, we need to install another library such as `jQuery` or load in another package / third-party dependency to execute `HTTP` requests.

> **NOTE**: an increasingly popular option via the npm world is a module called [axios](https://github.com/mzabriskie/axios) which can be used to make AJAX calls. It provides a similar interface and behavior to that of `ngResource` in Angular. We do not use this in the solution.

#### Step 8: [Connect to OMDB Api](https://github.com/ga-wdi-exercises/react-omdb/commit/2e3178e796567a4639369ed4962f70242dd7cc0e)

Now that we can render hard-coded results...

**Actions**
- Visit the [OMDB API documentation](http://omdbapi.com/) to determine how to properly use the API - note that we do not need a key
- We're going to be querying the API based on title to return a collection of results
- Load in jQuery and use it to make an AJAX call to the API endpoint using the search query
- Create an `omdbHelpers` file that will `module.exports` the function definition used to make the API calls to OMDB
- In the SearchContainer component, use your OMDB helper method to query the API when the user submits a search
- Store the API call response to SearchContainer's state
- Pass the movie data to the Results component in place of the hard-coded data

> **NOTE:** Make sure to look through the whole API JSON response. You're going to have to parse through it and save only the data you need.

**Q**. What parsing of user input to do we need to account for in order to make a valid search query?

> A: It's a good idea to replace any white space characters with a "+" to help format a proper url

**Q**. Why might it be a good idea to separate our code relating to API calls into a helpers file?

> A: It reduces the complexity of the components and we might want to reuse the functions we are defining in other components

**Q**. How might we handle bad response data such as no image found...?

> A: We can parse the initial response, check for bad inputs, and modify the data  to set a valid default, the return the new results

---

### Style in React

When it comes to adding styles to React, there is a bit of debate over what's the best practice. Facebook's official docs and recommendations are to write stylesheets that treat your CSS rule declarations as properties on one big Javascript object that can be passed into components via inline styles.

From the [Docs](https://facebook.github.io/react/tips/inline-styles.html)...

>  "In React, inline styles are not specified as a string. Instead they are specified with an object whose key is the camelCased version of the style name, and whose value is the style's value, usually a string"

However, this kind of rethinking the wheel feels like a step backwards for a lot of designers and developers who cringe at the notion of inline styles. For them, they choose to build React apps through a more traditional flow of adding ids and classes and then targeting elements via external stylesheets.

Also, via Webpack and other custom loaders, it is possible to use many third-party libraries or processors such as SASS, LESS, and Post-CSS.

Interesting to note, this problem has not been universally solved, and thus the debate will most likely continue to rage on until [somebody](https://medium.com/@jviereck/modularise-css-the-react-way-1e817b317b04#.61qgjgdu3) figures it out. Therefore, its often left to a team decision when choosing the best option for the application.

> Interested in learning more? Check out some excellent [blog posts](http://jamesknelson.com/why-you-shouldnt-style-with-javascript/) on the [subject](http://stackoverflow.com/questions/26882177/react-js-inline-style-best-practices) from the [front-end community](https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/)

---

## Bonus

---

### Step 9: [Add Styles with React](https://github.com/ga-wdi-exercises/react-omdb/commit/b8e07c0fa4310d5a2bf66f7a5d2592037d4ebfe1)

To add the finishing touches to our application, let's take a stab at styling our app with inline-styles and advance our markup with some help from Bootstrap...

**Action**
- Install `css-loader` and `style-loader` loaders with npm
- Define a new loader in your webpack configuration that targets any css files and applies the css and style loader transformations
- Load in Bootstrap CDN in `app/index.html`
- Modify UI to include Bootstrap classes
- Create a `styles` directory and make a file for your CSS rule definitions - this will be written in Javascript!
- Load in that file in any component and then use that to apply inline styling

**Q**. What are some tradeoffs for using inline-styles to style React components?

## Closing (10 minutes / 2:30)

- What are some struggles you encountered when building out a more complex React app for the first time?
- What are some good rules of thumb to help keep components maintainable?

---

## Resources

* [Imperative vs. Declarative Javascript](http://www.tysoncadenhead.com/blog/the-state-of-javascript-a-shift-from-imperative-to-declarative#.VxgGxZMrKfQ)
* [Styling in React](http://survivejs.com/webpack_react/styling_react/)
* [ReactJS Fundamentals Course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)
