---
path: "/authentication-and-testing"
title: "Authentication & Testing"
date: "2019-12-15"
tags: ['Authentication', 'Testing', 'JWT', 'Sessions', 'Cookies', 'lambda school']
excerpt: "Authentication is the process by which our Web API..."
---

# Authentication & Testing

## Notes

### Authentication

**Authentication** is the process by which our Web API indentifies the identity
of a client that is trying to access a resource.  If Web API has authentication, 
it means that clients can:
- Register accounts
- Login to prove identity
- Logout of the system to invalidate access until they login again
- Reset their passwords

**Authorization** comes *after* authentication, and handles what type of access a
user should have.

When storing a user's password into a database, we must ensure that they are not
saved as plain text.

We can use [bcryptjs](https://www.npmjs.com/package/bcryptjs) to save our passwords in a secure manner.

Bcryptjs features include:
- Password hashing function
- Manual and automatic salting (A salt is a random string that's used as
    additional input in the hashing function)
- Accumulative hashing rounds

Having an algorithm that hashes the information multiple times means an attacker
needs to have the hash, know the algorithm used, and how many rounds were used
to generate the hash in the first place.

Example of bcryptjs usage from Lambda School's TK:
```javascript
server.post('/api/login', (req, res) => {
  let { username, password } = req.body;

  Users.findBy({ username })
    .first()
    .then(user => {
      // check that passwords match
      if (user && bcrypt.compareSync(password, user.password)) {
        res.status(200).json({ message: `Welcome ${user.username}!` });
      } else {
        // we will return 401 if the password or username are invalid
        // we don't want to let attackers know when they have a good username
        res.status(401).json({ message: 'Invalid Credentials' });
      }
    })
    .catch(error => {
      res.status(500).json(error);
    });
}); 
```

### Sessions & Cookies

The HTTP protocol is stateless.  It has no memory across requests.  By default,
whenever we change pages all previous information the server had about the
client is lost - including authentication information.

**Sessions** provide a way to persevere data across requests.  We can persevere
authentication information so there is no need to re-enter credentials on every
new request the client makes to the server.

**Cookies** are small key/value pair data structures. They are passed back and
forth between client and server and stored in the browser .

The basic workflow when using *cookies* and *sessions* for authentication is:
- Client sends credentials
- Server verifies credentials
- Server creates a session for the client
- Server produces and sends back cookie
- Client stores the cookie
- Client sends the cookie on every request
- Server verifies the cookie is valid
- Server provides access to the resource

For Node.js, we can use [express-session](https://www.npmjs.com/package/express-session) to handle sessions.

### JSON Web Tokens

We can use JWTs (JSON Web Tokens) as an alternative to sessions and cookies.
When the user successfully logs in using their credentials, a JWT will be
returned and must be saved locally (typically in local storage).

A JWT is a string that has three parts separated by a period (.).  They are:

The **Header**, which contains the algorithm with the token type.
EG. 
```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
```
The **Payload**, which includes claims info or any other data we'd like to store
in the token (most likely a user id)
```javascript
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```
The **Signature** which is created by base64 encoding the header and payload
together, and then signing it with a secret

An example of a full JWT string: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

Check out the 'Debugger' section at [jwt.io](https://jwt.io) to play around with
the different parts and see out it changes the final output.

Example of JWT usage from Lambda School's TK:
```javascript
// ./auth/auth-router.js

const jwt = require('jsonwebtoken'); // installed this library

router.post('/login', (req, res) => {
  let { username, password } = req.body;

  Users.findBy({ username })
    .first()
    .then(user => {
      if (user && bcrypt.compareSync(password, user.password)) {
        const token = generateToken(user); // new line
 
        // the server needs to return the token to the client
        // this doesn't happen automatically like it happens with cookies
        res.status(200).json({
          message: `Welcome ${user.username}!, have a token...`,
          token, // attach the token as part of the response
        });
      } else {
        res.status(401).json({ message: 'Invalid Credentials' });
      }
    })
    .catch(error => {
      res.status(500).json(error);
    });
});

function generateToken(user) {
  const payload = {
    subject: user.id, // sub in payload is what the token is about
    username: user.username,
    // ...otherData
  };

  const options = {
    expiresIn: '1d', // show other available options in the library's documentation
  };

  // extract the secret away so it can be required and used where needed
  return jwt.sign(payload, secrets.jwtSecret, options); // this method is synchronous
}
```

### Testing

When building a Web API using Express, we use *unit testing* to test the
application logic, and *integration testing* to test the route handlers and
middleware.

The tests we write for endpoints are called *integration tests* because they
test how different parts of the system work together.  *Unit tests* are when we
verify the correctness of one part of the system in isolation.

Three questions commonly tested for our endpoints:
- Does it return the correct status for the input provided?
- Does it return the data in the expected format?
- Does the data returned, if any, have the right content?

Example of [supertest](https://github.com/visionmedia/supertest) usage from
Lambda School TK:
```javascript
/*
- when making a GET request to the `/` endpoint 
  the API should respond with status code 200 
  and the following JSON object: `{ api: 'running' }`.
*/
const request = require('supertest'); // calling it "request" is a common practice

const server = require('./server.js'); // this is our first red, file doesn't exist yet

describe('server.js', () => {
  // http calls made with supertest return promises, we can use async/await if desired
  describe('index route', () => {
    it('should return an OK status code from the index route', async () => {
      const expectedStatusCode = 200;

      // do a get request to our api (server.js) and inspect the response
      const response = await request(server).get('/');

      expect(response.status).toEqual(expectedStatusCode);

      // same test using promise .then() instead of async/await
      // let response;
      // return request(server).get('/').then(res => {
      //   response = res;

      //   expect(response.status).toEqual(expectedStatusCode);
      // })
    });

    it('should return a JSON object fron the index route', async () => {
      const expectedBody = { api: 'running' };

      const response = await request(server).get('/');

      expect(response.body).toEqual(expectedBody);
    });

    it('should return a JSON object fron the index route', async () => {
      const response = await request(server).get('/');

      expect(response.type).toEqual('application/json');
    });
  });
});
```

---

Overall, it was a very hectic two weeks but I learned a ton and it was a great wrap
up to the Back-end lectures.  I'll miss Sean Kirkby's lectures.  He was my favorite
instructor at Lambda School thus far.

Next up is Build Week. I'm excited to put my knowledge to the test and build out an
awesome backend!


