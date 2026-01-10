**Chaos Tool Suite (CTools) for Drupal 7.x**

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

This description comes straight from the classic **Drupal 7-era project page** (and closely matches the original README), capturing CTools at its peak as the foundational Swiss Army knife for many of the most powerful site-building modules in the Drupal 7 ecosystem (like Panels, Views bulk operations, etc.).

Note: Drupal 7 is end-of-life, and this version of CTools is legacy — use only for historical reference or maintaining old sites!
