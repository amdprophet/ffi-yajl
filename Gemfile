source "https://rubygems.org"

gemspec name: "ffi-yajl"

platforms :rbx do
  gem "rubysl", "~> 2.0"
end

group :development do
  # for testing loading concurrently with yajl-ruby, not on jruby
  # gem 'yajl-ruby', platforms: [ :ruby, :mswin, :mingw ]
  gem "github_changelog_generator"
end

group :development_extras do
  gem "chefstyle"
end

instance_eval(ENV["GEMFILE_MOD"]) if ENV["GEMFILE_MOD"]

# If you want to load debugging tools into the bundle exec sandbox,
# add these additional dependencies into Gemfile.local
eval_gemfile(__FILE__ + ".local") if File.exist?(__FILE__ + ".local")
