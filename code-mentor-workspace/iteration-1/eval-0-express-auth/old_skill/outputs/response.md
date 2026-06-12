Starting with user authentication in Node.js and Express is a great milestone! Authentication generally involves three core pillars:
1. **Password Security**: Never storing passwords in plain text.
2. **Session/Token Management**: Remembering who the user is after they log in (typically via JSON Web Tokens (JWT) or Session Cookies).
3. **Route Protection**: Restricting access to certain endpoints using **middleware**.

Here is a step-by-step guide on how to design and start building your authentication system.

---

### 1. Choose Your Session Management Strategy
Before writing code, decide how your backend will remember logged-in users:
* **JSON Web Tokens (JWT)** (Common for APIs/SPAs): The backend issues a signed token to the client upon login. The client sends this token in the header of subsequent requests. It is stateless, meaning the server doesn't need to store session data in a database.
* **Cookie-Based Sessions**: The server creates a session store (e.g., using `express-session`) and sends a session ID inside a secure cookie. The browser automatically sends this cookie with every request.

### 2. Set Up Password Hashing
When a user registers, you must hash their password before saving it to your database. Never store plain-text passwords. Use a library like `bcryptjs` to hash and compare passwords:
* **Hash on Sign-up**: `await bcrypt.hash(password, saltRounds)`
* **Compare on Login**: `await bcrypt.compare(password, hashedPassword)`

### 3. Implement Authentication Middleware
In Express, middleware functions run before your route handlers. This is the perfect place to check if a user is authenticated. If they are, you let the request proceed; if not, you block it and return a `401 Unauthorized` status.

Here is a minimal, idiomatic example of what an authentication middleware skeleton looks like using JSON Web Tokens (JWT):

```javascript
// middleware/auth.js
const jwt = require('jsonwebtoken');

const requireAuth = (req, res, next) => {
  // 1. Get the token from the Authorization header
  const authHeader = req.headers.authorization;
  
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ message: 'Authentication token required' });
  }

  const token = authHeader.split(' ')[1];

  try {
    // 2. Verify the token using your secret key
    const decoded = jwt.verify(token, process.env.JWT_SECRET || 'your_fallback_secret');
    
    // 3. Attach the user data to the request object so subsequent routes can use it
    req.user = decoded;
    
    // 4. Pass control to the next middleware or route handler
    next();
  } catch (error) {
    return res.status(403).json({ message: 'Invalid or expired token' });
  }
};

module.exports = requireAuth;
```

You would use this middleware to protect your routes like this:

```javascript
// routes/profile.js
const express = require('express');
const router = express.Router();
const requireAuth = require('../middleware/auth');

// This route is now protected! Only authenticated requests can reach it.
router.get('/profile', requireAuth, (req, res) => {
  res.json({ 
    message: 'Welcome to your profile!', 
    userId: req.user.id 
  });
});

module.exports = router;
```

---

## Conceptual Insight

In Express, authentication relies heavily on the **Middleware Pattern**. Express routes request and response objects through a chain of functions. When you place an authentication middleware before a route handler, you create a gatekeeper. By attaching decoded user data directly to `req.user` inside the middleware, you ensure that any downstream route handler can access the current user's identity cleanly, without needing to verify tokens repeatedly. 

Another critical concept is **cryptographic hashing vs encryption**. Passwords must be hashed using a slow, one-way cryptographic function with a "salt" (a random piece of data added to the password). Unlike encryption, hashing cannot be reversed. When a user logs in, you run their input password through the same hashing function and check if the result matches the stored hash. This ensures that even if your database is compromised, the attackers cannot easily reverse-engineer the original passwords.

---

## Next Step Exercise

1. **Install Dependencies**: Open your terminal in your Node/Express project directory and install `bcryptjs` and `jsonwebtoken`:
   ```bash
   npm install bcryptjs jsonwebtoken
   ```
2. **Create a Test Middleware**: Create a file named `auth.js` in your project and write a simple middleware function that looks for a custom header (e.g., `x-mock-auth: true`). If the header is missing, return a `401` status. If it's present, call `next()`. Mount this middleware on one of your test routes and verify that it blocks requests when the header is missing.
