# Repository guide

## Stack and layout

- This is a Hugo **extended** static site built with HugoBlox modules; use Hugo `0.164.0` and Node `22` to match CI (`.github/workflows/publish.yaml`) and Netlify (`netlify.toml`).
- `content/` holds pages: use `content/blog/` for technical posts and `content/post/` for news/activity updates. Publications and projects live in `content/publication/` and `content/projects/`; the projects section is `/projects/` (nav entry) and each card is `/projects/<slug>/`.
- Site settings are in `config/_default/`; author profiles are in `data/authors/`. Custom templates are in `layouts/` and assets in `assets/` (both are mounted through `config/_default/module.yaml`).
- `layouts/blog/list.html` and `layouts/search/list.html` depend on Pagefind's generated `/pagefind/` assets.
- Landing pages use `type: landing` + `sections[].block: collection`. A collection block silently defaults to `content.count: 5`; set `count: 0` to show every match. Its "See all" link appears only when `count` exceeds the limit and resolves to the section page, so keep the landing page's `count` and the target section `_index.md` in sync.
- `layouts/_partials/functions/build_links.html` is a **local full copy** of the HugoBlox `blox@v0.12.0` partial because upstream hardcodes `site.GetPage "project/<name>"` for publication→project links. Our copy looks in `projects/` first, then `project/`, and emits a build warning for unresolvable names. When bumping the blox module, re-copy the upstream file and re-apply that patch (marked `LOCAL OVERRIDE` in the file).
- A publication's `projects: [...]` entries must be the **folder names** under `content/projects/` (e.g. `RoboStack`), not the page titles — the lookup is path-based, so a title mismatch silently drops the link (now warned at build time).
- Every project page (and the section page) keeps an `aliases` entry for its old `/project/...` URL. `disableAliases` must stay `false` for those redirect pages to exist on GitHub Pages (Netlify additionally reads them from `_redirects`).

## Build and verify

- There are no npm scripts or repository test, lint, formatter, or typecheck commands. Install the declared frontend tools with `npm ci`.
- A **Go toolchain on `PATH`** is required: the HugoBlox modules in `config/_default/module.yaml` are fetched by Hugo via `go`, and `npm ci` must have installed the Tailwind v4 CLI in `node_modules/.bin` before CSS can render.
- Use `hugo server -D` for local preview; use `hugo --minify` for a focused production build.
- Generate the search index **after every production build**: `npx pagefind --site public`.
- For the closest Netlify build, run `npm ci && hugo --gc --minify -b "$URL" && npx pagefind --source public`. Deploy previews add `--buildFuture`.
- Run `hugo mod tidy` only when Hugo module metadata or dependencies change.

## Deployment and generated files

- Pushes to `main` deploy to GitHub Pages. CI builds with `hugo --minify --baseURL "<Pages base URL>/"`, then runs Pagefind; preserve that order.
- `config/_default/hugo.yaml` has a placeholder `baseURL`, so pass an explicit base URL when validating production links.
- Do not commit generated `public/`, `resources/`, `hugo_stats.json`, `.hugo_build.lock`, `node_modules/`, or `go.sum` (all are ignored).
- `publications.bib`, when present, is converted into `content/publication/` by the `import-publications` GitHub workflow.
