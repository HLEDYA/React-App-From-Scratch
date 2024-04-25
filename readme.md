# Creating a react app without using create-react-app

## Initilization

### Create the directory of your app
```
mkdir my-react-app
cd my-react-app
```

### Create a nodejs app with npm init
```
npm init
```



## Installation

### Install React dependencies
```
npm i react react-dom
```

### Install webpack for bundling 
webpack-dev-server will be used as development server with hot reloading capability.
```
npm i webpack webpack-dev-server webpack-cli --save-dev
```

### Install babel for JS transpiling
```
$ npm i babel-core babel-loader @babel/preset-react @babel/preset-env html-webpack-plugin --save-dev
```

## Configuring

### Configure webpack
Create webpack.config.js in the root of your app's directory

```JS
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  //This property defines where the application starts
  entry:'./src/index.js',
    
  //This property defines the file path and the file name which will be used for deploying the bundled file
  output:{
    path: path.join(__dirname, '/dist'),
    filename: 'bundle.js'
  },
    
  //Setup loaders
  module: {
    rules: [
      {
        test: /\.js$/, 
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      }
    ]
  },
    
  // Setup plugin to use a HTML file for serving bundled js files
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    })
  ]
}
```

### Configure babel
Create .babelrc
```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## Coding
### index.js
```js
import React from "react"
import ReactDOM from "react-dom"
import App from "./components/App"

ReactDOM.render(<App />, document.getElementById("app"));
```
### index.html
```html
<html>
  <head>
    <script src="index.js" type="javascript"></script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```
### App.js
create components/App.js
```js
import React from 'react'

function App() {
  return (
    <div>App</div>
  )
}

export default App
```
