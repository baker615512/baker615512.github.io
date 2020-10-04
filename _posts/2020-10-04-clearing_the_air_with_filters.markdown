---
layout: post
title:      "Clearing the Air with Filters"
date:       2020-10-04 19:53:27 +0000
permalink:  clearing_the_air_with_filters
---


## What's That Smell?

One of the coolest features I discovered in Rails is the Action Controller Filter.  Almost every app and website require you to be logged in to navigate the site.  When I created an app for the Sinatra project, I allowed anyone to view an index page.  However, if you wanted to view or modify anything else, I required the user to be logged in.  I created a helped method in my Application Controller that would redirect the user to the home page where they could log in if they were not already. 

```
def redirect_if_not_logged_in
  if !logged_in?
    redirect '/'
  end
end
```

While this helper method was convenient, I had to put this method at the beginning of all my CRUD routes (Create, Read, Update, Destroy).  This was repetitive and stinky because everyone knows repeating yourself is one of the worst codesmells.

## Rails to the Rescue

We were introduced to Action Controller Filters in a lab, but it was so nice to use it in my Rails project. Once again, I created helper methods in my Application Controller as such:

```
private

def current_user
  @current_user ||= Gamer.find_by_id(session[:gamer_id])
end

def logged_in?
  !!current_user
end
```

By adding the before_action filter to the top of my controllers, I was able to ensure users would be logged in to interact with my website.

## But That's Not All!

One other snippet of code is often repeated in many apps.  For instance, if you have a Group model, you will need this code in most controller actions:

```
@group = Group.find_by_id(params[:id])
```

We typically tuck that away in a private method at the bottom of the controller and name it set_group.  In fact, I found that I had this code at the beginning of my Show, Update, Edit, and Destroy actions within my controller.  With the help of the before_action filter, I was able to remove even more repetitive code with this one line:

```
before_action :set_group, only: [:show, :edit, :update, :destroy]
```

Ahhh. So fresh and so clean! I can breathe much easier now.
