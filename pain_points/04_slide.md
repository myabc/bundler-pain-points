!SLIDE bullets incremental
# III. Declaring a Dependency more than once

## Why?

- test against multiple versions of a resource (for example, in CI) _(problem A)_
- facilitates developing componentised systems:
  (perhaps working against a git repository of a dependency, or an Engine in git)
  _(problem B)_

.notes Travis CI allows you to specify multiple Gemfiles in your .travis.yml.
.notes The Engines issue is my big motivation for trying to deal with this issue.

!SLIDE
# III. Declaring a Dependency more than once
## Fix

Concept is EASY: Use multiple Gemfiles

!SLIDE
# III. Declaring a Dependency more than once
## Fix for problem A

Multiple `Gemfile`s, where you want to use different versions or tighten versions
that might have been defined in the `.gemspec`.

!SLIDE code
I've seen this solution used by Ripple, for example.

    @@@ ruby
    # Taken from:
    # https://github.com/seancribbs/ripple/blob/master/Gemfile.rails31

    gem 'activemodel', '~> 3.1.0'

    instance_eval File.read(File.expand_path('../Gemfile', __FILE__))

!SLIDE
# III. Declaring a Dependency more than once
## Fix for problem B

Set `BUNDLE_GEMFILE` and use a `Gemfile.local`


!SLIDE code
# Generate a Gemfile.local using Rake

    @@@ruby
    task :local_gemfile do
      gemfile = File.read('Gemfile')
      gemfile.gsub!(/git: ["']git@github\.com:payango\/([\w-]+)\.git["']/, 'path: \'../\1\'')
      File.open('Gemfile.local', 'w') { |file| file.write(gemfile) }
    end

<https://gist.github.com/2016633>

.notes A pain to by hand so use Rake.

!SLIDE
# III. Declaring a Dependency more than once
## Working against another git repository

.notes My Bash skills leave much to be desired.

    BUNDLE_GEMFILE=Gemfile.local bundle install

Of course you can wrap this in a script:

    local_gemfile_on
    local_gemfile_off

.notes Still to be fixed: autoloading of Engines, libraries. Upgrade `BUNDLE_GEMFILE`.
If you're using Rails 3.1, you may also have to update your `config/boot.rb`