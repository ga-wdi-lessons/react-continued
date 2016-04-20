# React: Practice, Paradigms and Principles

---

## Learning Objectives

- Differentiate between Object Oriented Programming and Functional Programming paradigms
- Explain how React incorporate principles of Functional Programming
- Identify state in a React app
- Define the role of Container components and when we would use them
- Utilize React's PropTypes to type check the values passed into our components
- Explain the ways to add styles to a React app
- Use jQuery to make AJAX calls in a React app

---

## Framing

In today's class you're going to get practice building a React app that's more complex than yesterday's simple blog example. When building an app like this, it's important to keep certain development practices and paradigms in mind so that we write maintainable code.

### F.I.R.S.T. Components

Building in React is a fundamental shift from how we have coded previously. Throughout this course, we've focused on an object-oriented paradigm.

**What does OOP mean?**  
**What benefits do we get from OOP?**

> Encapsulation (of a sort). An object is a wrapper for behavior and data.

**In what way do we encapsulate our code in React?**

> Through components that define the structure, styling and behavior of a UI element. Data exists independently of a component definition.

A React component is built to expect an input and render a UI with it. More importantly, a (well-structured) component only receives data specific to its purpose. For example, our `Post` component from the blog example will only receive `title`, `author` and the like as inputs -- nothing else.

While this doesn't sound too groundbreaking, it is very different from the OOP principles we've gotten used to. This is because React follows a more **functional** approach to programming. A component will never behave differently depending on what input is passed into it. In other words, in a React component, **the same input will always produce the same output**.

One thing that's hard to adjust to in React coming from an OOP background is packing too much information into a component.

You can build an app in a lot of ways, but if you want to look at some of the best practices, we can talk about what a component should be: **F.I.R.S.T.**

#### Focused

Components should do one thing and do it well.

#### Independent

Components should increase cohesion and reduce coupling. In other words, components should not rely on one another but they should compliment one another.

> What about nested components? Well, you could use the Comment we placed in Post yesterday in a completely different component.

#### Reusable

Components should be written in a way that reduces the duplication of code.

> See earlier example about Comments not being restricted to Posts.

#### Small

Ideally, components should be short and condensed.

#### Testable

Because the same input will always produce the same output, components are easily unit testable.

> If you're interested, [Ava](https://www.npmjs.com/package/ava) is a popular testing library for React.

## State

So why do we follow all these principles? If not, it is easy to lose control of our application's state. **What do we mean by state?**

We've talked about `.state` at a more granular level: the properties of a component that change as the application runs. But now we're asking what it means for an application to have a singular "state" at a given point in time.

So what is this "state"? The organization and flow of data in an application at any point in time.

Let's think of states in terms of a game: Pokémon.
* **Q:** What can you say about the player when a new game starts?

> 0 Pokemon. We're stuck in Pallet Town (City #1). Professor Oak is around.

What about when the game ends?

> 150 Pokemon. Maybe 151. 8 gym badges.

It's easy to think about this in terms of a game, because you can attribute very specific data to a particular state.

And how do you transition between states? **Events.**

You can think of your application as a global function. It receives user interaction as input and what we receive as output is a brand new state.

---

### Group Activity: Identify States while using Google

With the idea that state transitions are caused by events in mind...
* Visit Google's homepage.
* From there, interact with Google so that you arrive at different states.
* Keep a running list of these states.
* Think critically about whether a visual change corresponds to a state change or not.


---

## React OMDB

Intro to the solution

---

### Group Activity: Id OMDB app's states

Fork and clone repo and follow instructions in Step 0

---

### Initial Setup

---

### Walkthrough

---

#### Adds Hello World React

To kick things off, let's add a HelloWorld component to make sure things are all wired together.

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

<!-- TODO: Add Commit Diff  -->

---

#### Adds Home UI

Great, now that we know React is working, let's refactor that HelloWorld component to serve as our app's Home component.

<!-- TODO: Add Commit Diff  -->

**Q**. Why do you think we have to use the `className` syntax when defining class attributes for our elements?

> A: `class` is a protected keyword in React/JSX

**Q** How would you summarize the Home's component's responsibility?

> A: This will be our application's root element, the parent in which we will nest the rest of our child components. In charge of render what the user sees on initial page load

**Bonus**: Add a logo and initial layout

---

#### Adds Search UI

Ok, we now have a proper header on the page and our Home component setup, but our movie browser app is lacking the ability to search for movies...let's change that!

We are going to construct a Search component and render that later on as a child in the Home component.

**Q**. What method do we need to define in order for our component's state to be set when it is first rendered?

> A: `getInitialState()`

**Q**. What is an example of explicit state mutation in React?

> A: `this.setState()`

**Q**. What is the importance of `onChange` and `onSubmit`?

> A: they are examples of built in event handlers that we must supply a listener callback function to

**Q**. Why do we have to prevent the default behavior of our form submission event in our handler?

> A: In order to prevent the event firing a page refresh and thus losing our app's state

<!-- TODO: add Commit Diff -->

---

### Check-in / Break

---

### Container Components

When building in React, it's important to keep in mind some of the principles of what a component should be. According to the React's developers, React components should be FIRST: focused, independent, reusable, small, and testable. In order to help keep components slim, a good practice is to move as much of the business logic surrounding a component's state to a container component.

If you're using React correctly, you're going to notice you have a lot of components that simply take in some data via props and output some UI - that is, components with just a render method. The reason for this is because a really great paradigm to get used to is separating your components into container components and presentational components, with presentational components optionally taking in some data and rendering a view.

---

#### Adds Search Container

Let's look at our Search component, right now, even without worrying about querying the API or displaying the results, our component is starting to get a little heavy due to all our code relating to state. This is a good sign that we have an opportunity to refactor, and move the logic out of the "presenter" component, and into a "container component"

**Q**. What is our end goal in refactoring our Search component?s

> A: To make Search a purely presenter component, who's only job is to take data from props and render a view

**Q**. What is the importance of the props passed down to our Search component?

> A: We are passing down to function to handle user input and when a user submits a search, finally we are passing down the actual user query

<!-- TODO: add commit diff  -->

---

## Prop Types

If you've come to JavaScript from a strictly typed language you've most likely missed the assurance that types gives you. Some, however, feel like a strictly typed language is too demanding and prefer something a little more laid back. PropTypes in React are the middle ground in terms of type checking properties that are passed to your components.

PropTypes are great for finding bugs in our components but another useful feature is their ability to add documentation to a component. When we look at a well written component, we can look at the render method to figure out what it's going to look like and we can look at its propTypes to figure out what it needs to accept to render properly.

---

### Adds PropTypes to Search

With our latest refactoring, we now are using a container component to handle the logic relating to our app's search functionality, and we then pass the necessary data and functions down to our presenter component. Because of this shift, the values that we pass down via props become a lot more important and therefore we need a way to enforce that we are getting the values we expect, and that they are the right type.

Let's add some propType definitions to our Search component:


**Q**. What is adding PropTypes similar to the Rails world?

> A: Active Record validations

**Q** How can you assure that a certain prop is passed down?

> A: By adding the `.isRequired` property to our type definitions

**Q** What is another benefit we get as developers by adding PropTypes definitions to our components?

> A: It adds a layer of documentation to our code. We can look at a component, view its render method to see the UI it will output, and then look at the PropTypes to see the data values in needs to render

---

## AJAX w/ React

---

## Style in React

---

## Quiz Questions

---

## Resources

* [Imperative vs. Declarative Javascript](http://www.tysoncadenhead.com/blog/the-state-of-javascript-a-shift-from-imperative-to-declarative#.VxgGxZMrKfQ)
