---
title: Developer tools migration
excerpt_image: /assets/frontend/2026-07-08-developer-tools-migration.png
tags:
  - developer tools
  - tools
---
Starting in Home Assistant 2026.8, Developer Tools will be renamed to Tools. This change will impact UIX Styling using the theme item `uix-developer-tools(-yaml)`.

As the current Developer Tools panel (`ha-panel-developer-tools`) and new Tools panel (`ha-panel-tools`) are both config panels (`ha-panel-config`), which can be styled in theme with `uix-config(-yaml)`, the following changes will take place in UIX Styling.

1. The theme item `uix-developer-tools(-yaml)` will cease to apply in Home Assistant 2026.7 as `ha-developer-tools-panel` will cease to exist.
2. There will be **NO** direct replacement theme item.
3. The new Tools panel (`ha-panel-tools`) can be styled using `uix-config(-yaml)`.

You can prepare for this change now swapping out any existing `uix-developer-tools(-yaml)` theme item with a `uix-config(-yaml)` theme item as per below example theme code.

Existing theme example, changing card heading color on the YAML tab to red.

```yaml
  uix-developer-tools-yaml: |
    developer-yaml-config $ ha-card $: |
      :host {
        --ha-card-header-color: red;
      }
```

New theme code which will work prior to and after 2026.7 is released.

```yaml
  uix-config-yaml: |
    ha-panel-developer-tools,ha-panel-tools $:
      developer-yaml-config $ ha-card $: |
        :host {
          --ha-card-header-color: red;
        }
```

{% include admonition.html type="homeassistant" title="Home Assistant output" body="![example](/assets/frontend/2026-07-08-developer-tools-migration.png)" %}
