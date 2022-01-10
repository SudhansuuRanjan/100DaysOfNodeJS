## Create a webserver that uses all available(multicore server) cores using cluster module. ( use loadtest library)

In `server.js` file write 

```
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
var y =  process.pid
  console.log("Master" + y +" is running");

  // Fork workers.
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    var x = worker.process.pid ;
    console.log("worker " + x + " died");
  });
} else {
    // Workers can share any TCP connection
    // In this case it is an HTTP server
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('hello world');
  }).listen(8000);
  // test the load of the server ->
  // loadtest -n 1000 -c 100 http://localhost:8000
  var z = process.pid ;
  console.log("Worker " + z + " started");
}
```

Now in terminal run `npm start`

See the Console response .

Example response 

```
Master16148 is running
Worker 11536 started
Worker 18312 started
Worker 3004 started
Worker 1936 started
Worker 7492 started
Worker 11712 started
Worker 17452 started
Worker 1192 started
```

Boom !! You Completed Day 6 Challenge.

[Back to Home](../README.md)