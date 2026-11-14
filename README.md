# Bilibili Scraper

![Bilibili Scraper](https://raw.githubusercontent.com/smoldesk/apify-scrapers/main/assets/bilibili/banner.webp)

Scrape Bilibili (哔哩哔哩) videos, comments, danmaku (弹幕), creators and trending charts. No login and no API key (an optional cookie of your own unlocks full comment threads). Runs on [Apify](https://apify.com/smoldesk/bilibili-scraper).

## What you get

- **Keyword search** with sort, video length and date range filters (dates or relative: `7 days`, `3 months`). Latin brand names are also searched under their Chinese name (Nike + 耐克), plus your own aliases.
- **Videos**: views, likes, coins, favorites, shares, danmaku and comment counts, engagement rate, tags, category, honors and the uploader's followers.
- **Creators**: profile (followers, level, bio, verification, live room) and their uploads, newest or most played.
- **Trending**: the popular feed and the top-100 ranking for 18 categories.
- **Comments and replies**: most liked and newest merged, plus reply threads. Follow-up mode re-reads delivered videos a day later for new comments.
- **Danmaku**: the scrolling comments, with the second of the video each one appears at, for every part of multi-part videos. Optional **danmaku profile** per video: busiest minute, reactions per minute, most repeated lines.
- **Chinese sentiment**: positive / neutral / negative + score on comments, danmaku and titles, tuned for Bilibili slang.
- **Pseudonymous mode**: stable keys instead of commenter names and IDs.
- **Only new videos** mode for daily monitoring of a keyword or creator.

## Run it

Open the [Bilibili Scraper on Apify](https://apify.com/smoldesk/bilibili-scraper), fill in the form and click Start. Or call it from code with your [Apify token](https://console.apify.com/settings/integrations):

```bash
curl -X POST "https://api.apify.com/v2/acts/smoldesk~bilibili-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "searchQueries": ["黑神话悟空"],
    "maxVideosPerSearch": 100,
    "searchSort": "views",
    "publishedAfter": "2026-09-01",
    "includeDanmaku": true,
    "maxDanmakuPerVideo": 200,
    "includeDanmakuProfile": true,
    "sentimentAnalysis": true
  }'
```

## Sample output

```json
{
  "type": "video",
  "bvid": "BV1bdpC6PEmG",
  "url": "https://www.bilibili.com/video/BV1bdpC6PEmG",
  "title": "想象轻启丨第二代海鸥视界大不一样",
  "durationSeconds": 60,
  "durationText": "1:00",
  "publishedAt": "2026-10-14T07:30:39+00:00",
  "category": "日常",
  "tags": ["比亚迪"],
  "authorName": "比亚迪",
  "authorFollowers": 243950,
  "views": 7325,
  "likes": 217,
  "coins": 29,
  "favorites": 9,
  "shares": 49,
  "danmakuCount": 2,
  "commentCount": 147,
  "engagementRate": 0.0618
}
```

```json
{
  "type": "danmaku",
  "videoBvid": "BV1g1C6Y2Ef3",
  "text": "在进入二周目前，先来跟着up检查一番",
  "videoTimeSeconds": 0,
  "mode": "scroll",
  "color": "#e2027f",
  "sentAt": "2025-09-29T08:41:44+00:00"
}
```

Export as JSON, CSV or Excel, or pipe it into Google Sheets, Make, Zapier or n8n.

## Pricing

Pay per result. No monthly fee. Prices drop on paid Apify plans.

| Result (per 1,000) | Free | Starter | Scale | Business |
|---|---|---|---|---|
| Video | $2.50 | $2.50 | $2.20 | $1.90 |
| Creator profile | $2.00 | $2.00 | $1.75 | $1.50 |
| Comment or reply | $0.50 | $0.50 | $0.50 | $0.50 |
| Danmaku | $0.10 | $0.10 | $0.10 | $0.10 |


## Limits

- Without a cookie Bilibili shows about 3 comments per order, so you get ~6 top-level comments per video (most liked + newest) plus complete reply threads. Add your own `SESSDATA` cookie for full threads, or use danmaku for reactions at scale.
- Sentiment is word-list based (no AI model) and stays neutral on sarcasm or memes it doesn't know.
- Bilibili caps keyword search at 1,000 results per query. Split by date range or use narrower keywords.
- Danmaku covers the most recent 1,000 to 3,000 per video.
- Subtitles and play URLs need a login and are not included.

## FAQ

**Does Bilibili have a public API?**
Not an official one for developers. This scraper reads the public endpoints the website loads for any visitor and returns JSON with English field names.

**How do I scrape Bilibili comments?**
Set `includeComments` to true. `maxCommentsPerVideo` caps the rows per video; replies fill up the rest. Logged out, Bilibili shows about 3 comments per order. For full threads paste the `SESSDATA` cookie of your own account (a secondary one is best) into `bilibiliCookie`; it is used only for comment requests.

**What are coins on Bilibili?**
Viewers tip videos with coins. With likes and favorites they are the strongest engagement signal on the platform, and the video record includes all three.

**Do I need a Bilibili account or a Chinese phone number?**
No. Everything works without one. A cookie of your own only adds full comment threads.

**How do I track a creator's new uploads?**
Put the UID or profile URL in `users`, turn on `onlyNewVideos` and schedule the run daily.

## More scrapers

Bilibili is one of 21 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
