---
layout: post
title:  "Optimizing API Calls: A Quick Fix for Faster Websites"
date:   2024-09-26 13:00:44 +0545
categories: Rails, Nextjs
share: true
---

**Last week, I wrote code after long time.** It felt good to be back, and my task was straightforward: improve the performance of a website. 

The site uses a following technology stack:
- **Backend**: Ruby on Rails
- **Frontend**: Next.js
- **Database**: PostgreSQL

As I dug into the site’s performance, a few things caught my attention:
1. Multiple redundant API calls were being made from the same page.
2. The API responses were bloated with unnecessary data. For example, even if the homepage only needed 20 items, the API was returning the entire dataset, complete with irrelevant associated data.
3. **API Call Priority**: The API that provided data for the hero section—one of the most critical parts of the page—was being called last, delaying its rendering.

**So, I made a few key changes that drastically improved the site's performance:**
1. **Eliminated redundant API calls**: I consolidated the calls so that the same data wasn’t being fetched multiple times.
2. **Optimized API responses**: By breaking down large APIs and limiting the data returned, I was able to reduce both database load and the size of the responses. This sped up the overall API performance.
3. **Prioritized API calls**: Even though JavaScript API calls are asynchronous, they still hit the backend and can bottleneck if poorly sequenced. I made sure the hero section's data was fetched first, ensuring that key content loaded faster and improved the user experience.

There are countless ways to enhance site performance, but sometimes small tweaks can make a big impact.

Until next time, happy coding!

