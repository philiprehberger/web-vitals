# @philiprehberger/web-vitals

[![CI](https://github.com/philiprehberger/ts-web-vitals/actions/workflows/ci.yml/badge.svg)](https://github.com/philiprehberger/ts-web-vitals/actions/workflows/ci.yml)
[![npm version](https://img.shields.io/npm/v/@philiprehberger/web-vitals.svg)](https://www.npmjs.com/package/@philiprehberger/web-vitals)
[![License](https://img.shields.io/github/license/philiprehberger/ts-web-vitals)](LICENSE)
[![Sponsor](https://img.shields.io/badge/sponsor-GitHub%20Sponsors-ec6cb9)](https://github.com/sponsors/philiprehberger)

Web Vitals calculation utilities and client error capture

## Installation

```bash
npm install @philiprehberger/web-vitals
```

## Usage

```ts
import { getWebVitalRating, calculateWebVitalStats, formatWebVitalValue } from '@philiprehberger/web-vitals';

const rating = getWebVitalRating('LCP', 2100); // 'good'
const stats = calculateWebVitalStats('LCP', [1200, 2500, 3800, 1800]);
console.log(formatWebVitalValue('LCP', stats.p75)); // '2.5s'
```

### Client Error Capture

```ts
import { initClientErrorCapture } from '@philiprehberger/web-vitals';

initClientErrorCapture({
  endpoint: '/api/monitoring/errors',
});
```

## API

| Export | Type | Description |
|--------|------|-------------|
| `getWebVitalRating(metric, value)` | Function | Returns `'good' \| 'needs-improvement' \| 'poor'` for a metric value |
| `calculateWebVitalStats(metric, values)` | Function | Compute p50/p75/p95 percentiles and rating distribution |
| `calculatePercentile(sortedValues, percentile)` | Function | Generic percentile calculation on a sorted array |
| `formatWebVitalValue(metric, value)` | Function | Format a value for display (e.g. `2500` -> `'2.5s'`) |
| `getRatingLabel(rating)` | Function | Convert rating to display label (`'Good'`, `'Needs Improvement'`, `'Poor'`) |
| `getWorstMetric(metrics)` | Function | Find the worst-performing metric from a set of stats |
| `normalizePagePath(url)` | Function | Replace dynamic URL segments with `[id]`/`[uuid]` placeholders |
| `initClientErrorCapture(options)` | Function | Set up global error and unhandled rejection capture |
| `WEB_VITALS_THRESHOLDS` | Constant | Threshold definitions for all six Core Web Vitals |
| `WebVitalName` | Type | `'LCP' \| 'CLS' \| 'FID' \| 'INP' \| 'FCP' \| 'TTFB'` |
| `WebVitalRating` | Type | `'good' \| 'needs-improvement' \| 'poor'` |
| `WebVitalStats` | Type | Stats object with percentiles and rating counts |
| `PageWebVitals` | Type | Per-page metrics with worst metric identification |
| `ClientErrorCaptureOptions` | Type | Options: `endpoint`, `headers?`, `beforeReport?` |

## Development

```bash
npm install
npm run build
npm test
```

## License

MIT
