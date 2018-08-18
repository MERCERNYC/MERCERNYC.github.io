---
layout: post
title:      "Flatiron School Tracker -Rails App Project"
date:       2018-08-18 19:12:45 +0000
permalink:  flatiron_school_tracker_-rails_app_project
---

The Flatiron School Tracker App was built using Ruby on Rails framework and no scaffolding was used to build this project. This app was created with an intention to help Flatiron students to track their coursework and organize topics by timeline to get stuff done along their learning journey with Flatiron School.

My app is pretty simple so I created my own authentication and authorization methods without using gems like Devise and Pundit which could add a lot to my simple app. In order to make the registration process easier, I have included a third party log in with a single provider Github. Make sure your email is not private on your github account or the login won't work. After logged in, the student can add topics and subjects related to the topic they are working on related to their curriculum.

```
def create
    #Log in with OmniAuth path
    if auth
      @student = Student.find_or_create_by(uid: auth['uid']) do |u|
      u.name = auth['info']['name']
      u.email = auth['info']['email']
      u.password = SecureRandom.hex
    end

    session[:student_id] = @student.id
    redirect_to @student

    else
    #normal login
    @student = Student.find_by(email: params[:session][:email])
    if @student && @student.authenticate(params[:session][:password])
    #log the user in and redirect to the user's create topic else give invalid login and require login
    session[:student_id] = @student.id
    flash[:success] = "Sucessfully logged in!"
    redirect_to @student
    else
    flash.now[:danger] = 'Invalid email/password combination'
    render :new
    end
   end
  end
```

After adding topics, the student is taken to the show page, which lets the student update, check topics with most subjects. Only current users can see topics and subjects displayed on the page.

Here are the steps I used to create my project application.

**1- Creating the Application**

To create files with Rails just type on the terminal:

$ rails new app_name

**2- Install the Required Gems**

By default Rails applications manage gem dependencies with Bundler. I added the gems below to my gemfile.

gem ‘omniauth’
gem ‘omniauth-github’
gem ‘dotenv-rails’
gem ‘pry’
gem ‘bycrypt’

Run bundle:

$ bundle_install

**3-Create the Database**

Example of a table to create students table.

```
class CreateStudents < ActiveRecord::Migration[5.2]
  def change
    create_table :students do |t|
      t.string :name
      t.string :email
      t.string :password_digest
      t.timestamps
    end
  end
end
```


Use a rake command to run the migration:

$ rake db:create

**4- Create Models**

Here is an example of my app/models/student.rb file. I have added validations and to secure password, I included the gem bcrypt in my gemfile .

The has_secure_password adds methods to authenticate against a BCrypt password. This mechanism requires you to have a password_digest attribute. This is create to secure your app if you are not using gems to secure your app.


These validations will ensure that students have a name, email, and password and that the email is unique to the student. If you type the below on your terminal you can see how the validation works.

```
student = Student.new

When password is blank.

student.valid? # => false
```

**5- Create Views**

Remember that view directly interact with the user. This is where I put all the code that makes my app look nice, and how my user sees and interacts with it . Here is an example of the topics view folders.


**6- Create Controller**

It’s the brains of the application, and ties together the model and the view. Here is where all the actions code goes. I used flash provided by Rails which provides my students (user) with useful information on the status of their request.


Once my MVC was ready and working properly. I started playing around and added CSS and Bootstrap to make the app look nice and colorful.

**
Here is a checklist :**

**Model:** Where I defined association between my models which makes common operations simpler in the code.

```
class Student < ApplicationRecord
     has_many :topics
     has_many :subjects, through: :topics
end

class Topic < ApplicationRecord
     belongs_to :student
     has_many :subjects
end

```

**View:** Where my users interacts with my app. I used partials to simplify my views and to keep it  dry. Partials are  great tool for cleaning up layouts.


Finally, the **Controller** where I defined how a user adds a topic. The Controller connects the View’s create button to the Model, so that when the user you click “Create Topic,” the Model adds a new topic.

```
def index
    #if not logged_in you cant see topics
     if logged_in?
      @topics = current_user.topics
    else
      flash[:danger] = "Please sign up or login to see topics."
      redirect_to login_path
    end
  end
```

To build everything from scratch without the help of crazy gems is definitely a challenge, but I learned a lot throughout the process . I hope this blog helps you with your project.  :)


For more code details please check my project by visiting my github!

Thanks. :)
