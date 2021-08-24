---
layout: post
title: Caching in Rails
tags: rails
---

**What is Caching?** 

Caching is one of the most effective ways to boost an application's performance. It stores content generated during the request-response cycle to reuse it when responding to similar requests. 

Rails supports caching out of the box, and caching is enabled only in production. However, you can turn it on/off by running `rails dev:cache` command. You can access the cache by calling `Rails.cache`.

Rails provides three types of caching techniques: **page**, **action**, and **fragment** caching. Fragment caching is the default. 

1. Page Caching
   - Cache the generated page, so the web server (Apache or Nginx) can serve the request directly, without involving the entire Rails stack. 
   - Though it is fast, it's unsuitable for pages that need authentication. 
   - You also have to implement cache expiration. 
2. Action Caching
   -  Similar to page caching, except the incoming request hits the Rails stack.
   -  This allows Rails to run the before filters like authentication before serving the cached response. 
3. Fragment Caching
   -  Enabled by default, fragment caching is suitable for dynamic web applications, where different parts of the page need to be cached and expired separately. 
   -  It wraps a fragment of view logic in a cache block, to be served out of the cache store for future requests. 
   -  Consider the following code, which caches each product on a page. For the first request, Rails creates a new cache entry which is used for subsequent requests. The cache expires when the view fragment changes and/or the model is updated. 

```erb
<% @products.each do |product| %>
	<% cache product do %>
  	<%= render product %>
  <% end %>
<% end %>
```
**Russian Doll Caching**

You can nest cached fragments inside other cached fragments. If a single entry is updated inside a cached collection, Rails reuses all the other fragments when regenerating the outer fragment. 

**SQL Query Caching**

Allows you to cache the result set of a SQL query. If Rails sees the same query, it will use the cached result set, instead of executing the query against the database again. 

Rails creates query caches at the start of an action and destroys at the end of that specific action. Hence, the query caches are persisted only for the duration of the action. 

**Cache Stores**

You can set up your application's default cache store by setting the `config.cache_store` configuration option. 

```ruby
config.cache_store = :memory_store
```

Rails provides the following cache stores:

1. MemoryStore: keeps entries in memory in the same Ruby process. 
2. FileStore: uses file system to store the entries. You must specify the path to the directory where the cache files will be stored, when initializing the cache.
3. MemCacheStore: uses Memcached as a cache.  
4. RedisCacheStore: uses Redis as a cache. 

These were the basics of caching in Rails. I will add new posts as I learn more. 
