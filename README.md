# obs-ptz-stats

Traffic and release-download history for [glikely/obs-ptz](https://github.com/glikely/obs-ptz), tracked here instead of in that repository's own commit history.

GitHub's built-in Traffic insights only retain 14 days, and release asset download counts are a running total with no history. Two scheduled workflows in this repo snapshot that data daily and persist it on dedicated branches, so long-term trends can be reconstructed:

- **[repo-stats.yml](.github/workflows/repo-stats.yml)** — runs [jgehrcke/github-repo-stats](https://github.com/jgehrcke/github-repo-stats) against `glikely/obs-ptz` and publishes an aggregated HTML/PDF report to the `github-repo-stats` branch (views, clones, referrers, popular paths, stars, forks).
- **[release-download-stats.yml](.github/workflows/release-download-stats.yml)** — appends each release asset's `download_count` to `release-download-stats/downloads.csv` on the `release-download-stats` branch.

## Setup

`repo-stats.yml` needs a repository secret named `GHRS_GITHUB_API_TOKEN`: a personal access token with `repo` scope, able to read the traffic API for `glikely/obs-ptz` and push commits here. Add it under Settings > Secrets and variables > Actions.

`release-download-stats.yml` needs no extra setup — release download counts are public, so the default `GITHUB_TOKEN` is enough.
