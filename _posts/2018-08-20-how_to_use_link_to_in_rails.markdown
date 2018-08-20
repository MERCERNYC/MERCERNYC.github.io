---
layout: post
title:      "How to use link_to in Rails"
date:       2018-08-20 16:38:11 +0000
permalink:  how_to_use_link_to_in_rails
---


After finishing my project Ruby on Rails.  I thought would me nice to refresh on form_for subject with  [Ruby on Rails API](http://api.rubyonrails.org/v5.1/classes/ActionView/Helpers/FormHelper.html). 

I had hard to grasp all the magic Rails provides while working on my project. You can easily  to get lost while working with routes and forms. Throughout my project, I used the form helpers. They are designed to make working with resources much easier compared to using vanilla HTML and kept my views clean.


If you are creating a sign up page in your project like I did, you must know that the  heart of the signup page  to create a user is a form for submitting the relevant signup information (first_name and last_name) for example. We can accomplish this in Rails with the form_for helper method, which takes in an Active Record object(f) and builds a form using the object’s attributes.

For example, to create a new user you typically set up a *new instance* of User in the UserController#new action, @user, and in the view template pass that object to form_for:

```
<%= form_for @user do |f| %>

  <%= f.label :first_name %>:
  <%= f.text_field :first_name %><br />

  <%= f.label :last_name %>:
  <%= f.text_field :last_name %><br />

  <%= f.submit %>
	
<% end %>
```

The presence of the *do* keyword indicates that form_for takes a block with one variable, which we’ve called f (for “form”). Form_for(@user) allows Rails to infer that the action of the form should be to POST to the URL /users.

The HTML generated for this block:

```
<form action="/user" class="new_user" id="new_user" method="post">
  <input name="authenticity_token" type="hidden" value="NrOp5bsjoLRuK8IW5+dQEYjKGUJDe7TQoZVvq95Wteg=" />
  <label for="user_first_name">First name</label>:
  <input id="user_first_name" name="user[first_name]" type="text" /><br />

  <label for="user_last_name">Last name</label>:
  <input id="user_last_name" name="user[last_name]" type="text" /><br />

  <input name="commit" type="submit" value="Create User" />
</form>
```

Remember that the key to creating a user is the special* name* attribute in each input. Rails uses de values entered by the new user and construct an initialization hash via de params.

Also, Rails knows to construct a form with the post method, which is the proper verb for creating a new object. You might be wondering how to delete a record with link_to.  Remember that calling the destroy action of a Restful controller requires a DELETE request. Most browsers don't support methods other than "GET" and "POST" when it comes to submitting forms. To go around this problem that can be easily achieved by passing the :method => :delete hash as an option to the link_to helper. Here is an example. 

```
 <td> <%= link_to topic_path(topic), method: :delete, data: {confirm: 'Are you sure?'} do %> </i> Delete
   <% end %></td>

    <a data-confirm="Are you sure?" rel="nofollow" data-method="delete" href="/topics/4"></a> 
```

You will probably want some sort of confirmation when removing objects to prevent accidental deletes. The easiest way to add that is with a simple javascript alert box that will ask the user to confirm his delete request.

Here is one more example when you want to use a form_for helper when a model is not present. Example SessionController to login a User. We have to give form_for slightly more information like the name of the resource and the corresponding URL.

```
<%= form_for(:session, url: login_path) do |f| %>
...
<% end %>
```


I really enjoyed learning Rails and I am still reviewing some of the main topics just to get a better understanding. I hope this blog helped you to understand a little bit more about form_for helper.  

Thanks. :)


