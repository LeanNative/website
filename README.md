# LeanNative website

The static site for https://leannative.com: `docs/`, with the examples' newest journey media from LeanNative's
CI, deployed by GitHub Pages from [the Pages workflow](.github/workflows/pages.yml) (the Pages source is
"GitHub Actions").

- `docs/index.html`, `docs/style.css`: the page (plain HTML and CSS, no scripts)
- `docs/CNAME`: the custom domain
- `scripts/fetch-journey-media`: takes the newest successful run of LeanNative's check.yml on main that published
  every example's `journey-media-<example>` artifact, checks each against its journey-provenance.json, and puts
  it in `docs/journeys/<example>/`. Build output: never committed. When it fails, nothing is deployed.
- `scripts/check-site`: every `journeys/` file the page names is there.
- The workflow deploys on a push to main, every six hours, and by hand; a pull request only builds and checks.
- What is left lives in [LeanNative's issues](https://github.com/LeanNative/leannative/issues), not on the page.

Preview, with CI's media (needs a token, e.g. `GH_TOKEN=$(gh auth token)`) or a local journey-media output
(`DIR/simple/`, `DIR/bluetooth-auth/`):

    scripts/fetch-journey-media [--from DIR] && scripts/check-site && python3 -m http.server -d docs
