# HTTP

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
