# React: Practice, Paradigms and Principles

---

## Learning Objectives

* Differentiate between Object-Oriented Programming and Functional Programming paradigms
* Explain how React incorporates principles of Functional Programming
* Identify state in a React app
* Define the role of Container components and when to use them
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

<details>
  <summary>In what way do we encapsulate our code in React?</summary>

  > Through components that define the structure, styling and behavior of a UI element. Furthermore, data flows independently through components.

</details>

A React component is built to expect an input and render a UI with it. More importantly, a (well-structured) component only receives data specific to its purpose. For example, our `Post` component from the blog example will only receive `title`, `author` and the like as inputs -- nothing else.

While this doesn't sound too groundbreaking, it is very different from the OOP principles we've gotten used to. This is because React follows a more **functional** approach to programming. For React components under this approach, **the same input will always produce the same output**.

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
  <summary><strong>Q: What do we mean by a React component's "state"?</strong></summary>

  > The properties of a component that change as the application runs. As opposed to .props, which are immutable.

</details>

So we've talked about `.state` at a more granular level. But now we're asking what it means for an application to have a singular "state" at a given point in time.

So what is this "state"? The organization and flow of data in an application at any point in time.

Let's think of states in terms of a game: Pokémon.

<details>
  <summary><strong>Q: What can you say about the player when a new game starts?</strong></summary>

  > 0 Pokemon. We're stuck in Pallet Town (City #1). Professor Oak is around.

</details>

<details>
  <summary><strong>Q: What about when the game ends?</strong></summary>

  > 150 Pokemon. 8 gym badges.

</details>

It's easy to think about this in terms of a game, because there is a clear idea of a beginning, end and states that reflect progress in between. You can attribute very specific data to all of these states.

<details>
  <summary><strong>Q: So we know an application can have different states. But how do we transition in between them?</strong></summary>

  > Events.

</details>

You can think of your React application as a state machine. It receives user interaction as input and what we receive as output is a UI that reflects a brand new state.

Let's look at the process of a rendering a React Component...
![](./react-render.png)


---

## Break (10 minutes / 0:50)

---

## Exercise: React OMDB

For this exercise, we are going to build a React app from scratch that will serve as a movie browser application, allowing users to enter a search term, and view results of movies via the OMDB api.

The desired outcome is for you to take a look at the solution and from there devise your own implementation. We have also included a a step-by-step walkthrough of how to build out the demoed solution below.

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

Now visit `http://localhost:3000` in the browser. You should see the final version of the OMDB React application.

Spend two minutes playing with the application. As you're doing that, make note of the following...

* How would you divide what you see into React components?
* What different states can you detect in the application?

---

#### Step 1: [Set up a `HelloWorld` Component](https://github.com/ga-wdi-exercises/react-omdb/commit/0024bef69f88dd9a5e086762a151b6063ecdf511) (5 minutes / 1:25)

To kick things off, let's add a `HelloWorld` component to make sure things are all wired together.

**Actions**:
- Fork and clone this [the exercise](https://github.com/ga-wdi-exercises/react-omdb/), then run `$ npm i` from the root project directory
- In your `/src` directory, configure your `App.js` and `index.js` files to render a `HelloWorld` component
- Run `npm start` and make sure everything is working

<details>
  <summary><strong>Q: What dependency do we need to load in whenever we want to create a component definition?</strong></summary>

  > React

</details>

<details>
  <summary><strong>Q: How do we go about starting to define a React component?</strong></summary>

  ```js
  class ComponentName extends Component {
    // Component definition goes in here...
  }
  ```

</details>

<details>
  <summary><strong>Q: What is the one method that every React component must have defined?</strong></summary>

  > render

</details>

<details>
  <summary><strong>Q: What is the syntax for rendering an application's root element?</strong></summary>

  ```js
  ReactDOM.render(
     <MyRootElement />, // some component
     document.getElementById("app") // some div
  )
  ```

</details>

---

#### Step 2: [Adds Home UI](https://github.com/ga-wdi-exercises/react-omdb/commit/13a6ae733e45a9ac8bfacc10978f531b68b653c6) (5 minutes / 1:30)

Great, now that we know React is working, let's refactor that HelloWorld component to serve as our app's Home component.

**Actions**
- Rename `App.js` to `Home.js` to better indicate the purpose of the file. Make sure to update references to this file elsewhere in your application accordingly.
- Create a Home component that returns a container `<div>` element, which should in turn contain a `<h1>` element.
- Render that component to the DOM.

> **NOTE:** The solution separates components into different files. Each of these files exports the component definition. This is a good way of organizing a React application, but not the only way. You are welcome to keep all component definitions in a single `index.js` file as well.

<details>
  <summary><strong>Q: Why do you think we have to use the `className` syntax when defining class attributes for our elements?</strong></summary>

  > `class` is a protected keyword in React/JSX.

</details>

<details>
  <summary><strong>Q: How would you summarize the Home component's responsibility?</strong></summary>

  > A: This will be our application's root element, the parent in which we will nest the rest of our child components. In charge of render what the user sees on initial page load.

</details>

---

#### Step 3: [Adds Search UI](https://github.com/ga-wdi-exercises/react-omdb/commit/1161c0c3eba93e036261c96288c75b1cf9ddf476) (20 minutes / 1:50)

> Here are some other commits demonstrating how we can complete this part in three steps...
>
> 3.1: [Add Static Search UI](https://github.com/ga-wdi-exercises/react-omdb/commit/4c5e83f0146e004cc0321242311bd7b727beaa3f)  
> 3.2: [Wire Up Form With Event Listener](https://github.com/ga-wdi-exercises/react-omdb/commit/7d446952e9ff5d7290caab4783b368d62f7b42b2)  
> 3.3: [Use State to Track Search Query](https://github.com/ga-wdi-exercises/react-omdb/commit/1161c0c3eba93e036261c96288c75b1cf9ddf476)  

Ok, we now have a proper header on the page and our Home component setup, but our movie browser app is lacking the ability to search for movies. Let's change that!

We are going to construct a `Search` component. That component will then be rendered later on as a child in the `Home` component.

**Actions**

First...
- Create a new file for your `Search` component.
- Define a `Search` component that renders a search form. This can be a simple form with a single input and submit button.
- Import the `Search` file to your `Home` file.
- Render the `Search` component in the `Home` component.

Then...
- Define your `Search` component's initial state. It should have a `query` value that corresponds to a search term.
- Define a function that is triggered whenever the user submits the Search form. Start by just logging `"clicked!"` to make sure it works.
  - Use an event listener to attach this function to your form. Try googling `onSubmit`.
- Define a function that updates your `query` value in state whenever a change is made to the input field. Try googling `onChange`.
- Update your submit function so that it now logs the `query` value in state.

> **HINT:** Start small. Just focus on getting the UI, then worry about wiring up the button so you are logging the search term.

<details>
  <summary><strong>Q: What method do we need to define in order for our component's state to be set when it is first rendered?</strong></summary>

  ```js
  constructor(props){
    super(props)
    this.state = {
      // Define state here...
    }
  }
  ```

</details>

<details>
  <summary><strong>Q: What value(s) should we include in our Search component's initial state?</strong></summary>

  > A value representing a user's search query.

</details>

<details>
  <summary><strong>Q: What is an example of explicit state mutation in React?</strong></summary>

  > `this.setState()`

</details>

<details>
  <summary><strong>Q: How might we use / what is the importance of `onSubmit`?</strong></summary>

  > They are examples of built in event handlers that we must supply a listener callback function to

</details>

<details>
  <summary><strong>Q: Why do we have to prevent the default behavior of our form submission event in our handler?</strong></summary>

  > In order to prevent the event firing a page refresh and thus losing our app's state

</details>

---

### Check-in / Break (15 minutes / 2:05)

---

### Container Components

When building in React, it's important to keep in mind some of the principles of what a component should be. According to React's developers, React components should be FIRST: focused, independent, reusable, small, and testable. In order to help keep components slim, a good practice is to move as much of the business logic surrounding a component's state to a container component.

If you're using React correctly, you're going to notice you have a lot of components that simply take in some data via props and output some UI - that is, components with just a render method. The reason for this is because a really great paradigm to get used to is separating your components into container components and presentational components, with presentational components optionally taking in some data and rendering a view.

---

#### Step 4: [Move Search Logic to a Container Component](https://github.com/ga-wdi-exercises/react-omdb/commit/8d4d671801909adfdf871c12dbfb6daff28d242c)

Let's look at our `Search` component, right now, even without worrying about querying the API or displaying the results, our component is starting to get a little heavy due to all our code relating to state. This is a good sign that we have an opportunity to refactor, and move the logic out of the "presenter" component, and into a "container component"

**Actions**

- Refactor your Search component so that it only renders a UI based on passed in data. You will refactor your state-related methods into a separate "container" component...
- Create a new file for and define your `SearchContainer` component
- This `SearchContainer` component should handle the business logic for your app's state (i.e., the methods removed from your initial Search component)
- Load the file containing the `Search` component in the `SearchContainer` file
- SearchContainer's `render` method should render the `Search` component. `SearchContainer`'s methods and query value (the search term) should be passed into Search via `.props`.

<details>
  <summary><strong>Q: What is our end goal in refactoring our Search components?</strong></summary>

  > To make Search a purely presenter component, who's only job is to take data from props and render a view.

</details>

<details>
  <summary><strong>Q: What is the importance of the props passed down to our Search component?</strong></summary>

  > We are passing down functions to handle user input and when a user submits a search, as well as the actual user query

</details>

---

#### Step 5: [Rendering Hard-Coded Results](https://github.com/ga-wdi-exercises/react-omdb/commit/da936065246dc91a5be826602b3550d05b0adffd)

Now that we have better organization and clarity in our code, let's work to get results to render after a user searches. In order to do this, we will need to keep track of the state of a user's search (i.e., have they clicked "search" yet or not?).

Continuing to build on the theme of small achievable wins, let's start by only worrying about rendering some hard-coded movies.

**Actions**
- In a new file, define a `Results` component that will take in a collection of movie objects and render each individual movie's title and poster - you can represent the latter with a URL string.
- Refactor your `SearchContainer` component to include state relating to whether or not a user has searched.
- In the `SearchContainer` file, load in the file containing your Results component.
- If a user has searched, instead of rendering the Search component, render a Results components for which the hard-coded movie data is passed in as `props`.
- As a final touch, make the Home header link to root so that we can easily navigate the app.

<details>
  <summary><strong>Q: What should the data type of the value that represents whether a user has searched or not be?</strong></summary>

  > A boolean. Think of this as an "on-off" switch.

</details>

<details>
  <summary><strong>Q: What Javascript tools can you use to dynamically render different UI's inside a component? In other words, how can I change what is rendered depending on whether the user has searched or not?</strong></summary>

  > By wrapping different return statements in a conditional block. If the user has searched, render this. If not, render that.

</details>

<details>
  <summary><strong>Q: Where does `.map` come from?</strong></summary>

  > It's a native method for collections in Javascript. It behaves exactly like the Ruby enumerable `.map`

</details>

<details>
  <summary><strong>Q: If you had to guess, what's the importance of supplying each individual result `item` with a `key` attribute?</strong></summary>

  > This allows React to keep track of each unique dynamically rendered child element. The key is treated as the unique identifier and is important in how React passes data to the child.

</details>

---

### BONUS: AJAX w/ React

Because React was developed originally to support view rendering, React does not come with support for `AJAX` calls out of the box. In order to make an ajax request, we need to install another library such as `jQuery` or load in another package / third-party dependency to execute `HTTP` requests.

> **NOTE**: an increasingly popular option via the npm world is a module called [axios](https://github.com/mzabriskie/axios) which can be used to make AJAX calls. It provides a similar interface and behavior to that of `ngResource` in Angular. We do *not* use this in the solution.

#### Step 6: [Connect to OMDB Api](https://github.com/ga-wdi-exercises/react-omdb/commit/70c28576d35e93331d37a425e45b73127f0713b3)

Now that we can render hard-coded results...

**Actions**
- Visit the [OMDB API documentation](http://omdbapi.com/) to determine how to properly use the API - note that we do not need a key
- We're going to be querying the API based on title to return a collection of results
- Load in jQuery and use it to make an AJAX call to the API endpoint using the search query
- Define a helper method to query the OMDB database. You can do this in a separate file called `Utils.js` or inside the SearchContainer. Remember to export / import your function if you define it in a separate file.
- In the SearchContainer component, use your OMDB helper method to query the API when the user submits a search
- Store the API call response to SearchContainer's state
- Pass the movie data to the Results component in place of the hard-coded data

> **NOTE:** Make sure to look through the whole API JSON response. You're going to have to parse through it and save only the data you need.

<details>
<summary><strong>Q: What parsing of user input to do we need to account for in order to make a valid search query?</strong></summary>

  > It's a good idea to replace any white space characters with a "+" to help format a proper url

</details>

<details>
  <summary><strong>Q: Why might it be a good idea to separate our code relating to API calls into a helpers file?</strong></summary>

  > It reduces the complexity of the components and we might want to reuse the functions we are defining in other components

</details>

<details>
  <summary><strong>Q: How might we handle bad response data such as no image found...?</strong></summary>

  > We can parse the initial response, check for bad inputs, and modify the data to set a valid default, then return the new results

</details>

---

### BONUS: Style in React

When it comes to adding styles to React, there is a bit of debate over what's the best practice. Facebook's official docs and recommendations are to write stylesheets that treat your CSS rule declarations as properties on one big Javascript object that can be passed into components via inline styles.

From the [Docs](https://facebook.github.io/react/tips/inline-styles.html)...

>  "In React, inline styles are not specified as a string. Instead they are specified with an object whose key is the camelCased version of the style name, and whose value is the style's value, usually a string"

However, this kind of rethinking the wheel feels like a step backwards for a lot of designers and developers who cringe at the notion of inline styles. For them, they choose to build React apps through a more traditional flow of adding ids and classes and then targeting elements via external stylesheets.

Also, via Webpack and other custom loaders, it is possible to use many third-party libraries or processors such as SASS, LESS, and Post-CSS.

Interesting to note, this problem has not been universally solved, and thus the debate will most likely continue to rage on until [somebody](https://medium.com/@jviereck/modularise-css-the-react-way-1e817b317b04#.61qgjgdu3) figures it out. Therefore, its often left to a team decision when choosing the best option for the application.

> Interested in learning more? Check out some excellent [blog posts](http://jamesknelson.com/why-you-shouldnt-style-with-javascript/) on the [subject](http://stackoverflow.com/questions/26882177/react-js-inline-style-best-practices) from the [front-end community](https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/)

---

### Step 7: [Add Styles with React](https://github.com/ga-wdi-exercises/react-omdb/commit/830697fc68dcdccafcae9f73e711103de8d93fc9)

> **Reminder**: `class` is a protected keyword in React, in order to add a class attribute to an element use the keyword `className`

To add the finishing touches to our application, let's take a stab at styling our app with inline-styles and advance our markup with some help from Bootstrap...

**Action**
- Load in Bootstrap CDN in `index.html`
- Modify UI to include Bootstrap classes
- Create a `styles` directory and make a file for your CSS rule definitions - this will be written in Javascript!
- Load in that file in any component and then use that to apply inline styling

<details>
  <summary><strong>What are some tradeoffs for using inline-styles to style React components?</strong></summary>
</details>

---

## Closing (10 minutes / 2:30)

- What are some struggles you encountered when building out a more complex React app for the first time?
- What are some good rules of thumb to help keep components maintainable?

---

## Resources

* [Imperative vs. Declarative Javascript](http://www.tysoncadenhead.com/blog/the-state-of-javascript-a-shift-from-imperative-to-declarative#.VxgGxZMrKfQ)
* [Styling in React](http://survivejs.com/webpack_react/styling_react/)
* [ReactJS Fundamentals Course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)
