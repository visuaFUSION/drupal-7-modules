# CTools Modal Accessibility Patches

## Status: Not Applied (Available for Future Use)

These patches improve modal dialog accessibility but were not applied due to their complexity and unofficial status. They are documented here for future consideration.

---

## Patch Chain (Must Be Applied in Order)

### 1. Modal Accessibility (#3342360)
**URL:** https://www.drupal.org/project/ctools/issues/3342360
**Version:** 7.x-1.15
**Status:** Needs review
**Patch:** `add-keydown-modal-close-3342360-8.patch`

**Changes:**
- Adds `Drupal.CTools.Modal.trigger` to track element that opened modal
- Adds `Drupal.CTools.Modal.originalBodySiblings` for aria-hidden management
- Adds `role="dialog"` and `aria-labelledby="modal-title"` to modal container
- Adds `tabindex="-1"` to modal for programmatic focus
- Adds keydown handler for close button (Enter/Space keys)
- Changes modal title from `<span>` to `<h2>` for semantic HTML
- Adds `role="button"` to close link
- Manages `aria-hidden` on body siblings when modal is open
- Initial focus now on dialog container instead of close button
- Restores focus to trigger element when modal closes

---

### 2. modalTabTrapHandler Refactor (#3387958)
**URL:** https://www.drupal.org/project/ctools/issues/3387958
**Version:** 7.x-1.x-dev
**Status:** Needs review
**Patch:** `modalTabTrapHandler-refactor-function-3387958-4.patch`
**Depends on:** #3342360

**Changes:**
- Moves `modalTabTrapHandler` out of `modalContent` function scope
- Makes it accessible as `Drupal.CTools.Modal.modalTabTrapHandler`
- Allows external JS to properly unbind the handler
- Refactors several internal functions to module scope
- General code cleanup and reorganization

**Why needed:**
The original `modalTabTrapHandler` was defined inside `modalContent()`, making it impossible to unbind from external modules. Calling `$('body').unbind('keydown', Drupal.CTools.Modal.modalContent.modalTabTrapHandler)` would unbind ALL keydown handlers because the function reference was undefined.

---

### 3. Modal Stacking (#3420490)
**URL:** https://www.drupal.org/project/ctools/issues/3420490
**Version:** 7.x-1.21
**Status:** Needs review
**Patch:** `ctools_stack_modal-3420490-5.patch`
**Depends on:** #3387958

**Changes:**
- Adds ability to stack modals (open modal from within modal)
- Saves previous modal to hidden div (preserving event handlers)
- Restores previous modal when current one closes
- Enabled via flag, not automatic for all modals

**Use case:**
Node edit form in ctools modal with an Inline Entity Form (IEF) field that also opens a ctools modal to select values.

---

## Why Not Applied

1. **Complex dependency chain** - Each patch depends on the previous
2. **Unofficial status** - All patches still "Needs review" on drupal.org
3. **Version mismatch** - Patches target different versions (1.15, 1.x-dev, 1.21)
4. **Extensive changes** - Combined patches modify 600+ lines of JavaScript
5. **Risk assessment** - CTools is foundational; breaking modals affects many modules

---

## How to Apply (If Needed)

```bash
# From the ctools module directory
cd ctools-7.x-2026.03/ctools

# Apply in order:
patch -p1 < /path/to/add-keydown-modal-close-3342360-8.patch
patch -p1 < /path/to/modalTabTrapHandler-refactor-function-3387958-4.patch
patch -p1 < /path/to/ctools_stack_modal-3420490-5.patch
```

**Test thoroughly after applying:**
- Modal open/close functionality
- Keyboard navigation (Tab, Shift+Tab, Escape, Enter, Space)
- Focus management (focus trap, focus restoration)
- Screen reader announcements
- Nested modals (if using #3420490)

---

## Related Issues

- **Original modal focus issue:** Focus was on close button; WAI-ARIA recommends dialog container
- **Keyboard trap:** Users could Tab out of modal to background elements
- **Focus loss:** Focus not restored to trigger element after modal close
- **Screen readers:** Missing ARIA attributes for proper announcements
