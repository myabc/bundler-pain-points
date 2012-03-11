!SLIDE
# II. Lack of Overridable Version Dependencies
## Why?

Overriding dependencies when a particular gem `gemspec` is out of date.

    @@@ ruby
    gem 'sass-rails' do
      override 'railties', '4.0.0'
    end

.notes Really annoying when latest version of Rails appears and there are
developers who haven't updated the plugins yet. You're prepared to take the risk
of testing the gem, but the only option is to fork the gem and add it as a git
dependency.

!SLIDE
# II. Lack of Overridable Version Dependencies
## Discussion and Fix

<https://github.com/carlhuda/bundler/issues/1549>

.notes There is an issue open for this, but this is not something the Bundler
developers currently want to add in. They prefer the fork and git hub dependency
workflow. I'd encourage you to +1 this issue!