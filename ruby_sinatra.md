# Sinatra -- A Ruby web framework

**Routes**	paths to resources based on request input

**Views**	a folder containing embedded Ruby files (`.erb`) which are rendered into HTML pages and served to the client

**layout.erb**	the default overarching layout template which stays the same across content and which contains a `<%= yield %>` `erb` tag to reference more-specific templates for individual pages; `layout.erb` is effectively a wrap-around template with general content which references, via yield, other, smaller templates for specialized content, making code more DRY.

a layout can be specified on a route like this:

```erb
get '/' do
  erb :index, layout: :post
end
```

Otherwise, if no layout is specified, Sinatra will look for the default layout, `layout.erb`.  This way, when you have content to a specific page, you just need to insert it via yield from its own `.erb` file in the `views/` folder, specifying it in the routes file.  Rather that repeating the elements that are the same, they are grouped into one `layout.erb` file.









# ![img](https://da77jsbdz4r05.cloudfront.net/images/working_with_sinatra/server-zoom-sinatra.png)



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

Let's transition from the app acting as a static file server into a more dynamic app which renders a template instead.

Templates or view templates are files that contain text that is converted into HTML before being sent to a user's browser in a response.  There are many templating languages with different ways to define what HTML to generate and how to embed dynamic values.

For example, you might want the <title> to be different on each page and so this would be a dynamic value defined in Ruby code and inserted into the template before it was sent to a user.

We'll use a templating language called `ERB` which stands for *embedded Ruby* and the fact that bits of Ruby code are embedded into another file.  `ERB` is also the default templating language in Ruby on Rails so knowledge gained here will carry over to projects that use that framework as well.

Here's an example of printing a dynamic value:

```erb
<h1><%= @title %></h1>
```

When the template is *rendered*, the value for `@title` will replace the ERB tags. If `@title == "Book Viewer"`, the rendered output of the template would be:

```html
<h1>Book Viewer</h1>
```

If you are having trouble with something not appearing in a template, always check to **make sure you have included the `=`**. This is a common mistake, since there is no error.







