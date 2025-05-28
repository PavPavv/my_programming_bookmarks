# My NodeJS cheat sheet

## Event loop

<!-- ADD -->

## Module system

<!-- ADD -->

## Filesystem (fs+path)

<!-- ADD -->

## Streams

### What is objectMode?

In Node.js, particularly when working with streams, objectMode is a property that you can set when creating readable or writable streams. By default, streams in Node.js operate in "byte mode", which means they treat the data flowing through the stream as a sequence of bytes (or buffers). However, sometimes you may want to work with more complex data structures like objects. This is where objectMode comes into play.

When you enable objectMode, the stream will handle JavaScript objects instead of just raw binary data. This is particularly useful for applications that need to process or transform data represented as objects, such as JSON data or any other structured information.

```javascript
const { Readable, Writable } = require('stream');

// Create a readable stream in object mode
const readable = new Readable({
  objectMode: true,
  read() {
    this.push({ message: 'Hello, World!' });
    this.push(null); // Signal that there's no more data
  }
});

// Create a writable stream in object mode
const writable = new Writable({
  objectMode: true,
  write(chunk, encoding, callback) {
    console.log(chunk); // Process the object
    callback();
  }
});

// Pipe the readable stream into the writable stream
readable.pipe(writable);
```

## Development

### Docker

#### Basic minimal Dockerfile to start develop in Node.js

```Dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 4800

CMD ["node", "src/index.js"]
```

#### Deploy

1. Rent a remote server
2. Install Node, git and Docker there via ssh command