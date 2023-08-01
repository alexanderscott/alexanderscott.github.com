source 'https://rubygems.org'
ruby '~> 2.7.4'

gem 'github-pages'

# gem "jekyll", ">=3.8.6"

gem "webrick"

gem "jekyll-analytics", "~> 0.1", git: 'https://github.com/hendrikschneider/jekyll-analytics', ref: '40e09570dea80e3a9ecb0ad796aad1c434ff067c'

# Official Plugins
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-redirect-from"
  gem "jekyll-seo-tag", "~> 2.6.1"
end

group :test do
  gem "nokogumbo"
  gem "html-proofer"
end

# gem "jekyll-theme-chirpy", "~> 6.1"

# group :test do
#   gem "html-proofer", "~> 3.18"
# end
#
# # Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# # and associated library.
# platforms :mingw, :x64_mingw, :mswin, :jruby do
#   gem "tzinfo", ">= 1", "< 3"
#   gem "tzinfo-data"
# end
#
# # Performance-booster for watching directories on Windows
# gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]
#
# # Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# # do not have a Java counterpart.
# gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
#
# # Lock jekyll-sass-converter to 2.x on Linux-musl
# if RUBY_PLATFORM =~ /linux-musl/
#   gem "jekyll-sass-converter", "~> 2.0"
# end
