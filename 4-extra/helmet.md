# Using `helmet.js` for Secure HTTP Headers in Node Express App

## Overview

`helmet.js` is a security middleware for Node.js Express applications that helps you set various HTTP headers to enhance security. This README.md provides a detailed guide on integrating and configuring `helmet.js` in a Node Express application.

## Prerequisites

Make sure you have a Node.js Express application already set up.

```bash
npm init -y
npm install express
```

## Installation

Install `helmet.js` using npm:

```bash
npm install helmet
```

## Configuration

### 1. Import `helmet` in your Express App

In your main server file (e.g., `app.js`), import `helmet` and use it as middleware:

```javascript
// app.js

const express = require('express');
const helmet = require('helmet');

const app = express();

// Use helmet middleware
app.use(helmet());
```

### 2. Helmet Middleware Configuration

You can configure `helmet` to enable or disable specific features according to your application's needs. Here's an example with common configurations:

```javascript
// app.js

const express = require('express');
const helmet = require('helmet');

const app = express();

// Use helmet middleware with specific configurations
app.use(
  helmet({
    contentSecurityPolicy: {
      directives: {
        defaultSrc: ["'self'"],
        scriptSrc: ["'self'", 'trusted-scripts.com'],
        styleSrc: ['style.com']
      }
    },
    frameguard: { action: 'deny' },
    referrerPolicy: { policy: 'same-origin' }
    // Add more configurations as needed
  })
);
```

### 3. Helmet Configuration Details

Here's a breakdown of some common configurations you can set using `helmet`:

- **Content Security Policy (CSP):**

  - `defaultSrc`: Specifies the default source for fetch directives.
  - `scriptSrc`: Defines valid sources for JavaScript.
  - `styleSrc`: Specifies valid sources for stylesheets.

- **Frameguard:**

  - `action`: Determines the action to take when X-Frame-Options denies framing. Options include 'deny', 'sameorigin', 'allow-from', or a URL.

- **Referrer Policy:**

  - `policy`: Sets the value of the Referrer-Policy header.

- **Other Configurations:**
  - Explore other configurations such as `noCache()`, `hidePoweredBy()`, `hsts()`, `dnsPrefetchControl()`, etc., based on your security requirements.

## Usage

Once configured, `helmet` will automatically set the appropriate HTTP headers for security. Test your application and ensure that the headers are applied as expected.
