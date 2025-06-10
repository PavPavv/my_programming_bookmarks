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

## Buffer

**Buffer** objects are used to represent a fixed-length sequence of bytes. Many Node.js APIs support **Buffers**.
The **Buffer** class is a subclass of JavaScript's **Uint8Array** class and extends it with methods that cover additional use cases. Node.js APIs accept plain **Uint8Array**s wherever Buffers are supported as well.

While the Buffer class is available within the global scope, it is still recommended to explicitly reference it via an import or require statement.

```javascript
const { Buffer } = require('node:buffer');

// Creates a zero-filled Buffer of length 10.
const buf1 = Buffer.alloc(10);

// Creates a Buffer of length 10,
// filled with bytes which all have the value `1`.
const buf2 = Buffer.alloc(10, 1);

// Creates an uninitialized buffer of length 10.
// This is faster than calling Buffer.alloc() but the returned
// Buffer instance might contain old data that needs to be
// overwritten using fill(), write(), or other functions that fill the Buffer's
// contents.
const buf3 = Buffer.allocUnsafe(10);

// Creates a Buffer containing the bytes [1, 2, 3].
const buf4 = Buffer.from([1, 2, 3]);

// Creates a Buffer containing the bytes [1, 1, 1, 1] – the entries
// are all truncated using `(value & 255)` to fit into the range 0–255.
// When you pass an array to Buffer.from(), each element of the array is converted to a byte (unsigned 8-bit integer, 0–255).
// Each value is coerced to a number, then masked to fit into 0–255.
// In JS, Number(257.5) truncated to integer is 257, then modulo 256: 257 % 256 = 1.
// In JS, negative numbers are converted via modulo 256: -255 % 256 = 1 (since -255 mod 256 = 1). So, this becomes 1.
// When passing an array with numbers like 257, 257.5, or negative numbers, Buffer.from() converts each to an 8-bit unsigned integer via modulo 256.
const buf5 = Buffer.from([257, 257.5, -255, '1']);

// Creates a Buffer containing the UTF-8-encoded bytes for the string 'tést':
// [0x74, 0xc3, 0xa9, 0x73, 0x74] (in hexadecimal notation)
// [116, 195, 169, 115, 116] (in decimal notation)
const buf6 = Buffer.from('tést');

// Creates a Buffer containing the Latin-1 bytes [0x74, 0xe9, 0x73, 0x74].
const buf7 = Buffer.from('tést', 'latin1');
```

**new Buffer()** is deprecated! The constructor **Buffer()** was deprecated in Node.js v10 and removed in v14. Instead, you should use **Buffer.from()**, **Buffer.alloc()**, or **Buffer.allocUnsafe()**.
**Buffer.of()** is a static method on the **Buffer** class, not an instance method. It's used to create a new Buffer from a list of values.

```javascript
Buffer.of(1, 2, 3); // creates a Buffer containing [1, 2, 3]
```

## net

In Node.js, both net.createConnection and net.connect are used to create a TCP connection to a server, but they are essentially the same and offer the same functionality with slight differences in usage. The presence of both functions is primarily for backward compatibility and code readability. Some developers
prefer net.createConnection as it might be more descriptive, while others might opt for net.connect as it is shorter. The write() method is used to send data from this socket to the remote server. This can be a string, Buffer, or an ArrayBuffer. If you send an object, it will be converted to a string using .toString(). A string that specifies the character encoding of the data, such as 'utf8', 'ascii', etc. The default encoding is 'utf8'.

## http

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
