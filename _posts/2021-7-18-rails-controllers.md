---
layout: post
title: Rails Controllers
tags: rails
---

I took the lazy Sunday evening to catch up on my reading of the official Rails [guides](https://guides.rubyonrails.org/action_controller_overview.html) on Action Controller. I paired that with chapter 4 of Obie Fernandez's [The Rails 5 Way](https://learning.oreilly.com/library/view/the-rails-5/9780134657691/), which is all about working with Rails controllers. This post tries to summarize the essentials, providing a brief overview of Rails controllers. 

The controller is responsible for managing the control flow of the application. It acts as a middleman between the model and the view, making the model available to the view to display the data to the user. 

**Naming Convention**: Prefer the pluralized version, e.g. `PostsController` instead of `PostController`. This contrasts with the naming convention for the models, which are supposed to be singular, e.g. `Post`. 

In its basic form, a Rails controller is a Ruby class extending from `ApplicationController`, which itself extends from `ActionController:Base`. 

```ruby
class PostsController < ApplicationController
  def index
  end
end
```

Upon receiving a request, the routing mechanism determines which `controller#action` to use. Then Rails creates an instance of the controller and invokes that action method. For example, a request for `/posts/new` instructs Rails to create an instance of `PostsController` and call its `new` method. 

Primarily, the controller does two things, understand the incoming request to figure out what to do and produce the appropriate view in response.

There are two ways to send data to the server:

1. Query string parameters: `/search?query=admin`
2. POST data, submitted via a form. 

Both query string parameters and the POST data are available in the `params` hash in the controller. 

```ruby
class HomeController < ApplicationController
  
  def index
  end

  # Fetch the query string parameter
  # from the request URL: /home/search?query=admin
  def search
    @query = params[:query]   #admin
  end
end

```

When Rails renders a view, it uses the instance variables set by the controller. 

>  Q. How can a view, which is an instance of `ActionView::Base` access the instance variables of a controller, which is an `ActionController`? 
>
> A. Rails loops through the controller object's variables, and for each one, creates an instance variable for the view with the same name and value. 

**Action Callbacks**

Action callbacks enable controllers to run code before and after an action.  You can use them for authentication, caching, or logging. The callbacks are nothing but class methods that appear at the top of the controller class. The actual methods that these callbacks call should be made private or protected. 

```ruby
class HomeController < ApplicationController
  before_action :authenticate
  
  def index
  end
 
  private
  
  def authenticate
		# authentication code
  end
end
```

Action callbacks can access the `request` and `response` objects set by Rails, along with all the instance variables set by the actions. They can set any instance variables to be used by other actions.  

You can also limit action callbacks to specific actions using the `:only` or `:except` options. Both options accept a single action `only: :index` or an array of actions `except: [:foo, :bar]`.

