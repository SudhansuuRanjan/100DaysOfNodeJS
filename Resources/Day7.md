##  Write a function that hash a password using bycryptjs and write another function that compare the hashed password and return boolean.


In `server.js` file write 

```
var bcrypt = require('bcryptjs');
const salt = 10 ;
const rawPassword = "May The Force Be With You"

function hashPass(password) {
  // Everytime hashed password will different. but when you will compare it using bcrypt.compare() method it gonna compare correctly :/.
  return bcrypt.hashSync(password, salt);
}

function verifyPass(password, hash) {
  return bcrypt.compareSync(password, hash);
}

// hashing...
const hash = hashPass(rawPassword);

const enteredPassword = "May The Force Be With You"
// verifying...
const isPasswordCorrect = verifyPass(enteredPassword, hash);

// Logs
console.log(hash);
console.log(isPasswordCorrect);

```

Now in terminal run `npm start`

See the Console response .

Example response 

`$2a$10$SyjCbrO4uoRJoYMC5N.VwerNXnQy6DYY3KpD986VmzzWx0jYjmGgG`

`true`

Boom !! You Completed Day 7 Challenge.