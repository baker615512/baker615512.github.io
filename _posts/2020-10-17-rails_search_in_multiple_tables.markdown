---
layout: post
title:      "Rails Search in Multiple Tables"
date:       2020-10-17 18:06:23 +0000
permalink:  rails_search_in_multiple_tables
---


During my Rails assessment, I was asked to create a seach bar on one of my index view pages. This didn't seem too hard until I tried to search from another table that has an association.

In my app, Gamers have many Gatherings and many Groups through Gatherings. Groups have the same relationships, and Gatherings is the join table that belongs to Gamers and Groups. When creating a gathering, you can select the day of the week and the game cafe where it will be hosted. The Gatherings index page displays 3 things:
1. the game title attribute of the group
2. the game cafe attribute of the gathering
3. the day of the week attribute of the gathering

It took a few minutes to create a search bar that would allow the gamer to search gatherings by the day of the week, but I was able to make that functional as this particular attribute is associated with the gathering.

But how could I search the Group table for the game title attribute???

After a few searches, I came across a StackOverflow post, the Ruby on Rails documentation, and this incredibly helpful video --- https://youtu.be/8mRnv9fi8iU

In my Gatherings model, I wrote this class method:

```
  def self.search(params)
    joins(:group).where('LOWER(day_of_week) LIKE :term OR LOWER(groups.game_title) LIKE :term', term: "%#{params}%")
  end
```

The actual search code is in my index view page for Gatherings:

```
<%= form_tag('/gatherings', method: 'get') do %>
    <%= label_tag(:q, "Search:") %>
    <%= text_field_tag(:q) %>
    <%= submit_tag("Search") %>
<% end %>
```

My Gatherings controller takes in the conditional params to tie it all together:

```
        if params[:q]
            @gatherings = @gatherings.search(params[:q])
        end
```

This challenge was fairly difficult for me, but it was an incredible feeling when I figured it out and learned this crucial piece of programming.
