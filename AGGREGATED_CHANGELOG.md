# EDData Stack - Aggregated Changelog (Last 7 Days)

Last updated: 2025-11-30 01:40:01 UTC

## eddata-collector

- **2025-11-26**: fix: Write only articles array to galnet-news.json cache (not wrapper object) ([787fd44](https://github.com/EDDataAPI/eddata-collector/commit/787fd447a7e39253ffe287cc3801ace938efbd1f))
- **2025-11-26**: debug: Add detailed logging to GalNet news fetching ([2fbff4e](https://github.com/EDDataAPI/eddata-collector/commit/2fbff4e122981e2fc4de1df47282abffd30cfdd6))

## eddata-api

- **2025-11-27**: fix: Allow server-to-server requests without origin header for Next.js proxy ([649137b](https://github.com/EDDataAPI/eddata-api/commit/649137bef35da69a83d33e3f5742a42f42745b81))
- **2025-11-26**: fix: Extract articles array from galnet-news.json collector format ([9962ddf](https://github.com/EDDataAPI/eddata-api/commit/9962ddf643bfdbbfd52bab337de8878badc502e5))
- **2025-11-25**: security: Fix js-yaml prototype pollution vulnerability via npm audit fix ([cfa7bd4](https://github.com/EDDataAPI/eddata-api/commit/cfa7bd44cb672cbfa84aa76beefc30068a44e07d))

## eddata-auth


## eddata-www

- **2025-11-27**: debug: add detailed logging to API proxy for troubleshooting ([ad46d49](https://github.com/EDDataAPI/eddata-www/commit/ad46d492246598d4246fe9e9f0d2b4d6105064ae))
- **2025-11-27**: Remove trailing whitespace in Cloudflare purge step ([9ed9bd6](https://github.com/EDDataAPI/eddata-www/commit/9ed9bd6404b42c72572123271b013b94ae8f8642))
- **2025-11-27**: feat: add Cloudflare cache purge after deployment ([8b52fd5](https://github.com/EDDataAPI/eddata-www/commit/8b52fd514815709fccb202972514fdc098351652))
- **2025-11-26**: fix: restore exact working API proxy from commit 5bd6bfe ([f7adbbf](https://github.com/EDDataAPI/eddata-www/commit/f7adbbf84cb037e0c2afb9657d4714fadfa4366f))
- **2025-11-26**: fix: simplify API proxy whitelist to allow all v2/ and api/ endpoints ([d9bed44](https://github.com/EDDataAPI/eddata-www/commit/d9bed44cbf4cf9427c2ffe3537dce3fe997c2a74))
- **2025-11-26**: fix: revert to working API proxy endpoint whitelist ([b23f9fa](https://github.com/EDDataAPI/eddata-www/commit/b23f9fa97f6c2b5d5285ec44c08422a065278451))
- **2025-11-26**: fix: improve API proxy endpoint matching logic ([4f5e845](https://github.com/EDDataAPI/eddata-www/commit/4f5e845e0372eabe4aeb5bfae505dc66974c0748))
- **2025-11-26**: fix: correct API proxy endpoint whitelist ([d4f4d53](https://github.com/EDDataAPI/eddata-www/commit/d4f4d535f51631d98529e1e62fe577fe384c2c63))

