# Bilibili Scraper

![Bilibili Scraper](https://raw.githubusercontent.com/smoldesk/apify-scrapers/main/assets/bilibili/banner.webp)

Scrape Bilibili (哔哩哔哩) videos, comments, danmaku (弹幕), creators and trending charts. No login, no cookies, no API key. Runs on [Apify](https://apify.com/smoldesk/bilibili-scraper).

## What you get

- **Keyword search** with sort, video length and date range filters.
- **Videos**: views, likes, coins, favorites, shares, danmaku and comment counts, tags, category, honors and the uploader's followers.
- **Creators**: profile (followers, level, bio, verification, live room) and their uploads, newest or most played.
- **Trending**: the popular feed and the top-100 ranking for 18 categories.
- **Comments and replies**: text, likes, author, level and reply threads.
- **Danmaku**: the scrolling comments, with the second of the video each one appears at.
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
    "maxDanmakuPerVideo": 200
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
  "commentCount": 147
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

- Logged-out visitors see only the top 3 comments of each video. Reply threads are complete. Use danmaku for audience reactions at scale.
- Bilibili caps keyword search at 1,000 results per query. Split by date range or use narrower keywords.
- Danmaku covers the most recent 1,000 to 3,000 per video.
- Subtitles and play URLs need a login and are not included.

## FAQ

**Does Bilibili have a public API?**
Not an official one for developers. This scraper reads the public endpoints the website loads for any visitor and returns JSON with English field names.

**How do I scrape Bilibili comments?**
Set `includeComments` to true. `maxCommentsPerVideo` and `maxRepliesPerComment` control the depth. Bilibili shows logged-out visitors only 3 top comments per video.

**What are coins on Bilibili?**
Viewers tip videos with coins. With likes and favorites they are the strongest engagement signal on the platform, and the video record includes all three.

**Do I need a Bilibili account or a Chinese phone number?**
No. Nothing to log in to and no proxy to set up.

**How do I track a creator's new uploads?**
Put the UID or profile URL in `users`, turn on `onlyNewVideos` and schedule the run daily.

## More scrapers

Bilibili is one of 20 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
