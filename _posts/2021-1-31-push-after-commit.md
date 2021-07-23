---
layout: post
title: How to Automatically Push Code After Commit
tags: how-to
---

If you are a solo developer working on a project, and need to push your changes immediately after committing them to the repository, Visual Studio Code has a shortcut that will make your life easier. 

Open the settings (cmd + comma), and type 'Post commit'. You will see the **Git: Post Commit Command**. Now select **Push** from the dropdown. Now VS Code will automatically push your code to the remote repository whenever you commit your changes.

<div class="random centered">
  <a href="{{site.images}}/post_commit.jpg">
	  <img src="{{site.images}}/post_commit.jpg" alt="Post Commit Hook">
  </a>
</div>

I find this highly useful when adding a new post on this blog, which is a static site hosted by GitHub Pages. I will add a post in [Typora](https://typora.io/) (which is my favorite Markdown editor), and commit my changes in VS Code, and it will take care of the rest. 

When combined with the keyboard shortcut (cmd + Enter) VS Code provides to commit the changes, deploying site is matter of typing a message and pressing couple of keys.

Blogging has never been this simpler!