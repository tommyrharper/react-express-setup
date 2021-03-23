# React Express Setup

https://dev.to/lschwall/make-a-react-app-with-webpack-babel-and-express-30n8

```
echo 'node_modules' >> .gitignore
npm init //npm init -y will say yes to all questions
npm install --save express
mkdir Server
touch Server/index.js
```

- Add to `index.js`:
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

- Now install nodemon
```
nodemon -v
// IF NOT INSTALLED:
npm i -g  nodemon
```

- Now add to `package.json`:
```JSON
  "scripts": {
    "start": "nodemon server/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

- Now you can run your server:
```
npm run start
```
- Navigate to `localhost:3000`, you should see:
```
Hello World from the server!
```

## Webpack

```
npm install --save-dev webpack webpack cli
```

- Update `package.json`:
```JSON
  "scripts": {
    "start": "nodemon server/index.js",
    "build": "webpack --mode production",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

```
mkdir src
touch src/index.js
npm run build
```

## Babel

```
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
touch .babelrc
```

- Add to `.babelrc`:
```
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

```
touch webpack.config.js
```

- Add to `webpack.config.js`
```JavaScript
module.exports = {
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

## React

```
npm install --save react react-dom
touch ./src/index.html
```

- Add to `index.html`

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

- Add to `./src/index.js`:

```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';
const Index = () => {
    return <div>WELCOME TO REACT APP!</div>;
};
ReactDOM.render(<Index />, document.getElementById('app'));
```

```
npm install --save-dev html-webpack-plugin
```

- Update `webpack.config.js`:
```JavaScript
const HtmlWebPackPlugin = require('html-webpack-plugin');
const path = require('path');
const htmlPlugin = new HtmlWebPackPlugin({
  template: './src/index.html',
  filename: './index.html'
});
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, 'dist'),
    filename: "[name].js"
  },
  plugins: [htmlPlugin],
  module: {
    rules: [
      test: /\.(js|jsx)$/,
      exclude: /node_modules/,
      use: {
        loader: "babel-loader"
      }
    ]
  }
}
```

- Update `package.json`:
```JSON
"scripts": {
  "start": "node server/index.js",
  "dev": "webpack --mode development && node server/index.js",
  "build": "webpack --mode production",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

- Now refactor `server/index.js`:
```JavaScript
