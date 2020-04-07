# Sinatra -- A Ruby web framework![img](https://da77jsbdz4r05.cloudfront.net/images/working_with_sinatra/server-zoom-sinatra.png)



Sinatra is a Rack-based web development framework. This means that it  comes with a lot of out of the box features that are meant to help make web development easier. It uses  Rack to connect to a web server, like WEBrick. On top of that, Sinatra  provides conventions for where to place your application code. It has built-in capabilities for routing, view templates, and many other  convenient features that you'd otherwise have to code up yourself.

But at the core, it's nothing more than some Ruby code connecting to a  TCP server, handling requests and sending back responses all in an  HTTP-compliant string format. Keep that in mind.



## How Routes Work

Sinatra provides a DSL for defining *routes*, and these routes are how a developer maps a URL pattern to some Ruby code. Take a look in `book_viewer.rb`:

```ruby
require "sinatra"
require "sinatra/reloader"

get "/" do
  File.read "public/template.html"
end
```

First we `require` Sinatra and `sinatra/reloader`, which causes the application to reload its files every time we load a page.

`get "/" do` is declaring a route that matches the URL `"/"`. When a user visits that path on the application, Sinatra will execute the body of the block. The value that is returned by the block is then sent to the user's browser.

In the example route, we're loading the contents of the file at "public/template.html" and sending it back to the browser. This file contains the HTML code that you currently see when viewing the application in a browser.

```
The ::read method is a class method of the IO class, and is available to File since it inherits from IO. Calling File.read opens the specified file and returns its contents as a string.

You don't need to know too much about the IO and File classes for the purposes of this course, but you may find it useful to briefly refer to the documentation for the IO::read and IO::readlines methods at certain points during this lesson.
```



## Rendering Templates









