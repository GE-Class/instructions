# Communication between Node & Flask

## Node.js

* Create a route in Express
* Load the `request` library
* Call the Flask API using `request`
* The response from Flask will be in `body`
* Send the Flask response back to the original caller with `res.send(body)`

```js
var request = require('request');
app.get('/users', function(req, res){
  request('http://url-to-your-flask-app/data/3', function(err, resp, body){
    res.send(body);
  });
});
```

