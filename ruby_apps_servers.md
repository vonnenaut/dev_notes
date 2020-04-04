# Ruby Applications, Application Servers and Web Servers

[Demystifying Ruby Applications, Ruby Application Servers, and Web Servers](https://medium.com/launch-school/demystifying-ruby-applications-ruby-application-servers-and-web-servers-c3d0fd415cb3)

http://blog.gauravchande.com/what-is-rack-in-ruby-rails

-   [Part 1](https://launchschool.com/blog/growing-your-own-web-framework-with-rack-part-1)
-   [Part 2](https://launchschool.com/blog/growing-your-own-web-framework-with-rack-part-2)
-   [Part 3](https://launchschool.com/blog/growing-your-own-web-framework-with-rack-part-3)
-   [Part 4](https://launchschool.com/blog/growing-your-own-web-framework-with-rack-part-4)



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

The application server is itself another application and it'll execute your application just like an object calls another object's method in Ruby.  The app server:

- contains code that allows it to parse HTTP information into Ruby data structures that make sense, for example, turning HTTP request headers into hashes.  

- contains code that allows it to interface with a standard web server via socket connections which utilize the socket API of the OS.  

- contains code that captures the return value of your application and transforms the return value into HTTP-formatted text.

  

The app server and web server communicate via a socket (either a TCP or Unix socket):

- Unix sockets replace a host with a file path, which is faster since network overhead is removed;

- this only works if the app server and web server are on the same machine

  

When the app server is ready to hand the parsed request to the Ruby app:

- it will call your Ruby app with a method, passing in the parsed request as an argument or series of arguments
- the Ruby app will execute and the application server will store the Ruby app's return value in a variable
- it will re-format this variable into an HTTP response that the web server will understand, then sending that formatted HTTP response back to the web server via a socket connection
- the web server then sends the HTTP response to the client



## Division of Labor

This architecture exemplifies the modular, separation-of-concerns based approach to development.  Thanks to application servers, our apps don't need to understand HTTP at all and don't need to return HTTP-compliant responses.  



**Web Server**	parsing, authenticating, concurreny management

**Application Server**	Parsing HTTP request into a data structure(e.g., headers --> hashes) to pass to a Ruby Application

**Ruby Application**	Executes actual application logic



**Client <--> Web Server <--> Application Server <--> Ruby Application**



An interface has at least 2 sides.  An app server is an interface between a web server and a Ruby application.  On the web server side, it's written to handle the type of info. web servers send and to successfully return the type of info web servers understand (HTTP text).

On the application side, it's written to call the application and to pass in certain arguments to the application.  Those arguments represent the HTTP request.  It's also written to capture the return value of calling that application, formatting that return-value into HTTP text and sending it back to the web server.

What arguments does the application server pass to the Ruby application?  **A developer needs to know, specifically, what method the server calls on the Ruby app, what arguments are passed to the Ruby app, the data type of the arguments, the order in which the arguments are passed in, how the application server locates the Ruby app so that it can call it, etc.**  A developer needs to know all of this to ensure that the application code responds to the right method, accepts the right arguments and returns the right values.

A problem can arise because there are many frameworks and application servers -- if all the servers use a different interface to call the Ruby app and all the frameworks construct Ruby apps that expect to be called with different methods and arguments, managing **compatibility issues** can become a big problem.

This scenario is perfect for introducing a protocol or set of conventions which would specify which method all application servers should use to call an application and which method all applications should respond to.  It would specify which values the application would return, once called, and therefore it would specify which values the application server could expect to be returned from the Ruby app, making it much easier to construct a valid HTTP response out of the values returned by the Ruby app.  It would also specify the argument(s) that should be passed into the app when called.  In short, it would specify a common language or interface that Ruby apps and application servers could use to communicate.

**Introducing Rack**

Such a protocol exists already -- Rack.

<img class="nq pm s t u jo ai jw" srcset="https://miro.medium.com/max/552/1*ZLDeP7B0Uu5BAluwXz3NRQ.png 276w, https://miro.medium.com/max/1046/1*ZLDeP7B0Uu5BAluwXz3NRQ.png 523w" sizes="523px" role="presentation" src="https://miro.medium.com/max/523/1*ZLDeP7B0Uu5BAluwXz3NRQ.png" width="523" height="383">

<img class="nq pm s t u jo ai jw" srcset="https://miro.medium.com/max/552/1*k7cbm7xNb31rNwTDnsWvgQ.png 276w, https://miro.medium.com/max/1046/1*k7cbm7xNb31rNwTDnsWvgQ.png 523w" sizes="523px" role="presentation" src="https://miro.medium.com/max/523/1*k7cbm7xNb31rNwTDnsWvgQ.png" width="523" height="383">

Application servers and Ruby web servers are synonymous.



**Further reading**

[Web Application Architecture — Principles, Protocols, and Practices 2nd Ed.](https://www.amazon.com/Web-Application-Architecture-Principles-Protocols/dp/047051860X/ref=sr_1_1?ie=UTF8&qid=1505141443&sr=8-1&keywords=web+application+architecture)

[What is Rack?](http://blog.gauravchande.com/what-is-rack-in-ruby-rails)

[Understanding Rack Middleware](https://codenoble.com/blog/understanding-rack-middleware/)

[Phusion Passenger Design and Architecture](https://www.phusionpassenger.com/documentation/Design and Architecture.html)

[Distinguishing Between Nginx and Thin](https://stackoverflow.com/questions/3677715/distinguishing-between-nginx-and-thin)

[Web servers and App servers](https://stackoverflow.com/questions/4113299/ruby-on-rails-server-options/4113570#4113570)

[What is Thin and Why do I need it?](https://serverfault.com/questions/605853/what-is-thin-and-why-do-i-need-it)



**Thin vs Nginx Difference:**

https://stackoverflow.com/questions/3677715/distinguishing-between-nginx-and-thin



# What is 'Rack' in Ruby/Rails?

**Rack is a specification** to standardize how web servers and applications talk to one another.  

**Web servers** send an env hash containing elements like 'REQEST_METHOD', 'PATH_INFO', 'HTTP_VERSION', etc.

**Apps** return an array containing exactly 3 elements: HTTP status code, a hash of HTTP headers and a body object (which must respond to each).



# Grow Your Own Web Framework With Rack Part 1

Covering:

- what rack is
- how to use it to handle incoming requests
- how to use templating techniques to return a response
- how to extract common code to plant the seeds for your very own web application development framework
- build a simple Rack application

## What is Rack?

a web server interface that provides a fluid API for creating web applications.  Rack-based popular frameworks include Sinatra and Ruby on Rails.  They're rack-based because they adhere to the Rack interface to easily communicate between the server and the client.   In some ways you can think of Rack as a protocol or specification (though it's slightly more than that.)

Rack gives developers a consistent interface when working with Rack-compatible servers, a way to abstract away the mundane work of connecting and communicating with the web-serving and content-generating tiers of Ruby web applications.



**Steps for Creating a Rackable Ruby Application**

1. Create a Gemfile.

   ```
   # Gemfile
   
   source "https://rubygems.org"
   
   gem 'rack', '~> 2.0.1'
   
   ```

   

2. Run `bundle install` to install dependencies from Gemfile.

3. Create a rackup configuration file in our project's root directory.

   ```
   # config.ru
   require_relative 'hello_world'
   
   run HelloWorld.new
   ```

4. Write your Ruby program, including the required call(env) method and returning a 3-element array containing the 3 required elements (status code (string), headers (hash) and response-body (responds to `each`).

5. Run the program with

   ```
   bundle exec rackup config.ru -p 9595
   ```

   



## What Makes a Rack Application?

Rack is a specification for connecting our application code to a web server and also our application to a client.  To this end, Rack has some very specific conventions in place.  Here's what you need to make your Ruby code into a Rack application:

1. Create a "rackup" file:  a configuration file specifying what to run and how.  '.ru' extension. 
2. The rack application used in the rackup file must be a Ruby object that responds to the method `call(env)`, which takes the environment variable for this application.

The call method always returns an array containing these 3 elements:

1. **Status code**, represented by a string or some other data type that responds to `to_i`,
2. **Headers** in the form of of key-value pairs inside a hash.  The key will be a header name and its value the value for that header.
3. **Response Body** is any object which can respond to an `each` method call.  An `Enumerable` or `StringIO` object would work, for example, or even a custom object with an `each` method.  The response can never be just a `String` by itself but it must `yield` a `String` value.



# Grow Your Own Web Framework With Rack Part 2







​	



















