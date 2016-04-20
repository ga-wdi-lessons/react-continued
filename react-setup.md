# Initial Setup

In today's class we will be building a simple movie browser from scratch. By the end of the lesson, it will be able to search for a movie by title and get back search results returned from OMDB's api

> If you're interested, the solution and commit history for the blog can be found [here](https://github.com/ga-wdi-exercises/react-omdb/commits/solution).

Let's start by creating a directory for the app and initializing `npm`...

```bash
$ mkdir react-omdb && cd react-omdb && npm init -y
```

> `npm init -y` accepts all the defaults that, without the flag, you would have to hit the return key to accept.

Run the following command in the terminal...

```bash
$ npm install --save react react-dom && npm install --save-dev html-webpack-plugin webpack webpack-dev-server babel-{core,loader} babel-preset-react
```

You'll know installation went okay if your `package.json` file looks like something like this. You might have different versions...

```js
// package.json

"dependencies": {
  "react": "^15.0.1",
  "react-dom": "^15.0.1"
},
"devDependencies": {
  "babel-core": "^6.7.6",
  "babel-loader": "^6.2.4",
  "babel-preset-react": "^6.5.0",
  "html-webpack-plugin": "^2.15.0",
  "webpack": "^1.13.0",
  "webpack-dev-server": "^1.14.1"
}
```

Let's take a look at the dependencies we just installed...
* **React:** The library itself.
* **React-DOM:** An additional module that allows us to update the DOM using React components.
* **Webpack:** You learned about this "code bundler" in your [Build Tools lesson](https://github.com/ga-wdi-lessons/build-tools#webpack-10-mins).
* **Babel:** This one's actually new. We'll be using Babel to compile an HTML-like syntax called JSX into Javascript.

Great now that our packages have been installed, it's a good idea to create a `.gitignore` file and make sure that all the files in `node_modules` are not tracked into source-control:

```bash
$ touch .gitignore && echo "node_modules" >> .gitignore
```

Continuing to buildout the app skeleton...

```bash
$ mkdir app
$ touch app/index.html app/index.js
```

Inside our `index.html` file, let's add some boilerplate html...
​
```html
<!-- app/index.html -->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React OMDB</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

### Webpack
​
Now we need to setup up Webpack for our application so that we can bundle and serve our static assets.
​
In your terminal run...

```bash
$ touch webpack.config.js
```
​
In that file, go ahead a define an initial object to export...
​
```js
// webpack.config.js

module.exports = {
​
}
```

<details>
  <summary>What are 3 things we need to account for when defining our Webpack configuration?</summary>

  > (1) **`entry`**: The location of the app's root javascript file (specifying the app's point of entry).
  >  
  > (2) **`output`**: Where we want the bundled up output to go.
  >  
  > (3) **`loaders`**: The specific transformations to apply to our code.

</details>
​

```js
// webpack.config.js​

module.exports = {
  // What file to feed into webpack
  entry: [
    "./app/index.js"
  ],
  // Where we want our outputted files to go
  output: {
    path: __dirname + '/dist',
    filename: "index_bundle.js"
  },
  // What transformations we want to apply to our code
  module: {
    loaders: [
      {
        test: /\.js$/, // target any file ending in js
        exclude: /node_modules/, // except for node_modules
        loader: 'babel-loader' // apply the babel loader
      }
    ]
  }
}
```

​Next we need to setup Babel to specify which transformations should be run by the loader. In our app's root directory, we need to create a babel configuration file...
​
```bash
$ touch .babelrc
```
​
Inside `.babelrc`...
​
```js
// .babelrc

{
  "presets": [
    "react"
  ]
}
```

​Everything inside the `presets` array will be the specific transformations applied by Babel. For now, however, we are only adding the `react` preset, which will convert our JSX code into regular Javascript.  

Another thing we have to do is configure webpack to produce an `html` file that loads our bundled code. At the top of `webpack.config.js`, let's utilize `html-webpack-plugin`...
​
```js
// webpack.config.js

var HtmlWebpackPlugin = require('html-webpack-plugin');
var HtmlWebPackPluginConfig = new HtmlWebpackPlugin({
  template: __dirname + "/app/index.html",
  filename: "index.html",
  inject: 'body'
});
```

Now we can go ahead and add that as a plugin in our webpack config...
​
```js
// webpack.config.js

  // Add this code after `module: {...}`
  plugins: [
     HtmlWebPackPluginConfig
  ]
}
```

​We're using `html-webpack-plugin` to look into our `app/` directory and copy the contents of `index.html` there so that we can be sure to create another `index.html` in the `dist/` directory.

This new `index.html` be the file that is loading in our bundled code and the one we will be serving our app from. Webpack will automatically sync the files after every change.

> `dist/` is the directory that will store all of our "bundled" code.​

In order to actually run webpack, let's define a script in `package.json` to test our app's configuration...
​
```js
// package.json

"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1", // This should already be in there.
  "production": "webpack -p"
}
```

> There should already be a `scripts` object in `package.json`. Add this new key-value pair to that.

​Now from the command line, we can run a script that will launch Webpack and start the bundling...
​
```bash
$ npm run production
```

​If this command executes without any errors, it will create a new directory `dist`. In that directory, we will find...
* **`index_bundle.js`**: our app's minified Javascript code.
* **`index.html`**: a new index file that will link to `index_bundle.js`

Last but not least, we need to configure a command that will run our server, and rebuild our app after every change. That's were `Webpack Dev Server` will come in.

In `package.json`, let's define a new npm script that will run our server:

```js
// package.json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1", // This should already be in there.
  "production": "webpack -p",
  "start": "webpack-dev-server"
}
```

Now we can go to our command line and run:

```bash
$ npm start
```

This will boot up our server and build and serve our app on `localhost:8080`

> **Note**: make sure you do not have any other node servers running.
