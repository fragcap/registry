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

- **Shards** are written by the FragCap Cloudflare Worker using a GitHub App installation token.
- **manifest.json** is auto-rebuilt by GitHub Actions whenever a shard is pushed.
- **GitHub Pages** serves all files as static JSON — no rate limits for readers.

## GitHub Pages

This repo is served at `https://fragcap.github.io/registry/`.

Readers fetch:
1. `GET /registry/manifest.json` — list of shard filenames (cached 1h)
2. `GET /registry/shards/{hash}.json` — per-user capsule summaries (cached 24h)
