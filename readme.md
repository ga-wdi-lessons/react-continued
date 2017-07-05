# React: Practice, Paradigms and Principles

## Learning Objectives

* Identify state in a React app
* Explain the properties and utility of components
* Distinguish container and presentational components
* Use jQuery to make AJAX calls in a React app
* Describe ways to add styles to a React app

## Framing (20 minutes / 0:20)

### [Components](https://facebook.github.io/react/docs/components-and-props.html)

Components let you split the UI into independent, reusable pieces, and think about each piece in isolation. Conceptually, components are like JavaScript functions. They accept arbitrary inputs (called "props") and return React elements describing what should appear on the screen.

In this class we'll look at building a React app that's more complex than the intro's blog example. When building an app like this, it's important to keep certain development practices and paradigms in mind so that we write maintainable code.

### [F.I.R.S.T. Components](https://addyosmani.com/first/)

A React component is built to expect an input and render a UI with it. More importantly, a well-structured component only receives data specific to its purpose. For example, our `Post` component from the blog example will only receive `title`, `author` and the like as inputs -- nothing else.

While this doesn't sound too groundbreaking, it is very different from the OOP principles we've gotten used to. This is because React follows a more **functional** approach to programming. For React components under this approach, **the same input will always produce the same output**.

You can build an app in a lot of ways, but if you want to look at some of the best practices, we can talk about what a component should be: **F.I.R.S.T.**

#### Focused

Components should do one thing and do it well. One thing that's hard to adjust to in React coming from an OOP background is packing too much information into a component.

> Think back to the Post component from the intro's class.

#### Independent

Components should increase cohesion and reduce coupling. Behavior in one component should not impact the behavior of another. In other words, components should not rely on one another.

> But they should compliment one another, just like our Comment component did for Post in the intro's class.

#### Reusable

Components should be written in a way that reduces the duplication of code.

> While the intro's Comment component was nested under a Post, we could have used it anywhere we wanted.

#### Small

Ideally, components should be short and condensed.

#### Testable

Because the same input will always produce the same output, components are easily unit testable.

> If you're interested, [Jest](https://facebook.github.io/jest/docs/tutorial-react.html) is a popular testing library for React.

## [State](https://facebook.github.io/react/docs/state-and-lifecycle.html) (10 minutes / 0:30)

So why do we follow all these principles? If not, it is easy to lose control of our application's state.

<details>
  <summary><strong>Q: What do we mean by a React component's "state"?</strong></summary>

  <br>

  > The properties of a component that change as the application runs. As opposed to .props, which are immutable.

</details>

<br>

So we've talked about `.state` at a more granular level. But now we're asking what it means for an application to have a singular "state" at a given point in time.

So what is this "state"? The organization and flow of data in an application at any point in time.

Let's think of states in terms of a game: Pokémon.

<details>
  <summary><strong>Q: What can you say about the player when a new game starts?</strong></summary>

  <br>

  > 0 Pokemon. We're stuck in Pallet Town (City #1). Professor Oak is around.

</details>

<br>

<details>
  <summary><strong>Q: What about when the game ends?</strong></summary>

  <br>

  > 150 Pokemon. 8 gym badges.

</details>

<br>

It's easy to think about this in terms of a game, because there is a clear idea of a beginning, end and states that reflect progress in between. You can attribute very specific data to all of these states.

<details>
  <summary><strong>Q: So we know an application can have different states. But how do we transition in between them?</strong></summary>

  <br>

  > Events.

</details>

<br>

You can think of your React application as a state machine. It receives user interaction as input and what we receive as output is a UI that reflects a brand new state.

Let's look at the process of a rendering a React Component...

![](./react-render.png)

## Break (10 minutes / 0:40)

## Exercise: React TVMaze

For this exercise, we are going to build a React app from scratch that will serve as a movie browser application, allowing users to enter a search term, and view results of tv shows via the OMDB api.

The desired outcome is for you to take a look at the solution and from there devise your own implementation. We have also included a step-by-step walkthrough of how to build out the demoed solution below.

Go ahead and clone [React TVMaze](https://github.com/ga-wdi-exercises/react-tvmaze/) now. This will be the code we start with.

### [Start with a Mock](https://facebook.github.io/react/docs/thinking-in-react.html#start-with-a-mock)

First step in creating a React app is to start with a mock and some sample data.

These are the two views for our app...

#### The Search Page

![search page](https://cloud.githubusercontent.com/assets/7882341/26462830/5af1a1ce-4150-11e7-9870-eb45ee12816a.png)

Here we've identified two components on the search page...
1. The top level component, which we'll call `Home`, is boxed in magenta.
2. The search input, a sub-component of `Home`, in yellow we'll call `Search`.

#### The Results Page

![results page](https://cloud.githubusercontent.com/assets/7882341/26462829/5aee3d7c-4150-11e7-89cd-5bcd4147f3bc.png)

Here we've identified three components on this page...
1. The same `Home` top level component.
2. A `results` components which contains results and an option to search again.
3. The individual results

#### Component Hierarchy

Given these breakdowns we have a component hierarchy that looks like...

- `Home`
  - `Search`
  - `Results`
    - `Result`

##### Sample Data

Here is some hard-coded data that we can use to begin building our application...

```js
const results = [
  {
    "name":"The Office",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/85/213184.jpg"
  },
  {
    "name":"Radiant Office",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/101/254702.jpg"
  },
  {
    "name":"The Office",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/93/234802.jpg"
  },
  {
    "name":"Mr. Box Office",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/97/244942.jpg"
  },
  {
    "name":"The Queen of Office",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/58/146476.jpg"
  },
  {
    "name":"No Offence",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/48/121682.jpg"
  },
  {
    "name":"Oficer",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/29/73047.jpg"
  },
  {
    "name":"Trzeci oficer",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/29/73053.jpg"
  },
  {
    "name":"Line Offline: Salaryman",
    "image":"http://static.tvmaze.com/uploads/images/medium_portrait/57/143508.jpg"
  },
  {
    "name":"Utenai Keikan","image":"http://static.tvmaze.com/uploads/images/medium_portrait/42/106093.jpg"
  }
]
```

### [Build a Static Version of the App](https://facebook.github.io/react/docs/thinking-in-react.html#step-2-build-a-static-version-in-react)

First we will build a static version of the app passing all of our data by `props`. This makes it much easier to avoid getting bogged down in tricky details of functionality while implementing the visual appearance of the UI.

1. [Home component](https://github.com/ga-wdi-exercises/react-tvmaze/commit/4446eb64dd7fb80dacf263b06f793ef092b8fe74)
2. [Search component](https://github.com/ga-wdi-exercises/react-tvmaze/commit/345ec65715d5840e43de9c526b32041568754d0f)
3. [Results component](https://github.com/ga-wdi-exercises/react-tvmaze/commit/8ab1c601e3b15c69ff5cfb7f958124ec68cef9db)

> Home should be passed two props for the static version of this app: `shows` and `hasSearched`.

## Break (10 minutes)

## Sync Up (20 minutes)

### [Identify the Minimal Representation of UI State](https://facebook.github.io/react/docs/thinking-in-react.html#step-3-identify-the-minimal-but-complete-representation-of-ui-state)

For our app to work we need...
- `movies` (movies to show)
- `query` (title being searched)
- `hasSearched` (boolean determining wether to show the search input or the results)

All of these are subject to change over time and so each must be kept in state.

### [Identify Where Your State Should Live](https://facebook.github.io/react/docs/thinking-in-react.html#step-4-identify-where-your-state-should-live)

Central to considering where state lives is the idea of **one way data flow**. The react documentation describes this step as "often the most challenging part for newcomers to understand".

Our task here is to look for the component for each aspect of state that could be the one place where that state is managed.

In our app, `query` is needed to keep track of what is going on in the search box, as well as to make the actual query.

This request will return the movies to the same component which managed the query so `movies` should be managed by the same component.

Finally, we have our `hasSearched` flag which we know to set when we make the request so these should all live in the same place.

Currently, the parent to the `Results` and `Search` components is `Home`.

We don't want to clutter our top level component as our app grows. This segues nicely into the idea of Container and Presentational Components.

#### [Container & Presentational Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

The above workflow has led to the popular component architecture of distinguishing container and presentational components.

Presentational components are components that render themselves based solely on the information that they receive from props. At this point, all of our components are presentational.

Container components are components whose job it is to exclusively manage state and as props any data needed by its presentational components.

This leads to a very nice division where state management and presentation are cleanly separated.

We are going to create a `SearchContainer` to manage `query`, `shows` and `hasSearched`.

### [Add Inverse Data Flow](https://facebook.github.io/react/docs/thinking-in-react.html#step-5-add-inverse-data-flow)

The last step is passing callbacks through props to presentational components to provide behavior.
We will need three functions defined on the `SearchContainer` component to provide necessary behavior to `Search` and `Results`...

1. `handleSearchInput` for managing changes to the input field
2. `onSubmitQuery` for kicking of the ajax request
3. `onSearchAgain` to set state back to render the search bar

> What is the point of all of these `.bind(this)` statements?

We are also going to add a `Utils.js` file where we ultimately will make the request to TVMaze.
For now we'll just hard code the mock data.

#### [SearchContainer component](https://github.com/ga-wdi-exercises/react-tvmaze/commit/1c896c5a975ea9d1f6fd07bbd655caf1d1f9f9ae)

### Replace Mock Data with an AJAX Request

Finally, we will replace the mock data with an actual AJAX request and update the `onSubmitQuery` to update state in handling the resolved promise.

#### [AJAX request](https://github.com/ga-wdi-exercises/react-tvmaze/commit/8bb4f4edd5a98261b2a89116e40ca20e9f025269)

### BONUS: Style in React

When it comes to adding styles to React, there is a bit of debate over what's the best practice. Facebook's official docs and recommendations are to write stylesheets that treat your CSS rule declarations as properties on one big Javascript object that can be passed into components via inline styles.

From the [Docs](https://facebook.github.io/react/tips/inline-styles.html)...

>  "In React, inline styles are not specified as a string. Instead they are specified with an object whose key is the camelCased version of the style name, and whose value is the style's value, usually a string"

However, this kind of rethinking the wheel feels like a step backwards for a lot of designers and developers who cringe at the notion of inline styles. For them, they choose to build React apps through a more traditional flow of adding ids and classes and then targeting elements via external stylesheets.

Also, via Webpack and other custom loaders, it is possible to use many third-party libraries or processors such as SASS, LESS, and Post-CSS.

Interesting to note, this problem has not been universally solved, and thus the debate will most likely continue to rage on until [somebody](https://medium.com/@jviereck/modularise-css-the-react-way-1e817b317b04#.61qgjgdu3) figures it out. Therefore, its often left to a team decision when choosing the best option for the application.

> Interested in learning more? Check out some excellent [blog posts](http://jamesknelson.com/why-you-shouldnt-style-with-javascript/) on the [subject](http://stackoverflow.com/questions/26882177/react-js-inline-style-best-practices) from the [front-end community](https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/)

### [Example of Object Literal Styles with React](https://github.com/ga-wdi-exercises/react-omdb/commit/830697fc68dcdccafcae9f73e711103de8d93fc9)

> **Reminder**: `class` is a protected keyword in React, in order to add a class attribute to an element use the keyword `className`

To add the finishing touches to our application, let's take a stab at styling our app with inline-styles and advance our markup with some help from Bootstrap...
- Load in Bootstrap CDN in `index.html`
- Modify UI to include Bootstrap classes
- Create a `styles` directory and make a file for your CSS rule definitions - this will be written in Javascript!
- Load in that file in any component and then use that to apply inline styling

## Closing (10 minutes / 2:30)

- What are some struggles you encountered when building out a more complex React app for the first time?
- What are some good rules of thumb to help keep components maintainable?

---

## Resources

* [Imperative vs. Declarative Javascript](http://www.tysoncadenhead.com/blog/the-state-of-javascript-a-shift-from-imperative-to-declarative#.VxgGxZMrKfQ)
* [Styling in React](http://survivejs.com/webpack_react/styling_react/)
* [ReactJS Fundamentals Course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)
