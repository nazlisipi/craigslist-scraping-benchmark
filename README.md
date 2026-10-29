# Craigslist Scraping Benchmark

AIMultiple benchmark of Bright Data, Oxylabs, Decodo, Nimble and Zyte on 500 Craigslist job posting pages, measuring success rate and end-to-end completion time.

> [Read the benchmark on AIMultiple](https://aimultiple.com/craigslist-scraper)

## Workload

Each provider received the same 500 job posting URLs, sent sequentially with a 2-second delay between requests, for 2,500 runs. All five returned rendered HTML from their production endpoints.

A run succeeded only if it passed three checks:

- Submission: the provider returned HTTP 200 to 399, or 404.
- Execution: async jobs finished within 10 minutes without errors. HTTP 429 triggered a 30-second backoff with up to 3 retries.
- Validation: CSS selectors found a non-empty job_title or company_name. Detected 404 pages counted as valid. An empty response became invalid if another provider extracted job data from the same URL.

## Benchmark results

All five providers reached 100% success, so the comparison uses average wall-clock completion time per request, with 95% bootstrap confidence intervals:

| Provider | Completion time (s) | 95% CI (s) |
| --- | ---: | ---: |
| Bright Data | 1 | 1-1.15 |
| Nimble | 7 | 6.57-7.35 |
| Oxylabs | 11 | 11-11.83 |
| Decodo | 12 | 11.60-12.67 |
| Zyte | 17 | 16.46-18.44 |

Only the Oxylabs and Decodo intervals overlap, so the data does not separate those two. Bright Data was the only provider run through a proxy (Web Unblocker); the other four used scraper or extraction APIs.

## Scope

Results cover one target, which the article describes as mostly static HTML with minimal JavaScript and few anti-bot defenses, so timings may differ on better-protected sites. Provider settings differed. The benchmark was added to the article on April 29, 2026.

## Ownership

The benchmark implementation was developed for AIMultiple and belongs to AIMultiple. This repository contains a documentation summary. Source code and benchmark datasets are not distributed here.
