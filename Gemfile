source 'https://rubygems.org'

gem 'jekyll', '3.9.2'

# webrick is no longer part of the Ruby standard library as of Ruby 3.0,
# but Jekyll 3.x's built-in dev server (`jekyll serve`) still requires it.
gem 'webrick', '~> 1.8'

group :jekyll_plugins do
  # Only jekyll-sitemap is actually wired up (robots.txt links to sitemap.xml).
  gem 'jekyll-sitemap', '1.4.0'

  # Markdown engine (Jekyll defaults to kramdown with GFM input).
  gem 'kramdown', '2.3.2'
  gem 'kramdown-parser-gfm', '1.1.0'

  # Windows-only helpers (no-ops elsewhere).
  gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
  gem 'wdm', '>= 0.1.0' if Gem.win_platform?
end
