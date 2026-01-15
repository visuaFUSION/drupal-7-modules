# XML Sitemap for Drupal 7.x

The XML Sitemap module creates a sitemap that conforms to the sitemaps.org specification. This helps search engines keep their search results up to date.

## Features

- **Automatic sitemap generation** — Creates XML sitemaps conforming to sitemaps.org spec
- **Search engine submission** — Automatically submits sitemap to search engines
- **Multi-language support** — i18n integration for multilingual sites
- **Content type integration** — Nodes, taxonomy terms, users, menu links
- **Custom links** — Add custom URLs to sitemap
- **Ctools modal support** — Modal dialog integration

---

## Versions

| Directory | Version | Status |
|-----------|---------|--------|
| `xmlsitemap-7.x-2.7/` | 7.x-2.7 | Original from drupal.org |
| `xmlsitemap-7.x-2026.01/` | 7.x-2026.01 | Updated for Drupal 7 LTSR |

---

## Changes in 7.x-2026.01

### PHP 8.1+ Compatibility

**Return Type Declaration Fix — XMLSitemapWriter class**
- **File:** `xmlsitemap.xmlsitemap.inc`
- **Problem:** PHP 8.1+ requires return type declarations for methods overriding parent class methods. The `XMLSitemapWriter` class extends PHP's built-in `XMLWriter` but had malformed `#[ReturnTypeWillChange]` attributes
- **Fix:** Corrected attributes from `#[ReturnTypeWillChange]` to `#[\ReturnTypeWillChange]` on:
  - `openUri()`
  - `startElement()`
  - `writeElement()`
  - `startDocument()`
  - `endDocument()`

---

## Submodules

| Module | Description |
|--------|-------------|
| **XML Sitemap** | Core sitemap generation |
| **XML Sitemap Custom** | Add custom links to sitemap |
| **XML Sitemap Engines** | Submit sitemap to search engines |
| **XML Sitemap i18n** | Internationalization support |
| **XML Sitemap Menu** | Include menu links in sitemap |
| **XML Sitemap Modal** | CTools modal integration |
| **XML Sitemap Node** | Include nodes in sitemap |
| **XML Sitemap Taxonomy** | Include taxonomy terms in sitemap |
| **XML Sitemap User** | Include user profiles in sitemap |

---

## Requirements

- PHP 7.4+ (PHP 8.0+ recommended, PHP 8.1+ compatible)
- Drupal 7 LTSR

---

## Upgrade Notes

- Direct drop-in replacement for XML Sitemap 7.x-2.7
- No database updates required
- No configuration changes needed
