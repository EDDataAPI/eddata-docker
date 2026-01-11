# EDData Stack - Aggregated Changelog (Last 7 Days)

Last updated: 2026-01-11 01:46:31 UTC

## eddata-collector

- **2026-01-05**: Add option to skip trade.db snapshots for low-memory servers ([ad7bb34](https://github.com/EDDataAPI/eddata-collector/commit/ad7bb34888ac8cd343f43ec513d113ae1a824a2e))
- **2026-01-04**: Add safe vacuum script for large SQLite databases ([49f5800](https://github.com/EDDataAPI/eddata-collector/commit/49f5800b8c9047e98d62acc43ea84825b907047f))
- **2026-01-04**: Remove staging/production configs and Cloudflare Worker ([9aa12fd](https://github.com/EDDataAPI/eddata-collector/commit/9aa12fddfe742bfc20f531624d58e02fb8b15bed))
- **2026-01-04**: Remove unused import in cleanup-old-trades.js ([e0c1bda](https://github.com/EDDataAPI/eddata-collector/commit/e0c1bdae585fdbec48f1ad3d062309f7f8262c3e))
- **2026-01-04**: Reduce trade data retention to 30 days and add cleanup script ([96b3a56](https://github.com/EDDataAPI/eddata-collector/commit/96b3a56c476efa397043135f1b9cbae876e1b9d7))
- **2026-01-04**: Increase SQLite cache and memory limits for large databases ([fdd12a8](https://github.com/EDDataAPI/eddata-collector/commit/fdd12a87a107230c618954d65ac83ba8caad25f1))
- **2026-01-04**: Use SKIP_INTEGRITY_CHECKS constant in startup script ([0a25f37](https://github.com/EDDataAPI/eddata-collector/commit/0a25f377d85474bf4ad2104f47984feb0e3979ae))
- **2026-01-04**: Adjust DB healthcheck timing and update integrity check message ([a8a612c](https://github.com/EDDataAPI/eddata-collector/commit/a8a612cfe438862dfce34a835051595a04bc215c))
- **2026-01-04**: Add option to skip database integrity checks on startup ([247bd31](https://github.com/EDDataAPI/eddata-collector/commit/247bd31a71ba02bbb5280949c5c62a27d37c99e8))
- **2026-01-04**: Add option to skip expensive index creation on startup ([bd8d4a8](https://github.com/EDDataAPI/eddata-collector/commit/bd8d4a8a23ff35d1be27477048be2a557fd84897))
- **2026-01-04**: Enhance caching, docs, and Docker performance options ([2816f61](https://github.com/EDDataAPI/eddata-collector/commit/2816f614bbe108d1089eb92e7726268b63d279f4))
- **2026-01-04**: Improve health check and maintenance status reporting ([89b96c2](https://github.com/EDDataAPI/eddata-collector/commit/89b96c2def1ae75832441ad0f7bfcbad99ebb1ca))
- **2026-01-04**: Fix formatting and logging in maintenance and stats scripts ([27bb3e9](https://github.com/EDDataAPI/eddata-collector/commit/27bb3e9cf86d79c664e8f346379d94f106317833))
- **2026-01-04**: Add SKIP_STARTUP_MAINTENANCE and async maintenance for faster startup ([b522034](https://github.com/EDDataAPI/eddata-collector/commit/b52203472278dc168e5aeb3cbf58b110debfbf24))

## eddata-api

- **2026-01-05**: Remove Cloudflare Worker and minor code cleanup ([3ba6860](https://github.com/EDDataAPI/eddata-api/commit/3ba68600fa5c33a97d6ef82a4a7b5190e0737bb8))
- **2026-01-04**: Update v1 API route to use wildcard matcher ([d99895e](https://github.com/EDDataAPI/eddata-api/commit/d99895ebc4886bd94256cc2ec360d0ffd311faa6))
- **2026-01-04**: Add Cloudflare Worker and update workflows ([a95a497](https://github.com/EDDataAPI/eddata-api/commit/a95a49709f67bd3093d0b55f30da8d697486f528))

## eddata-auth

- **2026-01-05**: Improve error handling and visitedstars response ([530ccbf](https://github.com/EDDataAPI/eddata-auth/commit/530ccbfa64d4e0c5521a856f7394f3090e980207))
- **2026-01-05**: Improve error handling and CORS in API routes ([99f011f](https://github.com/EDDataAPI/eddata-auth/commit/99f011fc16c6dcb1607682c3d2da3e90f3520b8c))
- **2026-01-05**: Fix CORS header when Origin is missing ([3e8b6d1](https://github.com/EDDataAPI/eddata-auth/commit/3e8b6d1a10def38f17be1d03f624b17976b8a592))
- **2026-01-04**: Update dependencies to latest major versions ([ffa5fc0](https://github.com/EDDataAPI/eddata-auth/commit/ffa5fc0c39445957480a65a7c9569bf0e5c0528f))

## eddata-www

- **2026-01-05**: Remove 'proxy' references from API comments ([21c5e37](https://github.com/EDDataAPI/eddata-www/commit/21c5e37ea03aa4f4a92b9ca909874a3032ecb47f))
- **2026-01-05**: Refactor API fetch URLs to use API_BASE_URL constant ([be5badb](https://github.com/EDDataAPI/eddata-www/commit/be5badb31edef27e6880e1a475cfd42967f11571))
- **2026-01-05**: Refactor API routes to Next.js pages API format ([f979534](https://github.com/EDDataAPI/eddata-www/commit/f979534cde933b69f8156f6f4740de7804a69ffd))
- **2026-01-05**: Migrate API endpoints to Next.js 16 route handlers ([882c454](https://github.com/EDDataAPI/eddata-www/commit/882c45404b1b64259aff9971dc018c8bf48afead))
- **2026-01-04**: Refactor Dockerfile dependency installation steps ([9e862f6](https://github.com/EDDataAPI/eddata-www/commit/9e862f66bcfd8aa9c30256fa1925c7bcede774d3))
- **2026-01-04**: Include .npmrc in Docker build context ([d7c5463](https://github.com/EDDataAPI/eddata-www/commit/d7c54631d3746f2a897399d7d4cce9edcdef2ec7))
- **2026-01-04**: Add .npmrc to enable legacy peer deps ([5b2f0dc](https://github.com/EDDataAPI/eddata-www/commit/5b2f0dcc5de05b56443bbdaf156976dce981849c))
- **2026-01-04**: Refactor to ES module syntax and update dependencies ([226ec01](https://github.com/EDDataAPI/eddata-www/commit/226ec019e736f5ae516691df7c2be365f1123871))

