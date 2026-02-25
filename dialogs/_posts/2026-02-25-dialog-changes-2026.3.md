---
title: Dialog changes in Home Assistant 2026.3
tags:
  - dialogs
---
There are major changes to dialogs in Home Assistant 2026.3. Changes include:

- `ha-dialog` now a new element using webawesome `wa-dialog` component rather than mdc dialog. The final element used is the Browser's `<dialog>` which is display in the Browser's [Top layer](https://developer.mozilla.org/en-US/docs/Glossary/Top_layer).
- the interim `ha-wa-dialog` is now `ha-dialog` as per above
- a number of dialogs are now using the newer `ha-adaptive-dialog` which either uses `ha-dialog` for larger views, or `ha-bottom-sheet` for smaller views like mobiles.
- more-info dialog is now using `ha-adaptive-dialog`.

As dialog modding is only a relative newer feature of UIX, this may not affect you directly. However for those who jumped in and modded out more-info, or other dialogs, you wil need to adapt your modifications, especially for more-info dialog.

A start of the types of changes required are below. This list is not exhaustive as there will be many scenarios based on what you have modded:

- for dialogs that were using `ha-wa-dialog` in the interim, you should be able to change your modifications to update all use of `ha-wa-dialog` to `ha-dialog`.
- for dialogs that have migrated to `ha-adaptive-dialog`, you will need to account for this extra element in your yaml theme selectors PLUS additional theming for `ha-bottom-sheet`.

This post will be updated as further examples arise in the 2026.3.0 beta period.

**Additional Resource:** For more information on likely changes for `ha-dialog` see [Browser Mod Issue #1163](https://github.com/thomasloven/hass-browser_mod/issues/1163)
