# Quick Start Guide


## Key commands

```
npm run start // start your server
```

## Quick Start

```
echo 'node_modules' >> .gitignore
npm init //npm init -y will say yes to all questions
npm install --save express
mkdir Server
touch Server/index.js
nodemon -v // check if nodemon is installed
npm i -g  nodemon // ONLY IF NOT ALREADY INSTALLED
npm install --save-dev webpack webpack cli
mkdir src
touch src/index.js
npm run build
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
touch .babelrc
touch webpack.config.js
npm install --save react react-dom
touch ./src/index.html
npm install --save-dev html-webpack-plugin
```

## Index.js

```JavaScript
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;
const mockResponse = {
  foo: 'bar',
  bar: 'foo'
};
app.get('/api', (req, res) => {
  res.send(mockResponse);
});
app.get('/', (req, res) => {
  res.status(200).send('Hello World from the server!');
});
app.listen(port, function () {
  console.log('App listening on port: ' + port);
});
```

## Package.json

```JSON
  "scripts": {
    "start": "node server/index.js",
    "dev": "webpack --mode development && node server/index.js",
    "build": "webpack --mode production",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

## .babelrc

```
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## webpack.config.js

```JavaScript
const HtmlWebPackPlugin = require("html-webpack-plugin");
const path = require('path');
const htmlPlugin = new HtmlWebPackPlugin({
  template: "./src/index.html",
  filename: "./index.html"
});
module.exports = {
  entry: "./src/index.html",
  output: {
    path: path.join(__dirname, 'dist'),
    filename: "[name].js"
  },
  plugins: [htmlPlugin],
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
}

```

## index.html

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React Example</title>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

## index.js

```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';
const Index = () => {
    return <div>WELCOME TO REACT APP!</div>;
};
ReactDOM.render(<Index />, document.getElementById('app'));
```