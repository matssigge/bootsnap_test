# README

This is a simple rails project which illustrates a weird crash. The project was created using the following steps:
* Running MRI 2.5.3, Rails 5.2.2
* `gem install rails` (5.2.2 is current)
* `rails new bootsnap_test -T`  
* Add rspec-rails gem to gemfile
* `rails g rspec:install`
* `rails g controller Home`
* Add the following (unreachable) code in HomeController
```ruby
    if false
      a(b: 1)
    end
```

* Now, when simply running `rspec` from the command line, I get a segfault, in what appears to be bootsnap/compile_cache/iseq.rb.
* If I remove the line `require 'bootsnap/setup'` from boot.rb, it works fine.
* If I remove the unreachable code, it works. 
* If I remove the keyword parameter from the `a(b: 1)` call, or replace it with a positional parameter, it works.
* If I switch to Ruby 2.4.5, it works.
* It does *not* fail on `rails server`, only `rspec`

I'm running a Mac, on macOS Mojave, 10.14.1. 
