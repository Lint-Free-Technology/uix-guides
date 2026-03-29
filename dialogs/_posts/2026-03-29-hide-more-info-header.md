---
title: Hide more-info dialog header
description: How to hide the more-info dialog header since Home Assistant 2026.3.0
excerpt_image: /assets/dialogs/2026-03-29-hide-more-info-header.png
tags:
  - dialogs
---

Since Home Assistant 2026.3.0, more-info dialog uses an adaptive dialog (`ha-adaptive-dialog`), which is includes either a standard dialog (`ha-dialog`) on larger screens or a bottom sheet (`ha-bottom-sheet`) on smaller screens. This guides shows how to target each type of dialog in order to hide the header.

In both cases, the parent dialog element is `ha-adaptive-dialog`. For more-info dialog UIX is applied in the light DOM of the adaptive dialog (`ha-adaptive-dialog`). To reach either dialog crossing of a shadow root `$` is required.

When the more-info dialog is `ha-dialog`, the full header item, `ha-dialog-header`, is in a slot in `wa-dialog`, which itself is in a shadow root of `ha-dialog`. The components used in `ha-dialog-header` are in slots in `ha-dialog` so styling these would not need crossing into `ha-dialog` shadow root.

When more-info is a bottom sheet (`ha-bottom-sheet`) the full header item, `ha-dialog-header`, is in a slot of `ha-bottom-sheet`.

Theme code hiding the more-info dialog header is shown below.

```yaml
UIX Theme:
  uix-theme: UIX Theme

  uix-more-info-yaml: |
    "$":
      .: |
        ha-bottom-sheet slot:nth-of-type(1) ha-dialog-header
        {
          display: none;
        }
      "ha-dialog $": |
        wa-dialog slot:nth-of-type(1) ha-dialog-header {
          display: none;
        }
```

{% include admonition.html type="homeassistant" title="More-info dialog with header removed" body="![Screenshot of Home Assistant fullscreen web browser media player dialog](/assets/dialogs/2026-03-29-hide-more-info-header.png)" %}
