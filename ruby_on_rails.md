# Ruby on Rails



## Creating a Rails App

`rails new app_name` --api		





**How to Manually Change from Default DB**









## Installation Notes

https://gorails.com/setup/ubuntu/18.04

https://www.digitalocean.com/community/tutorials/how-to-set-up-ruby-on-rails-with-postgres

1. Install Ruby

   ```
   sudo apt install curl
   curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
   curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
   echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

   sudo apt-get update
   sudo apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn
   ```

   

2. Install RVM

   ```
   sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
   gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
   curl -sSL https://get.rvm.io | bash -s stable
   source ~/.rvm/scripts/rvm
   rvm install 2.7.0
   rvm use 2.7.0 --default
   ruby -v
   ```

   

3. Install Bundler

   `gem install bundler`

4. Initialize git repo

   ```
   git init
   git add README.md
   git commit -m "first commit"
   git remote add origin https://github.com/username/repo_name.git
   git push -u origin master
   ```

5. Configure Git

   ```
   git config --global color.ui true
   git config --global user.name "YOUR NAME"
   git config --global user.email "YOUR@EMAIL.com"
   ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"
   ```

6. Add ssh key to your Github account

   `cat ~/.ssh/id_rsa.pub`

   `ssh -T git@github.com`   # <-- to verify

7. Install Rails

   `gem install rails -v 6.0.2.1`

8. Install and Set up Postgresql

   `sudo apt install postgresql libpq-dev`

   ```
   sudo -u postgres createuser USERNAME -s
   sudo -u postgres psql
   postgres=# \password USERNAME
   postgres=# \q
   (postgres=# \?)     <-- help command
   ```

9. Install Yarn v. 1.0+ and nodejs v.? (need to upgrade in Ubuntu 18.04); then run `rails webpacker:install`

10. Initialize new Rails project using PSQL

   `rails new project_name -d postgresql`

   `rails -v`	# <-- verify everything's installed correctly

   `bundle install`   # <-- installs all required gems

   `rails server`	# <-- starts app server

11. Create the database

    `rake db:create`

12. Run the Rails app server

    `rails server` or `rails s`



## Development

https://www.youtube.com/watch?v=pPy0GQJLZUM&t=514s

1. Generate a Controller (MV**C**)

   Controller is used to look at URL and decide what controller method to load, talk to model and view.

   Model deals with data storage (database, API)

   Views are used for UI (templates, browser view)

   App folder is most important, contains controllers, models, views subfolders;

   ```bash
   rails g controller Posts`
   # generates a controller named 'Posts'
   ```

2. Create an `index.html.erb` file in `app/views/posts/` folder

3. Create a route to this new index file, i.e., set this view as home view:

   ```
   # goes in /config/routes.rb
   root 'posts#index'

   ```

4. Create a `Pages` controller for static About or Terms pages

   ```
   $ rails g controller Pages

   # Then, go into /app/controllers/pages_controller.rb and add a method:

   class PagesController < Application Controller
     def about
     
     end
   end

   # Next, add an about.html.erb file to the /app/views/pages folder

   ```

5. Add a route to the new about page

   ```
   # go back into /config/routes.rb and add the following get request:
   get 'about' => 'pages#about'
   ```

6. Add a variable to About page and method

   ```
   # pages_controller.rb
   def about
     @title = 'About Us';
   end

   # about.html.erb
   <h1><%= @title %></h1>
   ```

7. Allow for creating many more views and methods (show, new, edit, destroy, etc.) automatically

   ```
   # routes.rb
   resources :posts

   # cli
   $ rake routes   # show all routes for app
   ```

   

   


------

## Rails Project Folder Structure



File/Directory 	Purpose
app/ 				Core application (app) code, including models, views, controllers, and helpers
app/assets 	 Applications assets such as Cascading Style Sheets (CSS) and images
bin/ 	 			Binary executable files
config/ 		    Application configuration
db/ 				  Database files
doc/ 				 Documentation for the application
lib/ 				    Library modules
log/ 				   Application log files
public/ 	  		Data accessible to the public (e.g., via web browsers), such as error pages
bin/rails 			 A program for generating code, opening console sessions, or starting a local server
test/ 					Application tests
tmp/ 					Temporary files
README.md 		A brief description of the application
Gemfile 				Gem requirements for this app
Gemfile.lock 		A list of gems used to ensure that all copies of the app use the same gem versions
config.ru 			  A configuration file for Rack middleware
.gitignore 			 Patterns for files that should be ignored by Git



