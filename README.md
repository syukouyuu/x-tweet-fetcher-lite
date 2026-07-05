# x-tweet-fetcher-lite

Current version: `1.1.0`

A small Codex/OpenClaw skill for fetching two default-supported content types:

- single public X/Twitter tweets via `scripts/fetch_tweet.py`
- public WeChat articles via `scripts/fetch_china.py`

This repository is intentionally trimmed down. It does not include timeline
crawling, reply crawling, Nitter clients, Playwright clients, profile analysis,
tweet growth tracking, paper tools, or search utilities.

## Files

```text
.
├── SKILL.md
├── README.md
├── VERSION
└── scripts
    ├── __init__.py
    ├── camofox_client.py
    ├── fetch_china.py
    └── fetch_tweet.py
```

## Requirements

- Python 3.10+
- No mandatory pip dependencies for the default-supported paths
- Network access for live fetching
- Optional Camofox service on `localhost:9377` for experimental Chinese
  platform paths that need browser rendering

## Fetch A Single Tweet

```bash
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456"
```

Pretty JSON:

```bash
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456" --pretty
```

Text output:

```bash
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456" --text-only
```

This route uses FxTwitter and returns tweet text, author metadata, stats,
media, quote information, and long-form article content when available.

## Fetch WeChat Articles

```bash
python3 scripts/fetch_china.py --url "https://mp.weixin.qq.com/s/..." --pretty
```

Public WeChat article fetching uses direct HTTP in the common case and is the
only default-supported Chinese-platform path in this lite skill.

## Experimental Camofox Paths

`fetch_china.py` still contains parsers for sites such as Weibo, Bilibili,
CSDN, Xiaohongshu, and Zhihu, but those paths require a Camofox-compatible
browser service on `localhost:9377` and are not treated as guaranteed lite
features.

On a default VPS without Camofox, Weibo and Bilibili will not work. If Camofox is
not running, report that condition directly.

The helper module `scripts/camofox_client.py` talks to this local service only.
It is included because `fetch_china.py` imports it.

## Verification

Local syntax and CLI smoke checks:

```bash
python3 -m py_compile scripts/fetch_tweet.py scripts/fetch_china.py scripts/camofox_client.py scripts/__init__.py
python3 scripts/fetch_tweet.py --help
python3 scripts/fetch_china.py --help
```

## Not Included

The lite version deliberately excludes:

- user timeline crawling
- reply or nested reply crawling
- Nitter clients
- Playwright browser clients
- profile analysis
- tweet growth tracking
- paper recommendation or Obsidian export tools
- general web search helpers
