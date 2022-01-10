## Create hello world web server without using any libraries



In `server.js` file write 

```
var http = require('http')
 http.createServer( (req,res) =>{
     
     res.write('Hello World');
     res.end()

 }).listen(3000);
```

Now in terminal run `npm start`

Our local server starts at port https://localhost:3000

Go to https://localhost:3000 and see the response .

Boom !! You Completed Day 3 Challenge.