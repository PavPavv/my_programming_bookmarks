# HTTP basics

> > The Hypertext Transfer Protocol (HTTP) is the protocol programs use to communicate over the World Wide Web. There are many applications of HTTP, but HTTP is most famous for two-way conversation between web browsers and web servers.

## Overview of HTTP

### Media Types

Because the Internet hosts many thousands of different data types, HTTP carefully tags each object being transported through the Web with a data format label called a MIME type. MIME (Multipurpose Internet Mail Extensions) was originally designed to solve problems encountered in moving messages between different electronic mail systems. MIME worked so well for email that HTTP adopted it to describe and label its own multimedia content.

Web servers attach a MIME type to all HTTP object data. When a web browser gets an object back from a server, it looks at the associated MIME type to see if it knows how to handle the object. Most browsers can handle hundreds of popular object types: displaying image files, parsing and formatting HTML files, playing audio files through the computer’s speakers, or launching external plug-in software to handle special formats.

A MIME type is a textual label, represented as a primary object type and a specific subtype, separated by a slash. For example:

- An HTML-formatted text document would be labeled with type _text/html_

- A plain ASCII text document would be labeled with type _text/plain_

- A JPEG version of an image would be _image/jpeg_

- A GIF-format image would be _image/gif_

- An Apple QuickTime movie would be _video/quicktime_

- A Microsoft PowerPoint presentation would be _application/vnd.ms-powerpoint_

### URI (Uniform resource identifier), URN(uniform resource name), URL(Uniform resource locator)

The server resource name is called a uniform resource identifier, or URI. All URLs can be URIs, but all URIs cannot be URLs. It is because a URI contains both URL and URN and represent URL or URN, or both.

### HTTP Transaction

An HTTP transaction consists of a request command (sent from client to server), and a response result (sent from the server back to the client). This communication happens with formatted blocks of data called HTTP messages.

### Methods

HTTP supports several different request commands, called HTTP methods. Every HTTP request message has a method.

### Status Codes

Every HTTP response message comes back with a status code. The status code is a three-digit numeric code that tells the client if the request succeeded, or if other actions are required.

### Request/Response message structure

HTTP messages consist of three parts:

- **Start line** (The first line of the message is the start line, indicating what to do for a request or what happened for a response.)

- **Header fields** (Zero or more header fields follow the start line. Each header field consists of a name and a value, separated by a colon (:) for easy parsing. The headers end with a blank line. Adding a header field is as easy as adding another line.)

- **Body\*** (After the blank line is an optional message body containing any kind of data. Request bodies carry data to the web server; response bodies carry data back to the client. Unlike the start lines and headers, which are textual and structured, the body can contain arbitrary binary data (e.g., images, videos, audio tracks, software applications). Of course, the body can also contain text.)

### TCP/IP

HTTP is an application layer protocol. HTTP doesn’t worry about the nitty-gritty details of network communication; instead, it leaves the details of networking to TCP/IP, the popular reliable Internet transport protocol.

HTTP network protocol stack:

1. Physical network hardware
2. Network-specific link interface
3. IP
4. TCP
5. HTTP

Before an HTTP client can send a message to a server, it needs to establish a TCP/IP connection between the client and server using Internet protocol (IP) addresses and port numbers.

Hostnames can easily be converted into IP addresses through a facility called the Domain Name Service (DNS). The final URL has no port number. When the port number is missing from an HTTP URL, you can assume the default value of port 80.

### Architectural Components of the Web

- Proxies (HTTP intermediaries that sit between clients and servers)

- Caches(HTTP storehouses that keep copies of popular web pages close to clients)

- Gateways (Special web servers that connect to other applications)

- Tunnels (Special proxies that blindly forward HTTP communications)

- Agents (Semi-intelligent web clients that make automated HTTP requests)

One popular use of HTTP tunnels is to carry encrypted Secure Sockets Layer (SSL) traffic through an HTTP connection, allowing SSL traffic through corporate firewalls that permit only web traffic.

## URLs and Resources

> > "http://www.some-site.com/seasonal/index-fall.html"

- where http:// is a scheme (how) _client_

- www.some-site.com is a host (where) _server_

- /seasonal/index-fall.html (what) _disk_

Most URL schemes base their URL syntax on this nine-part general format:

HTTP

```xml
<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
```

HTTPS

```xml
https://<host>:<port>/<path>?<query>#<frag>
```

- _scheme_ - Which protocol to use when accessing a server to get a resource.

- _user_ - The username some schemes require to access a resource.

- _password_ - The password that may be included after the username, separated by a colon (:).

- _host_ - The hostname or dotted IP address of the server hosting the resource.

- _port_ - The port number on which the server hosting the resource is listening. Many schemes have default port numbers (the default port number for HTTP is 80).

- _path_ - The local name for the resource on the server, separated from the previous URL components by a slash (/). The syntax of the path component is server- and scheme-specific. (We will see later in this chapter that a URL’s path can be divided into segments, and each segment can have its own components specific to that segment.)

- _params_ - Used by some schemes to specify input parameters. Params are name/value pairs. A URL can contain multiple params fields, separated from themselves and the rest of the path by semicolons (;).

- _query_ - Used by some schemes to pass parameters to active applications (such as databases, bulletin boards, search engines, and other Internet gateways). There is no common format for the contents of the query component. It is separated from the rest of the URL by the “?” character.

- _frag_ - A name for a piece or part of the resource. The frag field is not passed to the server when referencing the object; it is used internally by the client. It is separated from the rest of the URL by the “#” character.

## HTTP messages

HTTP messages are the blocks of data sent between HTTP applications. HTTP uses the terms _inbound_ and _outbound_ to describe transactional direction. Messages travel inbound to the origin server, and when their work is done, they travel outbound back to the user agent. HTTP messages flow like rivers. All messages flow downstream, regardless of whether they are request messages or response messages. The sender of any message is upstream of the receiver.

All HTTP messages fall into two types: request messages and response messages. Request messages request an action from a web server. Response messages carry results of a request back to a client.

Note that a set of HTTP headers should always end in a blank line (bare CRLF), even if there are no headers and even if there is no entity body.

All HTTP messages begin with a **start line**. The start line for a request message says what to do. The start line for a response message says what happened.

As methods tell the server what to do, status codes tell the client what happened.

### Status code classes

- 100-101 - Informational
- 200-206 - Successful
- 300-305 - Redirection
- 400-415 - Client error
- 500-505 - Server error

### Header classifications

- **General**- Can appear in both request and response messages
  - general
  - cache control headers
- **Request**- Provide more information about the request
  - Request informational headers
  - Accept headers
  - Conditional request headers
  - Request security headers
  - Proxy request headers
- **Response**- Provide more information about the response
  - Response informational headers
  - Negotiation headers
  - Response security headers
- **Entity**- Describe body size and contents, or the resource itself
  - Entity informational headers
  - Content headers
  - Entity caching headers
- **Extension**- New headers that are not defined in the specification

### HTTP Methods

#### GET

GET is the most common method. It usually is used to ask a server to send a resource.

#### HEAD

The HEAD method behaves exactly like the GET method, but the server returns only the headers in the response. No entity body is ever returned. This allows a client to inspect the headers for a resource without having to actually get the resource.

#### POST

The POST method was designed to send input data to the server. POST is used to send data to a server. PUT is used to deposit data into a resource on the server

#### PUT

The PUT method writes documents to a server, in the inverse of the way that GET reads documents from a server. The semantics of the PUT method are for the server to take the body of the request and either use it to create a new document named by the requested URL or, if that URL already exists, use the body to replace it.

#### TRACE

When a client makes a request, that request may have to travel through firewalls, proxies, gateways, or other applications. Each of these has the opportunity to modify the original HTTP request. The TRACE method allows clients to see how its request looks when it finally makes it to the server.

#### OPTIONS

The OPTIONS method asks the server to tell us about the various supported capabilities of the web server. You can ask a server about what methods it supports in general or for particular resources.

#### DELETE

#### PATCH

## Connection Management

HTTP connections really are nothing more than TCP connections, plus a few rules about how to use them. TCP connections are the reliable connections of the Internet.

1. The browser extracts the hostname
2. The browser looks up the IP address for this hostname (DNS)
3. The browser gets the port number (80 by default)
4. The browser makes a TCP connection to ip-address with certain port
5. The browser sends an HTTP GET request message to the server
6. The browser reads the HTTP response message from the server
7. The browser closes the connection

TCP gives HTTP a reliable bit pipe. Bytes stuffed in one side of a TCP connection come out the other side correctly, and in the right order.
TCP sends its data in little chunks called IP packets (or IP datagrams). In this way, HTTP is the top layer in a “protocol stack” of “HTTP over TCP over IP”. A secure variant, HTTPS, inserts a cryptographic encryption layer (called TLS or SSL) between HTTP and TCP.

When HTTP wants to transmit a message, it streams the contents of the message data, in order, through an open TCP connection. TCP takes the stream of data, chops up the data stream into chunks called segments, and transports the segments across the Internet inside envelopes called IP packets.

Each TCP segment is carried by an IP packet from one IP address to another IP
address. Each of these IP packets contains:

- An IP packet header (usually 20 bytes)
- A TCP segment header (usually 20 bytes)
- A chunk of TCP data (0 or more bytes)

A computer might have several TCP connections open at any one time. TCP keeps all these connections straight through port numbers.

A TCP connection is distinguished by four values:

```xml
<source-IP-address, source-port, destination-IP-address, destination-port>
```

### A brief overview of TCP performance

When you set up a new TCP connection, even before you send any data, the TCP software exchanges a series of IP packets to negotiate the terms of the connection.
The HTTP programmer never sees these packets—they are managed invisibly by the TCP/IP software. All the HTTP programmer sees is a delay when creating a new TCP connection.

> IP packets are usually a few hundred bytes for Internet traffic and around 1,500 bytes for local traffic.

Each TCP segment gets a sequence number and a data-integrity checksum. The receiver of each segment returns small acknowledgment packets back to the sender when segments have been received intact. If a sender does not receive an acknowledgment within a specified window of time, the sender concludes the packet was destroyed or corrupted and resends the data.

TCP slow start throttles the number of packets a TCP endpoint can have in flight at any one time. Put simply, each time a packet is received successfully, the sender gets permission to send two more packets. If an HTTP transaction has a large amount of data to send, it cannot send all the packets at once. It must send one packet and wait for an acknowledgment; then it can send two packets, each of which must be acknowledged, which allows four packets, etc. This is called “opening the congestion window.”


TCP has a data stream interface that permits applications to stream data of any size to the TCP stack—even a single byte at a time! But because each TCP segment carries at least 40 bytes of flags and headers, network performance can be degraded severely if TCP sends large numbers of packets containing small amounts of data. Sending a storm of single-byte packets is called “sender silly window syndrome.” This is inefficient, antisocial, and can be disruptive to other Internet traffic.

TCP connections are bidirectional. Each side of a TCP connection has an input queue and an output queue, for data being read or written. Data placed in the output of one side will eventually show up on the input of the other side. An application can close either or both of the TCP input and output channels. A **close()** sockets call closes both the input and output channels of a TCP connection. You can use the **shutdown()** sockets call to close either the input or output channel individually. This is called a “half close”.
Simple HTTP applications can use only full closes. But when applications start talking to many other types of HTTP clients, servers, and proxies, and when they start using pipelined persistent connections, it becomes important for them to use half closes to prevent peers from getting unexpected write errors.

In general, applications implementing graceful closes will first close their output channels and then wait for the peer on the other side of the connection to close its output channels. When both sides are done telling each other they won’t be sending any more data (i.e., closing output channels), the connection can be closed fully, with no risk of reset.

### HTTP Connection Handling

HTTP allows a chain of HTTP intermediaries between the client and the ultimate origin server (proxies, caches, etc.). HTTP messages are forwarded hop by hop from the client, through intermediary devices, to the origin server (or the reverse).
When an HTTP application receives a message with a Connection header, the receiver parses and applies all options requested by the sender.

#### Parallel connections

Concurrent HTTP requests across multiple TCP connection.
HTTP allows clients to open multiple connections and perform multiple HTTP transactions in parallel.
In practice, browsers do use parallel connections, but they limit the total number of parallel connections to a small number (often four). Servers are free to close excessive connections from a particular client.

- parallel connections have some disadvantages:
  - each transaction opens/closes a new connection, costing time and bandwidth
  - each new connection has reduced performance because of TCP slow start
  - there is a practical limit on the number of open parallel connections

#### Persistent connections

Reusing TCP connections to eliminate connect/close delays. Persistent connections stay open across transactions, until either the client or the server decides to close them.
Persistent connection that is already open to the target server, you can avoid the slow connection setup. Persistent connections can be most effective when used in conjunction with parallel connections. Today, many web applications open a small number of parallel connections, each persistent.

#### Pipelined connections

Concurrent HTTP requests across a shared TCP connection. This is a further performance optimization over keep-alive connections. Multiple requests can be enqueued before the responses arrive.

#### Multiplexed connections

Interleaving chunks of requests and responses (experimental).

#### Connection close

Any HTTP client, server, or proxy can close a TCP transport connection at any time. The connections normally are closed at the end of a message, * but during error conditions, the connection may be closed in the middle of a header line or in other strange places.

Each HTTP response should have an accurate Content-Length header to describe the size of the response body. Some older HTTP servers omit the Content-Length header or include an erroneous length, depending on a server connection close to signify the actual end of data. When a client or proxy receives an HTTP response terminating in connection close, and the actual transferred entity length doesn’t match the Content-Length (or there is no Content-Length), the receiver should question the correctness of the length.

Connections can close at any time, even in non-error conditions. HTTP applications have to be ready to properly handle unexpected closes. If a transport connection closes while the client is performing a transaction, the client should reopen the connection and retry one time, unless the transaction has side effects.

Side effects are important. When a connection closes after some request data was sent but before the response is returned, the client cannot be 100% sure how much of the transaction actually was invoked by the server. Some transactions, such as GETting a static HTML page, can be repeated again and again without changing anything. Other transactions, such as POSTing an order to an online book store, shouldn’t be repeated, or you may risk multiple orders. A transaction is idempotent if it yields the same result regardless of whether it is exe-
cuted once or many times. Implementors can assume the GET, HEAD, PUT, DELETE, TRACE, and OPTIONS methods share this property.

Nonidempotent methods or sequences must not be retried automatically, although user agents may offer a human operator the choice of retrying the request. For example, most browsers will offer a dialog box when reloading a cached POST response, asking if you want to post the transaction again.

## HTTP Architecture

### Web Servers

A web server processes HTTP requests and serves responses. The term “web server” can refer either to web server software or to the particular device or computer dedicated to serving the web pages.
Web servers implement HTTP and the related TCP connection handling. They also manage the resources served by the web server and provide administrative features to configure, control, and enhance the web server. The web server logic shares responsibilities for managing TCP connections with the operating system.

#### General-Purpose Software Web Servers

General-purpose software web servers run on standard, network-enabled computer systems.

##### What Real Web Servers Do

1. Set up connection—accept a client connection, or close if the client is unwanted.
2. Receive request — read an HTTP request message from the network.
3. Process request — interpret the request message and take action.
4. Access resource — access the resource specified in the message.
5. Construct response — create the HTTP response message with the right headers.
6. Send response — send the response back to the client.
7. Log transaction — place notes about the completed transaction in a log file

##### Step 1: Accepting Client Connections

When a client requests a TCP connection to the web server, the web server establishes the connection and determines which client is on the other side of the connection, extracting the IP address from the TCP connection. (Different operating systems have different interfaces and data structures for manipulating TCP connections. In Unix environments, the TCP connection is represented by a socket, and the IP address of the client can be found from the socket using the getpeername call.)

Some web servers also support the IETF ident protocol. The ident protocol lets servers find out what username initiated an HTTP connection. This Common Log Format ident field is called “rfc931,” after an outdated version of the RFC defining the ident protocol (the updated ident specification is documented by RFC 1413).

##### Step 2: Receiving Request Messages

When parsing the request message, the web server:

- Parses the request line looking for the request method, the specified resource identifier (URI), and the version number, * each separated by a single space, and ending with a carriage-return line-feed (CRLF) sequence
- Reads the message headers, each ending in CRLF
- Detects the end-of-headers blank line, ending in CRLF (if present)
- Reads the request body, if any (length specified by the Content-Length header)

###### Internal Representations of Messages

Some web servers also store the request messages in internal data structures that make the message easy to manipulate. For example, the data structure might con-
tain pointers and lengths of each piece of the request message, and the headers might be stored in a fast lookup table so the specific values of particular headers can be accessed quickly.

###### Connection Input/Output Processing Architectures

High-performance web servers support thousands of simultaneous connections. Web servers constantly watch for new web requests, because requests can arrive at
any time.

- **Single-threaded web servers**

Single-threaded web servers process one request at a time until completion. This architecture is simple to implement, but during processing, all the other connections are ignored. This creates serious performance problems and is appropriate only for low-load servers and diagnostic tools like type-o-serve.

- **Multiprocess and multithreaded web servers**

Multiprocess and multithreaded web servers dedicate multiple processes or higher-efficiency threads to process requests simultaneously.
A process is an individual program flow of control, with its own set of variables. A thread is a faster, more efficient version of a process. Both threads and processes let a single program do multiple things at the same time. For simplicity of explanation, we treat processes and threads interchangeably. But, because of the performance differences, many high-performance servers are both multiprocess and multithreaded.
The threads/processes may be created on demand or in advance. Systems where threads are created in advance are called “worker pool” systems, because a set of threads
waits in a pool for work to do.

- **Multiplexed I/O servers**

To support large numbers of connections, many web servers adopt multiplexed architectures. In a multiplexed architecture, all the connections are simultaneously watched for activity. When a connection changes state (e.g., when data becomes available or an error condition occurs), a small amount of processing is performed on the connection; when that processing is complete, the connection is returned to the open connection list for the next change in state. Work is done on a connection only when there is something to be done; threads and processes are not tied up waiting on idle connections.

- **Multiplexed multithreaded web servers**

Some systems combine multithreading and multiplexing to take advantage of multiple CPUs in the computer platform. Multiple threads (often one per physical processor) each watch the open connections (or a subset of the open connections) and perform a small amount of work on each connection.

##### Step 3: Processing Requests

##### Step 4: Mapping and Accessing Resources

Typically, a special folder in the web server filesystem is reserved for web content. This folder is called the document root, or docroot.

##### Step 5: Building Responses

Once the web server has identified the resource, it performs the action described in the request method and returns the response message. The response message contains a response status code, response headers, and a response body if one was generated.

If the transaction generated a response body, the content is sent back with the
response message. If there was a body, the response message usually contains:

- A Content-Type header, describing the MIME type of the response body ([Common MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types))
- A Content-Length header, describing the size of the response body
- The actual message body content

###### Redirection

Web servers sometimes return redirection responses instead of success messages. A web server can redirect the browser to go elsewhere to perform the request. A redirection response is indicated by a 3XX return code. The Location response header contains a URI for the new or preferred location of the content.

Redirects are useful for:

- Permanently moved resources
- Temporarily moved resources
- URL augmentation

URL augmentation - servers often use redirects to rewrite URLs, often to embed context. When the request arrives, the server generates a new URL containing embedded state information and redirects the user to this new URL. * The client follows the redirect, reissuing the request, but now including the full, state-augmented URL

- Load balancing
- Server affinity
- Canonicalizing directory names

##### Step 6: Sending Responses

##### Step 7: Logging

## Proxies

Proxies sit between clients and servers and act as “middlemen,” shuffling HTTP messages back and forth between the parties.

### Proxies Versus Gateways

Strictly speaking, proxies connect two or more applications that speak the same protocol, while gateways hook up two or more parties that speak different protocols. A gateway acts as a “protocol converter,” allowing a client to complete a transaction with a server, even when the client and server speak different protocols.

### Why Use Proxies?

- Child filter
- Document access controller
- Security firewall
- Web cache
- Surrogate
- Content router
- Transcoder
- Anonymizer
  - The user’s computer and OS type is removed from the User-Agent header.
  - The From header is removed to protect the user’s email address.
  - The Referer header is removed to obscure other sites the user has visited.
  - The Cookie headers are removed to eliminate profiling and identity data.

### Proxy Hierarchies

Proxies can be cascaded in chains called proxy hierarchies. In a proxy hierarchy, messages are passed from proxy to proxy until they eventually reach the origin server
(and then are passed back through the proxies to the client).

### How Proxies Get Traffic

- Modify the client
- Modify the network
- Modify the DNS namespace
- Modify the web server

When a client sends a request to a web server, the request line contains only a partial URI (without a scheme, host, or port).
When a client sends a request to a proxy, however, the request line contains the full URI.

### The Via Header

Each time a message goes through another node, the intermediate node must be added to the end of the Via list.
The Via header field contains a comma-separated list of waypoints. Each waypoint represents an individual proxy server or gateway hop and contains information about
the protocol and address of that intermediate node.

> Via = 1.1 cache.joes-hardware.com, 1.1 proxy.irenes-isp.net

Note that each Via waypoint contains up to four components: an optional protocol name (defaults to HTTP), a required protocol version, a required node name, and an
optional descriptive comment.

### The TRACE Method

HTTP/1.1’s TRACE method lets you trace a request message through a chain of proxies, observing what proxies the message passes through and how each proxy modifies the request message. The final recipient is either the origin server or the first proxy or gateway to receive a Max-Forwards value of zero (0) in the request.

You can use the Max-Forwards header to limit the number of proxy hops for TRACE and OPTIONS requests, which is useful for testing a chain of proxies forwarding messages in an infinite loop or for checking the effects of particular proxy servers in the middle of a chain. Max-Forwards also limits the forwarding of **OPTIONS** messages.

### The HTTP OPTIONS

Clients can use OPTIONS to determine a server’s capabilities before interacting with the server, making it easier to interoperate with proxies and servers of different feature levels.

## Caching
