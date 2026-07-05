# x-tweet-fetcher-lite

A small Codex/OpenClaw skill for fetching two kinds of content:

- single public X/Twitter tweets via `scripts/fetch_tweet.py`
- selected Chinese platform pages via `scripts/fetch_china.py`

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

- Python 3.9+
- No mandatory pip dependencies for the supported single-tweet path
- Network access for live fetching
- Optional Camofox service on `localhost:9377` for Chinese platform pages that
  need browser rendering

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

## Fetch Chinese Platform Content

```bash
python3 scripts/fetch_china.py --url "https://mp.weixin.qq.com/s/..." --pretty
python3 scripts/fetch_china.py --url "https://weibo.com/..." --pretty
python3 scripts/fetch_china.py --url "https://www.bilibili.com/video/..." --pretty
python3 scripts/fetch_china.py --url "https://blog.csdn.net/..." --markdown
```

`fetch_china.py` supports automatic platform detection. Some platforms can be
parsed through direct HTTP, while others require Camofox for rendering.

## Camofox

For pages that require browser rendering, start a Camofox-compatible browser
service on port `9377`.

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
