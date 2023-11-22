# Socket.IO

## Overview

Socket.IO is a JavaScript library designed for real-time web applications, facilitating seamless and bidirectional communication between web clients and servers. This README.md file provides an in-depth guide on integrating and utilizing Socket.IO in both the server and client components.

## Server-side Integration

### Installation

To begin using Socket.IO on the server, install the required packages using npm:

```bash
npm install express socket.io
```

### Implementation

Below is an example illustrating how to integrate Socket.IO into your Node.js server with Express:

```javascript
import express from 'express';
import { Server } from 'socket.io';

const PORT = process.env.PORT || 5000;

const app = express();

// Define a basic route
app.get('/', (req, res) => {
  res.status(200).json({ message: 'Hello there' });
});

// Set up the server
const server = app.listen(PORT, () => {
  console.log(`Server is up and running on port ${PORT}`);
});

// Create a new instance of Socket.IO, configuring CORS
const io = new Server(server, {
  cors: {
    origin: 'http://localhost:3000'
  }
});

// Handle connection events
io.on('connection', (socket) => {
  console.log(`a user with id ${socket.id} connected`);

  // Handle custom events
  socket.on('addUser', (user) => {
    console.log(user);
    socket.emit('userInfoReceived', { message: `${user.name} received` });
  });

  // Handle disconnection events
  socket.on('disconnect', () => {
    console.log(`a user with id ${socket.id} disconnected`);
  });
});
```

### Understanding Events

Sockets in Socket.IO operate based on events. Reserved events include 'connection,' 'message,' 'disconnect,' 'reconnect,' 'ping,' 'join,' and 'leave.' You can also create custom events like 'addUser' and 'userInfoReceived.'

## Client-side Integration

### Installation

For the client-side, install the Socket.IO client using npm:

```bash
npm install socket.io-client
```

### Implementation

Here's an example of integrating Socket.IO on the client side:

```javascript
import io from 'socket.io-client';

// Connect to the server
const socket = io('http://localhost:5000');

// Define user information
const user = {
  name: 'John',
  age: 25
};

// Emit a custom event 'addUser' with user information
socket.emit('addUser', user);

// Listen for the 'userInfoReceived' event
socket.on('userInfoReceived', (message) => {
  console.log(message);
});

// Other client-side events include 'connect,' 'connect_error,' 'connect_timeout,' 'reconnect,' and custom events.
```

This comprehensive guide covers the installation and implementation of Socket.IO on both the server and client sides. Feel free to explore and customize the code to suit your specific real-time communication needs.
