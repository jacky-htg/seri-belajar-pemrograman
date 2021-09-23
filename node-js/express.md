# Express

Express JS adalah framework yang handal di nodejs. Pembuatan routing menjadi lebih mudah.

### Create Project

```text
npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (nodejs) backend
version: (1.0.0) 
description: backend untuk latihan
entry point: (index.js) index.js
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/rijal/jackyhtg/seri-belajar-pemrograman/nodejs/package.json:

{
  "name": "backend",
  "version": "1.0.0",
  "description": "backend untuk latihan",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
```

### Install Express

Kemudian lanjukan dengan menginstall expres js

```text
npm install express
```

### Basic Routing

```javascript
var express = require('./node_modules/express');

var app = module.exports = express();

app.use(express.json());

app.get('/', function (req, res) {
  res.send('Selamat Pagi!')
});

app.get('/users', function (req, res) {
  const users = [
    {name: "Jacky", age: 17},
    {name: "Jaya", age: 15},
    {name: "Baya", age: 12}
  ];
  res.json(users)
});

app.post('/users', function (req, res) {
  const user = {
    name: req.body.name,
    age: req.body.age
  };
  res.status(201).send(user);
});

app.put('/users/:id', function (req, res) {
  var id = req.params.id;
  const user = {
    id,
    name: req.body.name,
    age: req.body.age
  };
  res.json(user)
});

app.delete('/users/:id', function (req, res) {
  res.sendStatus(204);
});

app.listen(3000);
console.log('Express started on port 3000');
```

