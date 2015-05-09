# appium_thor [![Gem Version](https://badge.fury.io/rb/appium_thor.svg)](https://rubygems.org/gems/appium_thor)[![Dependency Status](https://gemnasium.com/appium/appium_thor.svg)](https://gemnasium.com/appium/appium_thor)


Appium Thor helpers for appium's gems (appium_lib, appium_capybara).

--

# Example configuration

```ruby
Appium::Thor::Config.set do
  gem_name     'appium_thor'
  github_owner 'appium'
  github_name  'appium_thor'
  version_file 'lib/appium_thor/version.rb'
  docs_block do
    run 'docs/helpers_docs.md', globs('/lib/appium_thor/helpers.rb')
  end
end

# Must use '::' otherwise Default will point to Thor::Sandbox::Default
# Debug by calling Thor::Base.subclass_files via Pry
#
# https://github.com/erikhuda/thor/issues/484
#
class ::Default < Thor
  desc 'spec', 'Run RSpec tests'
  def spec
    exec 'rspec spec'
  end
end
```

# Defaults

      Option | Default
          --:|:--
gem_name     | must be provided
github_owner | `appium`
github_name  | `#{gem_name}`
version_file | `lib/#{gem_name}/version.rb`
docs_block   | no docs are generated


--

# Available tasks

Note to see gem warnings, run `gem build your_gem_name.gemspec`

```
thor build          # Build a new gem
thor bump           # Bump the z version number and update the date.
thor bumpx          # Bump the x version number, set y & z to zero, update the date.
thor bumpy          # Bump the y version number, set z to zero, update the date.
thor byte           # Remove non-ascii bytes from all *.rb files in the current dir
thor docs           # Update docs
thor gem_install    # Install gem
thor gem_uninstall  # Uninstall gem
thor info           # prints config info for this gem
thor notes          # Update release notes
thor publish        # Build and release a new gem to rubygems.org
thor release        # Build and release a new gem to rubygems.org (same as publish)
```

--

# docs_block

The `docs_block` method runs within the `docs.rb` context. Here's a more complex example:

```ruby
common_globs  = '/lib/appium_lib/*.rb', '/lib/appium_lib/device/*.rb', '/lib/appium_lib/common/**/*.rb'
android_globs = common_globs + ['/lib/appium_lib/android/**/*.rb']
ios_globs     = common_globs + ['/lib/appium_lib/ios/**/*.rb']

run 'docs/android_docs.md', globs(android_globs)

run 'docs/ios_docs.md', globs(ios_globs)
```
