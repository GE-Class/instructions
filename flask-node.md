# Communication between Express & Flask

## Express.js

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

## Flask

* Install Flask `pip install flask`
* Install Postgres library `pip install psycopg2` or `conda install psycopg2`
* Create a `main.py` file

```py
from flask import Flask, request, json, jsonify
app = Flask(__name__)

import sys
sys.path.append('.')
from user import User

@app.route("/users/<id>", methods=['GET'])
def money(id):
    rows = User.money(id)
    return jsonify(rows=rows)

if __name__ == "__main__":
    app.run(debug=True, host='0.0.0.0')
```

* Create `user.py`, will be used to talk to the Postgres database

```py
import psycopg2

class User:
    def money(id):
        conn = psycopg2.connect("dbname=ge_sales_dev user=postgres password=chyld host=127.0.0.1")
        cur = conn.cursor()
        cur.execute('SELECT * FROM "Sales" where user_id = ' + id + ';')
        data = cur.fetchall()
        cur.close()
        conn.close()
        return data
```
