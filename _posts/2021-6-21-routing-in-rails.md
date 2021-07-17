---
layout: post
title: Routing in Rails
tags: rails ruby
---

Routing is an important component of the Ruby on Rails framework. Here are a few essential  routing concepts, compiled from Obie Fernandez's excellent book "[The Rails 5 Way](https://learning.oreilly.com/library/view/the-rails-5/9780134657691/)", as well as the official [Rails documentation](https://guides.rubyonrails.org/routing.html) on routing. 

Primarily, routing does two things:

1. Maps requests to controller action methods.
2. Enables the dynamic generation of URLs for you to use as arguments to methods like `link_to` and `redirect_to` to generate proper HTML links.

Routes are defined in `config/routes.rb` file, generated when you bootstrap a Rails app. 

```ruby
Rails.application.routes.draw do
  # get "URL pattern", to: "controller/action"
  # get "URL pattern" => "controller/action"
  get "products/:id" => "products#show"
end
```

Routes are checked in the order they are defined in the `routes.rb` file. The search ends as soon as a match is found. 

**Redirect routes**

```ruby
get "/foo", to: redirect("/bar")
```

**Root**

The root route specifies what should happen when someone navigates to the 'root' of your application. 

```ruby
root to: "welcome#index"
root to: "home#index"
```

**Named Routes**

When you name a route, two new methods get defined for use in your controllers and views.

- `name_url` : returns a URL string that will trigger the route
- `name_path` : returns the path part of the URL (relative URL) without the protocol and host. 

```ruby
get "help" => "help#show", as: "help"

# help_url : https://railsapp.com/help
# help_path : /help
```

Using named routes, you can simplify the following code:

```ruby
link_to "Auction of #{item.name}",
	controller: "items",
	action: "show",
	id: item.id
```

to something simple:

```ruby
link_to "Auction of #{item.name}", item_path(id: item.id)
```

This assumes you have a named route defined as follows:

```ruby
get "item/:id" => "items#show", as: "item"
```

**Scoped Routes**

Rails allows you to bundle together related routing rules using scoped routes. For example, you can replace the following routing code

```ruby
get "auctions/new" => "auctions#new"
get "auctions/edit/:id" => "auctions#edit"
post "auctions/pause/:id" => "auctions#pause"
```

with the following code that uses scoped routes.

```ruby
scope controller: :auctions do
  get "auctions/new" => :new
  get "auctions/edit/:id" => :edit
  post "auctions/pause/:id" => :pause
end
```

you can further dry up the above code by using the `:path` argument to scope.

```ruby
scope path: "/auctions", controller: :actions do
  get "new" => :new
  get "edit/:id" => :edit
  post "pause/:id" => :pause
end
```

Furthermore, the `scope` method can interpret a symbol (if it's the first argument) as a controller. So you could just say:

```ruby
scope :auctions, path: "/auctions" do
end
```

Finally, you can use the `controller` method instead of the `scope` method.

```ruby
controller :auctions do
end
```

**Resource Routing**

Quickly declare all the common routes for a resource. It generates the routes for` index`, `show`, `new`, `create`, `edit`, `update`, and `destroy` actions. For example, a single entry in the rouging file, such as:

```ruby
resource :photos
```

creates the following routes for your app, all mapping to the Photos controller. 

| HTTP Verb | Path             | Controller#Action | Used For                          |
| --------- | ---------------- | ----------------- | --------------------------------- |
| GET       | /photos          | photos#index      | display a list of all photos      |
| GET       | /photos/new      | photos#new        | HTML form for creating new photo  |
| POST      | /photos          | photos#create     | create a new photo                |
| GET       | /photos/:id      | photos#show       | display a photo with the given id |
| GET       | /photos/:id/edit | photos#edit       | HTML form for editing the photo   |
| PATCH/PUT | /photos/:id      | photos#update     | update a specific photo           |
| DELETE    | /photos/:id      | photos#destroy    | delete a specific photo           |

You can also create multiple resources in the same line.

```ruby
resources :photos, :books, :videos
```

