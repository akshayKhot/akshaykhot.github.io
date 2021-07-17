---
layout: post
title: "CRUD: Resources in Rails"
tags: rails
---

It seems to me that Rails loves CRUD. CRUD stands for create read update and delete, a set of actions you can perform in an application that maps to the database operations. Things get very simple when you stick to conventions that Rails enforces upon you. 

Even though the [routing](/routing-in-rails) system doesn't force you to use standard names (you can map any action to any controller#method), it offers REST support using the `resources` method that gives you named routes pointing to CRUD-based actions. 

To enable support for a resource named `post`, add the following line to the `config/routes.rb` file. 

```ruby
resources :posts
```

This creates four named routes mapping to seven controller actions. 

| HTTP Verb | Path            | Controller#Action | Used For                                      |
| --------- | --------------- | ----------------- | --------------------------------------------- |
| GET       | /posts          | posts#index       | display a list of all posts                   |
| GET       | /posts/new      | posts#new         | displaly an HTML form for creating a new post |
| POST      | /posts          | posts#create      | create a new post                             |
| GET       | /posts/:id      | posts#show        | display a post with the given id              |
| GET       | /posts/:id/edit | posts#edit        | HTML form for editing the post                |
| PATCH/PUT | /posts/:id      | posts#update      | update a specific post                        |
| DELETE    | /posts/:id      | posts#destroy     | delete a specific post                        |

You can also create multiple resources in the same line.

```ruby
resources :photos, :books, :videos
```

Nested routes allow you to refer to a `comment` in the context of a `post`.

```ruby
resources :posts do
  resources :comments
end
```

However, Jamis Buck [recommends](http://weblog.jamisbuck.org/2007/2/5/nesting-resources) that you should not nest resources more than one level deep. The routes become confusing, and it's easy to make mistakes. 