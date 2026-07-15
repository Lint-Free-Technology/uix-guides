---
title: Styling adaptive popover dialogs - date picker example
description: Using UIX Styling with dialog theme to style date picker adaptive popover
excerpt_image: /assets/dialogs/2026-07-15-adaptive-popover-date-picker.png
tags:
  - dialogs
  - date picker
---
Home Assistant Frontend 2026.5 brought in a new adaptive popover dialog. It is like standard dialogs but on desktop shows a smaller dialog in place targeted to the element using the dialog, and on mobile uses a bottom sheet. The date picker dialog now uses adaptive popover dialog.

UI eXtension can style the adaptive popover using `uix-dialog-yaml` theming.

The example below shows an entities row with a date entity which will show the adaptive popover. The theme styling sets selected date(s) to red, and hover to red with opacity of 0.2. The theme yaml selector uses UIX Styling [Host/element path selection](https://uix.lf.technology/concepts/dom/#hostelement-path-selection) to only target dialogs of `type-dialog-date-picker`.

```yaml
uix-date-picker-selection: # theme name
  uix-theme: uix-date-picker-selection # setting UIX theme to theme name

  uix-dialog-yaml: |
    "&.type-dialog-date-picker": |
      calendar-month::part(range-inner),
      calendar-month::part(range-start),
      calendar-month::part(range-end),
      calendar-month::part(selected),
      calendar-month::part(selected):hover,
      calendar-month:not(.dummy)::part(button selected):hover {
        background-color: red !important;
      }
      calendar-month::part(button):hover {
        background-color: rgba(255, 0, 0, 0.2) !important;
      }
```

{% include admonition.html type="homeassistant" title="Styling date picker adaptive popover dialog" body="![Styling date picker adaptive popover dialog](/assets/dialogs/2026-07-15-adaptive-popover-date-picker.png)" %}
