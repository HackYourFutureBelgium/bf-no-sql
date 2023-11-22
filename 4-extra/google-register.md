# Integrating Google Account Registration in MERN App

This README.md provides a detailed guide on implementing Google account registration in your MERN (MongoDB, Express.js, React, Node.js) application using OAuth 2.0 authentication.

## Prerequisites

Ensure you have the following:

- A MERN stack application set up.
- A Google Cloud Platform (GCP) project with the necessary credentials.
- Basic knowledge of OAuth 2.0.

## Steps

### 1. Create a GCP Project

- Go to the [Google Cloud Console](https://console.cloud.google.com/).
- Create a new project or select an existing one.

### 2. Enable Google API

- In the Google Cloud Console, navigate to the "APIs & Services" > "Dashboard."
- Click on "+ ENABLE APIS AND SERVICES" and search for "Google+ API." Enable it.

### 3. Create OAuth 2.0 Credentials

- In the Google Cloud Console, navigate to "APIs & Services" > "Credentials."
- Click on "Create Credentials" > "OAuth client ID."
- Choose "Web application."
- Set the authorized JavaScript origins and redirect URIs for your app.

### 4. Set Up OAuth in Your Server (Node.js/Express)

- Install necessary packages:

  ```bash
  npm install express passport passport-google-oauth20 express-session
  ```

- Create a route for Google OAuth:

  ```javascript
  // routes/auth.js

  const express = require('express');
  const passport = require('passport');
  const router = express.Router();

  // OAuth 2.0 with Passport
  router.get(
    '/google',
    passport.authenticate('google', { scope: ['profile', 'email'] })
  );

  router.get(
    '/google/callback',
    passport.authenticate('google', { failureRedirect: '/' }),
    (req, res) => {
      res.redirect('/dashboard'); // Redirect to your app after successful login
    }
  );

  module.exports = router;
  ```

### 5. Implement OAuth in Your Server (Node.js/Express)

- Set up Passport with Google OAuth:

  ```javascript
  // config/passport.js

  const passport = require('passport');
  const GoogleStrategy = require('passport-google-oauth20').Strategy;

  passport.use(
    new GoogleStrategy(
      {
        clientID: 'YOUR_GOOGLE_CLIENT_ID',
        clientSecret: 'YOUR_GOOGLE_CLIENT_SECRET',
        callbackURL: 'http://localhost:5000/auth/google/callback' // Update with your callback URL
      },
      (accessToken, refreshToken, profile, done) => {
        // Implement user creation or retrieval logic
        return done(null, profile);
      }
    )
  );

  passport.serializeUser((user, done) => {
    done(null, user);
  });

  passport.deserializeUser((obj, done) => {
    done(null, obj);
  });

  module.exports = passport;
  ```

- Integrate Passport into your Express app:

  ```javascript
  // app.js

  const express = require('express');
  const passport = require('./config/passport'); // Path to your passport configuration
  const session = require('express-session');
  const authRoutes = require('./routes/auth');

  const app = express();

  // Configure session
  app.use(
    session({
      secret: 'your-secret-key',
      resave: true,
      saveUninitialized: true
    })
  );

  // Initialize Passport
  app.use(passport.initialize());
  app.use(passport.session());

  // Use your auth routes
  app.use('/auth', authRoutes);

  // ... Other routes and middleware

  const PORT = process.env.PORT || 5000;
  app.listen(PORT, () => console.log(`Server is running on port ${PORT}`));
  ```

### 6. Set Up OAuth in Your React App

- Install necessary packages:

  ```bash
  npm install react-google-login
  ```

- Create a Google Login component:

  ```jsx
  // components/GoogleLoginButton.js

  import React from 'react';
  import { GoogleLogin } from 'react-google-login';

  const GoogleLoginButton = () => {
    const responseGoogle = (response) => {
      // Handle the Google response, e.g., send it to your server for authentication
      console.log(response);
    };

    return (
      <GoogleLogin
        clientId="YOUR_GOOGLE_CLIENT_ID"
        buttonText="Login with Google"
        onSuccess={responseGoogle}
        onFailure={responseGoogle}
        cookiePolicy={'single_host_origin'}
      />
    );
  };

  export default GoogleLoginButton;
  ```

- Use the Google Login component in your app:

  ```jsx
  // App.js

  import React from 'react';
  import GoogleLoginButton from './components/GoogleLoginButton';

  const App = () => {
    return (
      <div>
        {/* Your app content */}
        <GoogleLoginButton />
      </div>
    );
  };

  export default App;
  ```

### 7. Testing

- Run your MERN app and test the Google login functionality.
  Certainly! Here's the updated version using ES6 import/export syntax:

### 1. Create a GCP Project

- Create or select a project on the [Google Cloud Console](https://console.cloud.google.com/).

### 2. Enable Google API

- Enable the "Google+ API" in the "APIs & Services" section.

### 3. Create OAuth 2.0 Credentials

- Create OAuth 2.0 credentials in the "Credentials" section with authorized origins and redirect URIs.

### 4. Set Up OAuth in Your Server (Node.js/Express)

#### Install necessary packages:

```bash
npm install express passport passport-google-oauth20 express-session
```

#### Create a route for Google OAuth:

```javascript
// routes/auth.js

import express from 'express';
import passport from 'passport';

const router = express.Router();

// OAuth 2.0 with Passport
router.get(
  '/google',
  passport.authenticate('google', { scope: ['profile', 'email'] })
);

router.get(
  '/google/callback',
  passport.authenticate('google', { failureRedirect: '/' }),
  (req, res) => {
    res.redirect('/dashboard'); // Redirect to your app after successful login
  }
);

export default router;
```

### 5. Implement OAuth in Your Server (Node.js/Express)

#### Set up Passport with Google OAuth:

```javascript
// config/passport.js

import passport from 'passport';
import { Strategy as GoogleStrategy } from 'passport-google-oauth20';

passport.use(
  new GoogleStrategy(
    {
      clientID: 'YOUR_GOOGLE_CLIENT_ID',
      clientSecret: 'YOUR_GOOGLE_CLIENT_SECRET',
      callbackURL: 'http://localhost:5000/auth/google/callback' // Update with your callback URL
    },
    (accessToken, refreshToken, profile, done) => {
      // Implement user creation or retrieval logic
      return done(null, profile);
    }
  )
);

passport.serializeUser((user, done) => {
  done(null, user);
});

passport.deserializeUser((obj, done) => {
  done(null, obj);
});

export default passport;
```

#### Integrate Passport into your Express app:

```javascript
// app.js

import express from 'express';
import session from 'express-session';
import passport from './config/passport'; // Path to your passport configuration
import authRoutes from './routes/auth';

const app = express();

// Configure session
app.use(
  session({
    secret: 'your-secret-key',
    resave: true,
    saveUninitialized: true
  })
);

// Initialize Passport
app.use(passport.initialize());
app.use(passport.session());

// Use your auth routes
app.use('/auth', authRoutes);

// ... Other routes and middleware

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server is running on port ${PORT}`));
```

### 6. Set Up OAuth in Your React App

#### Install necessary packages:

```bash
npm install react-google-login
```

#### Create a Google Login component:

```jsx
// components/GoogleLoginButton.js

import React from 'react';
import { GoogleLogin } from 'react-google-login';

const GoogleLoginButton = () => {
  const responseGoogle = (response) => {
    // Handle the Google response, e.g., send it to your server for authentication
    console.log(response);
  };

  return (
    <GoogleLogin
      clientId="YOUR_GOOGLE_CLIENT_ID"
      buttonText="Login with Google"
      onSuccess={responseGoogle}
      onFailure={responseGoogle}
      cookiePolicy={'single_host_origin'}
    />
  );
};

export default GoogleLoginButton;
```

#### Use the Google Login component in your app:

```jsx
// App.js

import React from 'react';
import GoogleLoginButton from './components/GoogleLoginButton';

const App = () => {
  return (
    <div>
      {/* Your app content */}
      <GoogleLoginButton />
    </div>
  );
};

export default App;
```

### 7. Testing

- Run your MERN app and test the Google login functionality.
