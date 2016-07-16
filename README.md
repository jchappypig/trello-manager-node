#### 1. Create a repo on Github and clone to local
#### 2. npm init
#### 3. Create a new file called index.js

```
var express = require('express');
var app = express();

app.get('/', function(request, response) {
  response.send('Hello world');
})

app.listen(3000);
```

#### 4. npm install --save express
#### 5. node index.js
#### 6. Add more info on the server start
```
var server = app.listen(3000, function() {
  console.log('Server running at http://localhost:' + server.address().port)
});
```
#### 7. npm start command
go to package.json, update the following to scripts section
```
  "scripts": {
    "start": "node index.js"
  },
```
#### 8. Watch changes update without restart server
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
#### 9. Load JSON file as data
```
var fs = require('fs');
var _ = require('lodash');
var users = [];

fs.readFile('users.json', {encoding: 'utf8'}, function(err, data) {
  if(err) throw err;

  JSON.parse(data).forEach(function(user) {
    user.name.full = _.startCase(user.name.first + ' ' + user.name.last);
    users.push(user);
  });
});

app.get('/', function(request, response) {
  response.send(JSON.stringify(users, null, 2));
});
```
#### 10. Show user data in a better format
```
app.get('/', function(request, response) {
  var buffer = ''

  users.forEach(function(user) {
    buffer += user.name.full + '<br/>'
  });
  response.send(buffer);
});
```
#### 11. Create link for each user
```
app.get('/', function(request, response) {
  var buffer = ''

  users.forEach(function(user) {
    buffer += '<a href=/' + user.username +'>' + user.name.full + '</a><br/>'
  });
  response.send(buffer);
});

app.get('/:username', function(request, response) {
  var username = request.params.username;
  response.send('Hi ' + username);
});
```
#### 12. Regular expression on routes
```
app.get(/big.*/, function(request, response, next) {
  console.log('Hi big guy!');
  next();
});
```
#### 13. Pug
```
$ npm install pug —save
```
setup pug engine in index.js
```
app.set('views', './views');
app.set('view engine', 'pug');

app.get('/', function(request, response) {
  response.render('index', {users: users});
});
```
add a new file index.pug under views folder
```
doctype html
html(lang="en")
  head
    title= "Users"
  body
    h1 users
    ul
      each user in users
        li
          a(href='/' + user.username)= user.username
```
