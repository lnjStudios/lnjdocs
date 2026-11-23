# linksndocs: docs.lnjstudios.com

"Links & Docs": robotics docs and guides by LnJ Studios. Hugo (extended) + Hextra theme as a **Hugo module**
(`go.mod`, `github.com/imfing/hextra v0.13.0`), so Go is needed and there is no theme submodule.

## Run / build

```sh
hugo server            # needs Go for the module download
hugo --gc --minify
```

## Deploy

`.github/workflows/pages.yaml`: push to `main` → Hugo 0.168.0 build (keep it ≥0.158: `hugo.yaml` uses `locale`) → GitHub Pages on
`koustavbetal.github.io`, which redirects to `docs.lnjstudios.com` (custom domain set in the repo's Pages settings).
The workflow hardcodes `--baseURL https://<owner>.github.io/`, so canonical/og/sitemap URLs point at
github.io instead of `docs.lnjstudios.com`.

## Layout

- `hugo.yaml`: config, menu (Docs, Guides, Search, About), dark theme, logos `static/images/lnj_*-mode.png`,
  footer `links` (first one: the `lnj` icon → lnjstudios.com, then socials).
- `content/docs/`: `MicroROS/` (setup, PIO code breakdown, troubleshooting) and `AMR-Docs/`
  (create a ROS 2 robot, robot state publisher, `ros2_control/`).
- `content/guides/`: How to Git, ROS2 101, ROS-Manager, URDF Wizard (`type: blog` lists).
- `content/about/`: hero (what this site is) + two cards: main site, and "Meet the contributors". No author pages here: author profiles
  live only on the main site (`https://lnjstudios.com/koustav/`).
- `layouts/`: overrides for sidebar (Hextra v0.13.0's, rooted at `/docs/<topic>/` so each topic lists only its own pages), footer (based on Hextra v0.13.0's; styles in `custom.css` `.lnj-*`, since
  the theme's Tailwind is precompiled and new `hx:` classes may not exist), search (v0.13 dialog trigger with a
  `/` hint; own `.lnj-search-kbd` class since theme JS rewrites `.hextra-search-trigger-kbd` to ⌘K on Mac), 404, blog list/single, `steps` shortcode; `assets/css/custom.css`;
  `data/icons.yaml` for custom icons (e.g. `u-ros`, `lnj` = the LnJ mark cropped from the main site's brand SVG).

## Conventions

- Front matter: `title`, `tags`, `description`, `date` (IST, `+05:30`), `authors` linking to `https://lnjstudios.com/koustav/`.
- File names have spaces (`MicroROS Setup.md`); Hugo slugifies them to lowercase-hyphen URLs.

## Gotchas

- Hugo here is a snap: `--destination` can't write to `/tmp` (private) or hidden dirs in `~`.
- Split with the main site: lnjstudios.com is for everyone (notes, releases, tool landing pages, about/author);
  this site is the deep end (chapter docs, function-by-function guides).
- `Robot State Publisher.md` currently has the title "MicroROS Troubleshooting" (copy-paste).
- Placeholder pages are live: `ros2_control/hgvhodcvdsuhfv.md`, `ros2_control/_index.md` ("hgchgchg"),
  and junk tags (`khuby`, `grduyfu`, `roman`, `jazzy-jelisco`, `ros2_conttrol`). Use `draft: true` for WIP.
- `.gitignore` is a ROS/colcon template and doesn't ignore `public/` or `resources/`.
