# Agundur GEO Scan

> Check whether a live URL is ready to be cited by AI search engines and LLMs (ChatGPT, Copilot, Perplexity, Google AI Overviews) — right from your GitHub Actions pipeline.

This action calls the free **GEO Scanner** API from [agundur.de](https://www.agundur.de/geo-scanner.html) and checks a URL for `llms.txt`, structured data, answer directness, E-E-A-T signals and more. It returns a 0-100 score plus a per-check breakdown, without leaving your CI run.

## What is GEO?

Generative Engine Optimization (GEO) is the SEO equivalent for AI-generated answers: making content easy for an LLM to find, understand, and cite as a source. This action runs the same rule-based checks as agundur.de's public GEO Scanner tool — no LLM calls involved, no API key required, deterministic and fast.

## Usage

```yaml
- name: GEO Scan
  uses: Agundur-KDE/geo-scan-action@v1
  with:
    url: https://example.com
```

### Fail the build below a threshold

```yaml
- name: GEO Scan
  uses: Agundur-KDE/geo-scan-action@v1
  with:
    url: https://example.com
    fail-under: '70'
```

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `url` | ✓ | — | The URL to scan |
| `lang` | | `en` | Report language: `de` or `en` |
| `fail-under` | | *(none)* | Fail the build if the score is below this threshold (0-100) |

## Outputs

| Output | Description |
|---|---|
| `score` | GEO score (0-100) |
| `report` | Full JSON report (score + per-check breakdown) |

## What gets checked

HTTPS, `robots.txt` rules for AI crawlers, indexability, canonical tags, `llms.txt`, Schema.org structured data, content freshness, FAQ markup, Open Graph tags, content available without JavaScript, heading structure, answer directness (does the first paragraph actually answer the page's core question), image alt text, and E-E-A-T signals.

## Try it without CI

Want to check a URL right now, no YAML required? Use the free web version at **[agundur.de/geo-scanner](https://www.agundur.de/geo-scanner.html)** — same checks, same scoring, instant result in your browser.

## Notes

This action is a thin wrapper around agundur.de's public API — the scan itself runs server-side, the scoring logic isn't bundled into this repo. Free to use; fair-use rate limits may apply in the future.

## License

MIT © [Agundur-KDE](https://github.com/Agundur-KDE)
