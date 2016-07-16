# trello-manager-node
This s a node version of trello manager while I already had a rails one. It talks to trello APIs and calculate points.


1. Create a repo on Github and clone to local
2. npm init
3. Create a new file called index.js
```
var express = require('express');
var app = express();

app.get('/', function(request, response) {
  response.send('Hello world');
})

app.listen(3000);
```
4. npm install --save express
5. node index.js
6. Add more info on the server start
```
var server = app.listen(3000, function() {
  console.log('Server running at http://localhost:' + server.address().port)
});
```
7. npm start command
go to package.json, update the following to scripts section
```
  "scripts": {
    "start": "node index.js"
  },
```
8. Watch changes update without restart server
```
$ npm install —save-dev nodemon
```
go to package.json, update the following to scripts section
```
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
```
