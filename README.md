# Jwt-Notes
Basic JWT notes

We will use the jsonwebtoken npm package.
Link: https://www.npmjs.com/package/jsonwebtoken
```
npm i jsonwebtokens
```

```
import jwt from 'jsonwebtokens'
```

How to create a token:
```
//jwt.sign(payload, secretOrPrivateKey, [options, callback])
```
- If callback is supplied, the callback is called with err or the JWT
- Synchronous: Returns the token as a string
- Make the payload an object, but it can be a buffer, or string of valid JSON
- Object literal payload will be turned to a string with JSON.stringify
- SecretOrPrivateKey is a string(utf-8 encoded), buffer, object, or KeyObjext containing either the secret from HMAC algo or the PEM encoded private key for RSA and ECDSA. (Read more in case you're interested in the page, I won't go into it)
- options:
  - algorithm(default: HS256)
  - expiresIn: in seconds, or a string of time spam vercel/ms (look below)
    - ex: 60, "2 days", "10h", "7d"
  - notBefore() expressed just like expiresIn
  - noTimestamp
There are more options, reference the npm page.

How to sign the token with the default algo?
```
const token = jwt.sign({ foo: 'bar' }, 'shhhh')
```

It does have a builtin exp to set when it expires, it's part of the payload:
```
jwt.sign({
  exp: Math.floor(Date.now() / 1000) + (60 * 60),
  payload: 'foobar'
}, 'secret')
```
Other options to set an expiration date:
```
jwt.sign({
  data: 'foobar'
}, 'secret', { expiresIn: 60 * 60 });

//or even better:

jwt.sign({
  data: 'foobar'
}, 'secret', { expiresIn: '1h' });
```

How to verify tokens:
```
//jwt.verify(token, secretKey, [options/callback])
```

When using a library like jsonwebtoken in Node.js, the jwt.verify() function's return value depends on how it is called: 
Synchronous use (no callback provided): It returns the decoded payload of the JWT if the signature is valid and all other validations (like expiration, audience, issuer) pass. If verification fails for any reason (e.g., invalid signature, expired token), it will throw an error (e.g., JsonWebTokenError, TokenExpiredError).
Asynchronous use (callback provided): It returns nothing (or undefined), and the result is handled via a callback function. The callback receives two arguments: (err, decoded).
If verification is successful, err will be null and the decoded argument will contain the decoded payload.
If verification fails, err will contain the specific error, and decoded will be undefined.
