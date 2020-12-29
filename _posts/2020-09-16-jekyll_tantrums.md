---
layout: post
title: Jekyll Tantrums
date: 2020-09-16
category: general
permalink: jekyll-tantrums
---

In the last few months, I had to switch laptops twice and get Jekyll
up and running on both of them. While the instructions on Jekyll
webpage get you started, they are not of much help in dealing with
the issues that you encounter while setting up Jekyll.

### Ruby tantrums 
Jekyll requires Ruby. It can be installed with the command:
```shell
sudo apt install ruby-full
```

This typically installs a version that is not the latest. But, it 
shouldn't be an issue as long as it is 2.5.0 or higher. So, as on
today, Ruby version is not an issue. 

To check the version number, run `ruby -v`. If you are lucky, you
will get the desired output. If you are not that lucky, as I was
today, you need to see where Ruby installed by running the command:
```shell
which ruby
```
Usually, the output of this command will be `\usr\bin\ruby`, and
sometimes, it can be `\usr\local\bin\ruby`. You can now get the
Ruby version by including the above path in the command:
```shell
/usr/bin/ruby -v #If Ruby is installed at \usr\bin
/usr/local/bin/ruby -v #If Ruby is installed at \usr\local\bib
``` 

You can also find the version number by looking at the Ruby binaries.

```shell
ls /usr/bin | grep ruby
```

In my case, I get `ruby` and `ruby2.5` as output. Running `ruby2.5 -v`
gives me Ruby's version number.

### `gem` tantrums
We install Jekyll by running the following command:
```shell
gem install jekyll
```

If this fails, which is usually the case in my experience, we again look at
the binaries.
```shell
ls /usr/bin | grep gem
```

This gives `gem` and `gem2.5`, and some other stuff. This output tells
us that we have to use `gem2.5` instead of `gem`. Now, install Jekyll and
bundler by running the following commands.
```ruby
gem2.5 install jekyll
gem2.5 install bundler
```

The following commands will complete the Jekyll set up process.
```ruby
sudo gem2.5 update --system
bundle update
```

Now, navigate to the root folder of your blog and serve it locally to 
ensure that things are fine.
```ruby
bundle exec jekyll serve
```

That's it!
