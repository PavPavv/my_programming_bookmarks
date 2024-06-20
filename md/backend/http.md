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