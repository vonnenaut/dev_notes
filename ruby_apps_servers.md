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

 Client requests first go through the pre-built web-facing application, taking incoming textual information and formatting it into HTTP text that's more user-friendly.  Our application sits behind the scenes, not having to worry about simultaneous requests, parsing HTTP requests, etc.  The pre-built application is called a web server (nginx, apache, etc.) and our app receives input from it instead of directly from the TCP socket.

Problem with this approach:

- the web server has no way to start our application directly
- the web server speaks HTTP and the application doesn't

One solution is to make web applications speak HTTP; The problem with this:

- the app alone would have to do a lot more than just parse an HTTP request sent from a web server, execute code based on the info. in that request and then return a properly-formatted HTTP response.  
- Communication would have to happen over a socket, meaning the application would have to implement socket communication.  
- To handle more than one request concurrently, the application will need to start multiple instances of itself (as apache does)  The application will need to implement a way to monitor for crashes and to handle those crashes

All of these functionalities are distinct from the business logic an application should contain and these features are general and necessary regardless of the application.  It makes sense to separate, therefore, to separate these responsibilities into something like an HTTP interface that translates HTTP requests, forwarded from the web server, into sensible arguments that are then passed to the application.  This interface can also translate the application's non-HTTP response into HTTP that is then passed back to the web server and, finally, to the client.  There exist many such interfaces, called application servers.

## Putting an Application Server Between the Web Server and Ruby App



















