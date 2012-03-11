!SLIDE smbullets incremental
# I. Lack of Optional Groups
## Why?

- Allow applications to be distributed without manual editing of the `Gemfile`.
- This problem nearly always comes down to database drivers.

!SLIDE
# I. Lack of Optional Groups
## In more detail…

    bundle install --without=postgres,sqlite3

.notes You could use groups, but you have to provide a list of what you want to
exclude rather than include.

    @@@ ruby
    gem 'pg',       groups: 'postgres'
    gem 'sqlite3',  groups: 'sqlite3
    gem 'mysql',    groups: 'mysql'

!SLIDE
# I. Lack of Optional Groups
## Discussion and a Fix

proposal from **@FooBarWidget** and **@mislav**:
<https://github.com/carlhuda/bundler/issues/1636>

    bundle install --with=postgresql

In the `Gemfile`, groups would look like this:

    @@@ ruby
    group :postgres, optional: true do
      gem 'pg'
    end

.notes Allowing applications to be distributed without requiring manual editing
of the Gemfile. Mislav's suggestion for optional groups strikes me as sensible.
There's a GitHub issue for this, so I'll let the issue do the talking.
