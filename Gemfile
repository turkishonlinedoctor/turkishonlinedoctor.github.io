source "https://rubygems.org"

gem "jekyll", "~> 4.3"

group :jekyll_plugins do
  gem "jekyll-polyglot", "~> 1.8"   # bilingual TR/EN routing
end

# Local dev server (Ruby 3+ removed webrick from the standard library)
gem "webrick", "~> 1.9"

# Windows and JRuby do not include timezone data
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.2.0", platforms: [:mingw, :x64_mingw, :mswin]
