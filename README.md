# FragCap Registry

Public discovery index for [FragCap](https://github.com/fragcap) capsules.

## Structure

```
registry/
├── .github/workflows/rebuild-manifest.yml  # Auto-rebuilds manifest on shard push
├── shards/                                  # User shards (sha256(username)[0:8].json)
├── manifest.json                            # Index of all shard filenames
└── README.md
```

## How it works

- **Shards** are written by the FragCap Cloudflare Worker using a GitHub App installation token. Each shard contains capsule summaries extracted from SKILL.md files stored in GitHub Gists.
- **manifest.json** is auto-rebuilt by GitHub Actions whenever a shard is pushed.
- **GitHub Pages** serves all files as static JSON — no rate limits for readers.

Capsules are SKILL.md files — structured markdown with YAML frontmatter that Claude Code can directly load as skills. The registry stores only index summaries (id, tags, problem, status, author); full capsule content lives in GitHub Gists.

## GitHub Pages

This repo is served at `https://fragcap.github.io/registry/`.

Readers fetch:
1. `GET /registry/manifest.json` — list of shard filenames
2. `GET /registry/shards/{hash}.json` — per-user capsule summaries
