---
layout: post
title: Exploring Rake
tags: ruby rake
---

Rake is a task runner written in Ruby. It performs repetitive tasks, such as

1. Making database backup
2. Running tests
3. Watch for file changes and compile the changed files

In the words of late Jim Weirich, the creator of rake, 

> The essence of rake is to take a task and break it down into its component pieces to specify what needs to be done to do the bigger task you are trying to do.  

**Usage**

Put the following code in a `Rakefile`.

```ruby
desc "Compile Code"
task :compile do
  puts "Compiling the code."
end
```

Run the task by running the following command

```bash
> rake compile
```

The description is listed when you run `rake --task` to see all available tasks.

```bash
> rake --task

rake compile         # Compile code
```

**Dependent Tasks**

```ruby
task :interpret do
  puts "Interpreting the code"
end

task compile: "interpret" do
  puts "Compiling the code"
end
```

```bash
> rake compile
Interpreting the code
Compiling the code
```

To run multiple dependent tasks, provide their names as an array of symbols. 

```ruby
task compile: %i(clean sanitize interpret) do
  puts "Compiling the code"
end
```

**Providing Defaults**

Use the `default` task to specify all tasks to run when you run the  `rake` command, without any arguments.

```ruby
task default: %i[clean sanitize]

desc "Cleaning the code"
task :clean do
  puts "Cleaning the code"
end

desc "Sanitizing the code"
task :sanitize do
  puts "Sanitizing the code"
end
```

 ```shell
 > rake
 Cleaning the code
 Sanitizing the code
 ```

**Scope**

You can scope tasks with similar names under different namespaces. 

```ruby
task :backup do
  puts "Database backup"
end

namespace :file do
  task :backup do
    puts "File backup"
  end
end
```

```bash
rake backup
> Database backup

rake file:backup
> File backup
```

**Access Environment Variables**

```ruby
task :show_state do
  puts "State = #{ENV["STATE"]}"
end
```

```bash
> export STATE=paused

> rake show_state
State = paused
```

Rake also allows you to pass the environment variable for the particular command. It's only valid for that specific command, though. 

```bash
> rake show_state STATE=running
State = running

> rake show_state          
State = paused
```

**What's Possible?**

First, it's all Ruby code. You can do anything in rake that you can do in Ruby. There's no limit. 

```ruby
task :sum do
  result = 0
  (1..10).each do |n|
    result += n
  end
  puts result
end
```

However, rake is perfect for file manipulation. It includes the `FileUtils` standard library. So you can use all standard file manipulation commands. 

```ruby
desc "Taking a backup of the Rakefile"
task :backup do
  mkdir_p "data/backup"
  cp "Rakefile", "data/backup/Rakefile"
end
```

You can also run shell commands. This is especially handy when you want to run `git add`, `git commit`, and `git push` commands. 

```ruby
desc "git add, commit, and push"
task :track do
  sh "git add ."
  sh "git commit -m '#{ENV['m']}'"
  sh "git push origin main"
end
```

Run the command as follows:

```bash
>  rake track m="initialize project"
```

Finally, rake can run Ruby scripts, too. 

```ruby
task :run do
  ruby "greet.rb"
end
```

**Summary** 

Rake is a task runner Jim Weirich wrote in Ruby. It allows you to specify dependent tasks to run them in order as well as automate repetitive tasks. You can leverage the power of shell and Ruby, which makes it very powerful. It's a tool that you should know, even if you are not a Ruby developer. 
