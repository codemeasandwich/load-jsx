# JSXTransformer
## A real-time transform for JSX ➜ JavaScript in ***NodeJs***

[![npm version](https://badge.fury.io/js/JSXTransformer.svg)](https://www.npmjs.com/package/JSXTransformer) [![npm downloads](https://img.shields.io/npm/dt/JSXTransformer.svg)](http://www.npmtrends.com/JSXTransformer) [![Known Vulnerabilities](https://snyk.io/test/npm/redux-auto/badge.svg)](https://snyk.io/test/npm/JSXTransformer)  [![Buy me a coffee](https://img.shields.io/badge/buy%20me-a%20coffee-orange.svg)](https://www.buymeacoffee.com/codemeasandwich)

---

### The Problem:
Setting up **webpack** and **babel** for a **node project** can be complicated, when maybe all you want is to **render some react elements**.

### **The Solution**:
JSXTransformer is a plug-n-play module that will dynamically parse all JSX imports. This will allow you to use JSX markup across your project without needing to worry about build or compile steps

---

## Features

- No configuration / bundle step needed
- plug-and-play with just ONE import
- Import files(.jsx, .js) using JSX markup within your NodeJs projects

## Bonus  

- Can insert `Import React from '{react}'` at the top of files that use JSX

---

# Install

`yarn add JSXTransformer`
**or**
`npm install --save JSXTransformer`



### constructor / setup

## ⚠ `JSXTransformer` Should be included before you import files with JSX markup in them.

The first step to import the lib
``` js
require('JSXTransformer')
```
If you want to have you React'ish libarty imported at the top of you JSX, use.
``` js
require('JSXTransformer')('preact')
```
this will add "import React from 'preact'" for example

##  You only need to `require('JSXTransformer')` once  on the first  JS file loaded ツ

---

# Example

### index.js
``` js
//Enable JSX
require("JSXTransformer")("react");

//Load server
require("./server");
```

### Elem.jsx
``` js
const Elem = () => (<>
        <div>Hi World</div>
        <button onClick={(e) => alert('Hello You!')}>Click!</button>
    </>)
export default Elem
```
### server.js

``` js
import ReactDOMServer from 'react-dom/server'
import express from 'express'
import Elem from './Elem.jsx'

const app = express()

app.get('/', (req, res) => {
    const jsx = ReactDOMServer.renderToString(<Elem />)

    res.send(`
        <!DOCTYPE html>
        <html> <body> ${jsx} </body> </html>
    `)
})

app.listen(3000, () => console.log(`App listening on http://localhost:3000}`))
```

