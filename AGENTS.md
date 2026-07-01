# AGENTS

## Cursor Cloud specific instructions

This repository is a **Jekyll 3.9.2 static site** (a personal homepage that publishes a
collection of Chinese novels under the `_novels/` collection). It is pure Ruby/Jekyll —
there is no Node app, no database, no backend service, and no automated test suite.

### Services
There is exactly one thing to run: the Jekyll dev server.

- Build (one-off): `bundle exec jekyll build`
- Run dev server (with live regeneration): `bundle exec jekyll serve --host 0.0.0.0 --port 4000`
  - The homepage (`/`) is intentionally not a page; content lives at collection paths such as
    `http://localhost:4000/lp/toc/`, `http://localhost:4000/lp/1/`, and `http://localhost:4000/dp/1/`.
  - `/dp/1/` legitimately renders the literal text `Pending...` — that is site content, not an error.
- There is no lint step and no test suite in this repo. Use `bundle exec jekyll build`
  as the "does it compile" check.

### Ruby 3.2 compatibility notes (non-obvious)
The VM ships Ruby 3.2, which is newer than what this project originally targeted. Two
compatibility fixes are baked into the `Gemfile`/`Gemfile.lock` and are required for it to
run on Ruby 3.x:
- `webrick` is added explicitly — it was removed from Ruby's stdlib in 3.0 but Jekyll 3.x's
  `jekyll serve` still `require`s it. Without it, `jekyll serve` crashes with
  `cannot load such file -- webrick`.
- `liquid` is pinned to `4.0.4` (up from `4.0.3`) — `4.0.3` calls `Object#tainted?`, which was
  removed in Ruby 3.2, causing `jekyll build` to fail with `undefined method 'tainted?'`.

### Gem location (non-obvious)
Gems are installed to `/home/ubuntu/.jekyll-bundle` via a global Bundler config
(`~/.bundle/config`, `BUNDLE_PATH`). This is deliberate: installing into the repo (e.g.
`vendor/bundle`) makes Jekyll try to build the gems' own template files and fail, because
`_config.yml` does not exclude `vendor/`. Keep gems outside the source tree. The update
script (`bundle install`) relies on this global config.
