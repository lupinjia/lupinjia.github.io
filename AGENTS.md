# Repository guide

## Stack and layout

- This is a Hugo **extended** static site built with HugoBlox modules; use Hugo `0.164.0` and Node `22` to match CI (`.github/workflows/publish.yaml`) and Netlify (`netlify.toml`).
- `content/` holds pages: use `content/blog/` for technical posts and `content/post/` for news/activity updates. Publications and projects live in `content/publication/` and `content/project/`.
- Site settings are in `config/_default/`; author profiles are in `data/authors/`. Custom templates are in `layouts/` and assets in `assets/` (both are mounted through `config/_default/module.yaml`).
- `layouts/blog/list.html` and `layouts/search/list.html` depend on Pagefind's generated `/pagefind/` assets.

## Build and verify

- There are no npm scripts or repository test, lint, formatter, or typecheck commands. Install the declared frontend tools with `npm ci`.
- Use `hugo server -D` for local preview; use `hugo --minify` for a focused production build.
- Generate the search index **after every production build**: `npx pagefind --site public`.
- For the closest Netlify build, run `npm ci && hugo --gc --minify -b "$URL" && npx pagefind --source public`. Deploy previews add `--buildFuture`.
- Run `hugo mod tidy` only when Hugo module metadata or dependencies change.

## Deployment and generated files

- Pushes to `main` deploy to GitHub Pages. CI builds with `hugo --minify --baseURL "<Pages base URL>/"`, then runs Pagefind; preserve that order.
- `config/_default/hugo.yaml` has a placeholder `baseURL`, so pass an explicit base URL when validating production links.
- Do not commit generated `public/`, `resources/`, `hugo_stats.json`, `.hugo_build.lock`, `node_modules/`, or `go.sum` (all are ignored).
- `publications.bib`, when present, is converted into `content/publication/` by the `import-publications` GitHub workflow.
