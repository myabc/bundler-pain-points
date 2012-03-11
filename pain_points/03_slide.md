!SLIDE
# II. Lack of Overridable Version Dependencies

Dependencies when a `Gemfile` is out of date.

    @@@ ruby
    gem 'sass-rails' do
      override 'railties', '4.0.0'
    end

<https://github.com/carlhuda/bundler/issues/1549>
