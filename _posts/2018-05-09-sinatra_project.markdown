---
layout: post
title:      "Sinatra Project"
date:       2018-05-09 16:34:20 +0000
permalink:  sinatra_project
---



I am so exited to see finally my Sinatra Project working. Every concept I’ve learned so far like Ruby, ORMs, Sinatra, Active Record finally came together.

I built a functional and simple web app that works like a todo list called Planner. As a mom, I built this app with moms-to-be in mind where they can manage their personal day-to-day tasks. Also they have the ability to create, read, updated and delete them.

Building this app with Sinatra was great, because I could learn the basics of HTTP and routing. My goal is after learning some Rails and Javascript; I can make this app even more functional down the road. Here are some of the process I followed to create my web app with Sinatra.

**File structure**

I could’ve used bundler to generate my project folders, but I decided it was a good practice to create this project without the help of bundler. This helped me to understand better the structure of my project. Takes more time but it’s good practice!

**Gemfile**

Then, I uploaded all the the gems needed to run my application.

**APP directory**

Next, my app directory is where I spent most of the time coding and where added my MVC directories.

After my project structure was ready, I started to code from the bottom up starting with:

**Database => Models =>Controllers =>Views**

**DB-Migration**

I created two migrations to create the users and the tasks table.
* 
* Users- have username, email, and password, and have many tasks.
* 
* Tasks- have name, and belongs to a user.
* 
**Models**

There are two models in this project — the User and Task model that creates the User and Task class.

* Task(belongs_to :user) and User (has_many :tasks)
* 
**Views**

Task and User folders in this directory contain .erb files because it allow to include regular HTML tags and special .erb tags which contain Ruby code. I used a lot of the the substitution tag (<%=) and the scripting tag (<%) throughout my files. Here is an example of my tasks index.erb view.

```

<% @tasks.each do |task| %> 
 <h3><a href=”tasks/<%= task.id%>” class=”list-group-item”><%= task.name %></a></h3>
 <% end %>
```

**Controllers**

There are three controllers in this application — the ApplicationController inherit from ActiveRecord::Base , UserController and TaskController inherit from application controller.

```
class ApplicationController < Sinatra::Base
use Rack::Flash
configure do
 set :public_folder, ‘public’
 set :views, ‘app/views’
 enable :sessions
 set :session_secret, “password_security”
 end
get ‘/’ do
 erb :index
 end
```

```
helpers do
def logged_in?
 !!current_user
 end
def current_user
 @current_user ||= User.find_by(:id => session[:user_id]) if session[:user_id]
 end
end
 end
```

**Config.ru**

The main purpose of this file is to run the app and is necessary when building Rack-based applications like Sinatra. I required my environment and my controllers. Added MethodOverride Sinatra middleware in order to use Patch, Put, and Delete requests.

```
require_relative ‘./config/environment’
use Rack::MethodOverride
use UsersController
use TasksController
run ApplicationController
```

**Config directory**

Sinatra doesn’t come with database. So I had to setup a database. The environment.rb file loads all the gems in my Gemfile, require all the app and set up the database as well.

```
ENV[‘SINATRA_ENV’] ||= “development”
require ‘bundler/setup’
Bundler.require(:default, ENV[‘SINATRA_ENV’])
ActiveRecord::Base.establish_connection(
 :adapter => “sqlite3”,
 :database => “db/#{ENV[‘SINATRA_ENV’]}.sqlite”)
require_all ‘app’
```

**Rakefile**

I created and use a Rakefile to run ActiveRecord migrations.

```
require_relative ‘./config/environment’ # Download environment
require ‘sinatra/activerecord/rake’#quickly make files and set up automated tasks
task :console do
 Pry.start
end
```

**Authentication**

To keep my app safe the users can sign up and log in and this was possible by enabling session to persist information across the HTTP requests and keep our session data.

```
post ‘/signup’ do
 @user = User.new(params)
 if @user.save
 session[:user_id] = @user.id
 redirect to “/tasks”
 #validations passed
 else
 erb :’users/signup’
 #validations failed
 end
 end
```
**Validation**

I added some validation to my user so a new record in the database cannot be created, edited or saved unless it passes the validations. To define a validation, I specified it on the model/class:

```
class User < ActiveRecord::Base
 has_secure_password
 has_many :tasks
 validates :username, :email, :password, presence: true
 validates :email, uniqueness: true
end
```

In the end, I am very happy to see that Planner my web app works quite nicely and meet all the requirements for my Sinatra Project. I hope you learned some basics of Sinatra with my blog. Thanks for reading my article! You can see all the code for this project on GitHub repo.
