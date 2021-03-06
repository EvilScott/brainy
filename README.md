# Brainy - An Artificial Neural Network [![Build Status](https://travis-ci.org/EvilScott/brainy.svg?branch=master)](https://travis-ci.org/EvilScott/brainy)

Brainy is an [Artificial Neural Network (ANN)](https://en.wikipedia.org/wiki/Artificial_neural_network) using the 
[Backpropagation](https://en.wikipedia.org/wiki/Backpropagation) algorithm. It was originally created as part of 
the Neural NFL project [here](https://github.com/EvilScott/neuralnfl), but was broken out into a gem to be more reusable.

_NOTE_: As of v2.0 Brainy is _JRuby only_. This decision was made for performance reasons, as it can now leverage the fast linear algebra functionality
found in the [JBLAS](http://jblas.org/) Java library.

### Installation
Brainy is hosted on [RubyGems.org](https://rubygems.org/gems/brainy/) making installation easy.
```
$ gem install brainy
```

### Usage
From [examples/sin.rb](https://github.com/EvilScott/brainy/blob/master/examples/sin.rb):
```ruby
# Example using sin wave function
require 'brainy'
net = Brainy::Network.new(1, 3, 1, learning_rate: 1.0)

# training
4000.times do
  i = rand(0..(Math::PI/2))
  o = Math.sin(i)
  net.train!([i], [o])
end

# testing
mse = 1000.times.map do
  i = rand(0..(Math::PI/2))
  o = Math.sin(i)
  (o - net.evaluate([i]).first) ** 2
end.reduce(:+) / 1000

puts "your MSE: #{ mse.round(6) }" # smaller is better
```
