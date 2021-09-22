The first difference between lambdas and procs is that the return keyword means different things. In a lambda, **return** just returns from the lambda.

In a proc, return behaves differently. Rather than return from the proc, it returns from the scope where the proc itself was defined:

```ruby
def run_proc
  p = proc { return 10 }
  p.call
  20
end

def run_lambda
  p = lambda { return 10 }
  p.call
  20
end

result = run_proc
puts result		# 10

result = run_lambda
puts result		# 20
```

The second difference between procs and lambdas concerns the way they check their arguments. If the proc is a lambda, Ruby will check that the number of supplied arguments match the expected parameters. 

Generally speaking, lambdas are more intuitive than procs because they’re more similar to methods. They’re pretty strict about arity, and they simply exit when you call return. For this reason, many Rubyists use lambdas as a first choice, unless they need the specific features of procs.

*from: [Metaprogramming Ruby 2](https://learning.oreilly.com/library/view/metaprogramming-ruby-2/9781941222751/)*