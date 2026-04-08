# AGENTS.md

## Cursor Cloud specific instructions

This is a **Jekyll static site** for [markussens.se](http://markussens.se/) (Markussens Studiefond — a Swedish scholarship foundation). It is hosted on GitHub Pages from the `gh-pages` branch.

### Tech stack

- **Ruby 3.4.2** (specified in `Gemfile`; `.ruby-version` says 2.7.2 but `Gemfile` takes precedence)
- **Jekyll 3.10** via the `github-pages` gem
- **Sass** (deprecated Ruby Sass) with Bourbon, Singularity, Breakpoint-sass libraries vendored in `_sass/`
- **Bundler** for Ruby dependency management

### Running the dev server

```sh
bundle exec jekyll serve --watch --host 0.0.0.0 --port 4000
```

The site will be at `http://localhost:4000/`. All three pages (Start, Presentation, Historik) should return HTTP 200.

### Building

```sh
bundle exec jekyll build
```

Output goes to `_site/`. Sass deprecation warnings about `call()` are expected and harmless.

### Validation / linting

```sh
bundle exec htmlproofer ./_site --disable-external
```

Known pre-existing failures (12 total): non-HTTPS links, protocol-relative jQuery URL, and obfuscated email addresses. These are in the existing codebase and not regressions.

### Gotchas

- Ruby is installed at `/usr/local/ruby-3.4.2/bin` — ensure this is on `PATH`.
- The `bower.json` / `.bowerrc` files exist but Sass dependencies are already vendored in `_sass/`; Bower is **not** needed.
- The `github-pages` gem pins Jekyll to 3.10 and many plugins to specific versions. Do not upgrade individual gems without checking compatibility.
