## Write a function that return hash of I love 100DaysOfNodeJs ( secret = 'seper-secret' ) Hash type = sha256


In `server.js` file write 

```
const crypto = require('crypto')

const secret = "super-secret";
function hash(string){
    return crypto.createHmac("sha256",secret).update(string).digest("hex");
}

console.log(hash("I Love 100DaysOfCode Bot"))

```

Now in terminal run `npm start`

See the Console response .

Example response 

`
3a8cce1a43b97989a12107be9014cad81a1b06ebbed6d08bc6f6a4f8b14de2d1
`

Boom !! You Completed Day 5 Challenge.