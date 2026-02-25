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

