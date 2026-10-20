# Telegram Channel Scraper — Python, Node.js & cURL examples

Get **posts from public Telegram channels** — text, date, **views, reactions**, links, photos, videos and forwards — plus **channel info** with subscribers. Newest N posts or the last N days. **$0.30 per 1,000 messages**, no Telegram account.

Hosted on Apify: **[Telegram Channel Scraper](https://apify.com/tidydata/telegram-channel-scraper)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/telegram-channel-scraper").call(run_input={
    "channels": [
        "@durov",
        "https://t.me/telegram"
    ],
    "maxMessagesPerChannel": 200,
    "newerThanDays": 30
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['channel', 'date', 'views', 'text']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/telegram-channel-scraper').call({"channels": ["@binance_announcements"], "newerThanDays": 7});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~telegram-channel-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"channels": ["@binance_announcements"], "newerThanDays": 7}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor) · [Google News](https://apify.com/tidydata/google-news-scraper) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.
