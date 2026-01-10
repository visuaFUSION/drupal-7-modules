# Chaos Tool Suite (CTools) for Drupal 7.x

This suite is primarily a set of APIs and tools to improve the developer experience. It also contains a module called **Page Manager** whose job is to manage pages. In particular it manages panel pages, but as it grows it will be able to manage far more than just Panels.

For the moment, it includes the following tools:

- **Plugins** — tools to make it easy for modules to let other modules implement plugins from `.inc` files.
- **Exportables** — tools to make it easier for modules to have objects that live in the database or live in code, such as 'default views'.
- **AJAX responder** — tools to make it easier for the server to handle AJAX requests and tell the client what to do with them.
- **Form tools** — tools to make it easier for forms to deal with AJAX.
- **Object caching** — tool to make it easier to edit an object across multiple page requests and cache the editing work.
- **Contexts** — the notion of wrapping objects in a unified wrapper and providing an API to create and accept these contexts as input.
- **Modal dialog** — tool to make it simple to put a form in a modal dialog.
- **Dependent** — a simple form widget to make form items appear and disappear based upon the selections in another item.
- **Content** — pluggable content types used as panes in Panels and other modules like Dashboard.
- **Form wizard** — an API to make multi-step forms much easier.
- **CSS tools** — tools to cache and sanitize CSS easily to make user-input CSS safe.

This description comes straight from the legacy **Drupal 7-era project page**, capturing CTools at its peak as the foundational Swiss Army knife for many of the most powerful site-building modules in the Drupal 7 ecosystem (like Panels, Views bulk operations, etc.).

---

## Versions

| Directory | Version | Status |
|-----------|---------|--------|
| `ctools-7.x-1.21/` | 7.x-1.21 | Original from drupal.org |
| `ctools-7.x-2026.03/` | 7.x-2026.03 | Updated for Drupal 7 LTSR |

---

## Changes in 7.x-2026.03

### Bug Fixes

**PHP 8.1 Compatibility — "Attempt to assign property on bool"**
- **File:** `includes/content.inc`
- **Issue:** [#3413093](https://www.drupal.org/project/ctools/issues/3413093)
- **Fix:** Added `!is_object($content)` check in `ctools_content_render()` to handle render callbacks that return non-object values

**Undefined Index Fix — term.inc**
- **File:** `plugins/arguments/term.inc`
- **Issue:** [#3497028](https://www.drupal.org/project/ctools/issues/3497028)
- **Fix:** Added `isset($conf['input_form'])` check before accessing the configuration value

### Security Hardening

**Path Traversal Prevention — stylizer.inc**
- **File:** `includes/stylizer.inc`
- **Fix:** Added input sanitization in `ctools_stylizer_get_image_path()` and `ctools_stylizer_get_css_id()` to prevent path traversal attacks via malformed style names

### Not Applied

Modal accessibility patches are documented but not applied due to complexity. See `MODAL_ACCESSIBILITY_PATCHES.md` for details.

---

## Security Notes

CTools contains architectural patterns inherited from Drupal 7's design that warrant awareness:

| Pattern | Location | Risk Level | Notes |
|---------|----------|------------|-------|
| `eval()` for exports | `includes/export.inc` | **Admin-only** | Intentional D7 design for code-based exports; only admins can import |
| `unserialize()` on cache | `includes/object-cache.inc` | **Low** | Operates on database-cached data; requires DB write access to exploit |
| `.html()` in modals | `js/modal.js` | **Medium** | Server-side must sanitize output; use `check_plain()` and `filter_xss()` |

**Recommendations:**
- Restrict admin permissions to trusted users only
- Ensure server-side output sanitization in all content rendered in modals
- Do not import exports from untrusted sources

---

## Submodules

| Module | Description |
|--------|-------------|
| **Chaos tools** | Core API library |
| **Page manager** | UI and API to manage pages |
| **Views content panes** | Allows Views content in Panels |
| **Custom content panes** | Create exportable content panes |
| **Custom rulesets** | Create exportable access rulesets |
| **Stylizer** | Create custom styles for Panels |
| **Bulk Export** | Bulk export data objects |
| **Term Depth access** | Access control based on term depth |
| **CTools AJAX Example** | Example module for AJAX usage |
| **CTools Plugin Example** | Example module for plugin development |
