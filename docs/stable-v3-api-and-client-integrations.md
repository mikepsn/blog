---
- Available as a Swagger endpoint.
- New endpoints for creating and fetching logs.
- New endpoints for creating and fetching deployments.
- Request throttling to make sure that you don't use up all of your included messages within a few minutes.
- API available on `https://api.elmah.io` (rather than `https://elmah.io/api`), which makes it possible for us to scale and modify the API without touching the website.

The message endpoints used to log messages to elmah.io looks almost identical to v2.