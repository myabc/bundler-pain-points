!SLIDE smbullets incremental
# III. Declaring a Dependency more than once

# Why?

- a. test against multiple versions of a resource (for example, in CI)
- b. working against a git respository of a dependency (for example, you're using Engines)

.notes The Engines issue is my big motivation for trying to deal with this issue.

.notes Yes, there are actually four. But 3 and 4 could be considered the same
issue, even though the mitigation is slightly different.

!SLIDE
# III. Declaring a Dependency more than once
# Facilitates developing componentized systems

!SLIDE
`BUNDLE_GEMFILE`

Solutions is to employ multiple Gemfiles.

Set `BUNDLE_GEMFILE`.

Multiple `Gemfile`s, where you want to use different versions or tighten versions
that might have been defined in the `.gemspec`.

I've seen this solution used by Ripple, for example.

    @@@ ruby
    # Taken from:
    # https://github.com/seancribbs/ripple/blob/master/Gemfile.rails31

    gem 'activemodel', '~> 3.1.0'

    instance_eval File.read(File.expand_path('../Gemfile', __FILE__))

    @javascript solution for swapping out images

<https://gist.github.com/2016633>

    @@@ruby
    task :local_gemfile do
      gemfile = File.read('Gemfile')
      gemfile.gsub!(/git: ["']git@github\.com:payango\/([\w-]+)\.git["']/, 'path: \'../\1\'')
      File.open('Gemfile.local', 'w') { |file| file.write(gemfile) }
    end



!SLIDE
# III. Declaring a Dependency more than once
## Working against another git repository

.notes My Bash skills leave much to be desired.

    BUNDLE_GEMFILE=Gemfile.local bundle install

    @@@ ruby
    local_gemfile_on
    local_gemfile_off


    bundle update payango_helpers
    rake bundle:local_gemfile
    rake bundle:local_install


.notes Still to be fixed: autoloading of Engines, libraries.
Upgrade `BUNDLE_GEMFILE`.



