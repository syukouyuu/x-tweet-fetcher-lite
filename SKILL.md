---
name: x-tweet-fetcher-lite
description: >
  Fetch a single X/Twitter tweet through FxTwitter and fetch public WeChat
  articles through fetch_china.py. This lite skill intentionally exposes only
  the maintained default-supported paths in this repository.
---

# X Tweet Fetcher Lite

Use this skill when the user asks to fetch:

- a single public X/Twitter tweet URL
- a public WeChat article URL with `fetch_china.py`

This lite version only treats these scripts as supported:

- `scripts/fetch_tweet.py`
- `scripts/fetch_china.py`
- `scripts/camofox_client.py` as a helper for `fetch_china.py`

Do not claim support for timeline crawling, reply crawling, Nitter, Playwright,
profile analysis, tweet growth tracking, paper recommendation, WeChat search,
or general web search. Those features are not part of this lite skill.

## Single Tweet

Fetch one public X/Twitter tweet through FxTwitter:

```bash
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456"
```

Useful options:

```bash
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456" --pretty
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456" --text-only
python3 scripts/fetch_tweet.py --url "https://x.com/user/status/123456" --lang en
```

The supported single-tweet path has no Python package dependencies beyond the
standard library. It does require network access to `api.fxtwitter.com`.

## WeChat Article Fetching

Fetch public WeChat article URLs:

```bash
python3 scripts/fetch_china.py --url "https://mp.weixin.qq.com/s/..." --pretty
```

Notes:

- WeChat public article fetching can often work through direct HTTP.
- This is the only default-supported Chinese-platform path in the lite skill.
- Weibo and Bilibili require a running Camofox browser service on
  `localhost:9377`; on a default VPS they should be treated as unavailable.
- If Camofox is unavailable, report that clearly instead of inventing fallback
  behavior.

## Output

Both scripts output structured JSON by default, with optional text-oriented
formats where the script supports them.

For agent use, prefer `--pretty` when the user needs inspection and default JSON
when another tool or script will consume the result.

## Boundaries

This skill is intentionally small. If the user asks for:

- user timelines
- replies or nested reply threads
- keyword search
- Nitter operations
- Playwright browser automation
- profile analysis
- tweet growth monitoring
- paper recommendation or Obsidian export
- default-VPS Weibo or Bilibili fetching

say that this lite skill does not provide that feature and ask whether they want
to use another tool or extend the skill.
