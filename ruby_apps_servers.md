# Ruby Applications, Application Servers and Web Servers



**TCPSocket**	class provided by Ruby's standard library which allows easier utilization of socket API

**API**	Application Programming Interface; a collection of programs that an application can use to access other components of the operating system

The Internet Protocol (IP) Suite, i.e., TCP/IP stack, includes TCP (transmission control protocol) and a TCP socket (IP + port) is what is used to communicate over the web in web app development.

The IP Suite includes many protocols which can be divided into the following ilayers:

1. Network Interface Layer ("Link" Layer)
2. Internet Layer
3. Transport Layer
4. Application Layer

TCP is mapped to Transport Layer, which specifies how info. is transmitted reliably from one network device to another.  The location of the remote device is specified by an IP address, a hierarchical addressing scheme which locates it across the internet.  The location within the sending device (the app) which sends the data is specified by port.  



## Request/Response Cycle (Ruby without a web server)

Here's how a Ruby applicatoin would have to respond to a client HTTP request if it had to drectly interact with the socket API.

- App uses socket API of OS via Ruby's TCPSocket class to open a passive connection, notifying OS that app is ready to receive connections through a particular port; it's ready to receive an HTTP request
- An HTTP request is received as one long string, which is parsed for header and body contents (request path, HTTP method, etc.)
- App performs actions specified in its code, including anything involving the parsed input from the client in its request, and returns an HTTP-compliant response (status, headers, body, properly formatted as string data)

Problems with this approach:

- app won't be able to handle multiple requests at once, so problems akin to head-of-line blocking, but as one slow client blocking others, may arise
- as HTTP requests grow in complexity, it will take more and more application logic to parse the request successfully

The solution is to implement all of this functionality either within the application code or separate the HTTP-related functionalities into a separate library or framework.  The latter option makes more sense in terms of re-usability.  

Even better is to use an already-existing application that handles sockets and HTTP-related features.  In this case, instead of opening a TCP connection directly between the app and the socket, we let a pre-built  app make use of the socket API of the OS.  The pre-built app would interface with the socket API and therefore be receiving HTTP requests from the client.  It would pass HTTP requests to our application, handle multiple requests at once and even provide other features like killing connections that take too long and serving static files without calling the application itself so that the application truly only needs to dedicate itself to producing the dynamic content needed and making server-side changes in response to forwarded HTTP requests.

 















