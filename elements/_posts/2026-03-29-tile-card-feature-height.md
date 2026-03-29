---
title: Tile card feature height
description: Styling tile card feature height. A guide on using uix_path() for finding yaml paths for styling locally and using themes.
excerpt_image: /assets/elements/2026-03-29-tile-card-feature-height.png
tags:
  - tile
  - card
  - themes
  - uix_path
---
Tile card features have a height which is a CSS var `--feature-height`. This is set on the feature element itself, `hui-card-feature`, which is in shadow root of `hui-card-features`. Below is a step by step guide on using [`uix_style_path()`](https://uix.lf.technology/concepts/dom/#uix_style_path0-specific-helper) to discover yaml selector to cross the shadow root for styling with UIX.

## Step 1: find feature needing styling

Use your browser to inspect the DOM and find the relevant feature whose height you wish to style.

The screenshot below shows `hui-card-feature` and that it indeed sets `--feature-height: 42px;`.

![DOM screenshot](/assets/elements/2026-03-29-tile-card-feature-height-1.png)

## Step 2: run uix_style_path/uix_path

With `hui-card-feature` selected in browser's inspector, run `uix_style_path($0)` (`uix_path()` is shorthand for `uix_style_path`).

![DOM screenshot](/assets/elements/2026-03-29-tile-card-feature-height-2.png)

## Step 3a: style tile card locally

From the `uix_style_path()` output take the 📝 Boilerplate UIX YAML and use to style tile card locally on dashboard.

📝 Boilerplate UIX YAML

```yaml
uix:
  style:
    "hui-card-features $": |
      hui-card-feature {
        /* your styles for hui-card-feature */
      }
```

Tile card styling

```yaml
type: tile
entity: light.bed_light
name:
  type: entity
vertical: false
features_position: bottom
grid_options:
  columns: 12
  rows: 1
features:
  - type: light-brightness
uix: # Included from Boilerplate UIX YAML, filling in desired styling
  style:
    "hui-card-features $": |
      hui-card-feature {
        --feature-height: 20px;
      }
```

## Step 3b: style tile card via theme

From the `uix_style_path()` output take the 📝 Boilerplate Theme YAML and use to create a new theme or add to an existing theme already set up for UIX styling. If you already have a theme you would just take the `uix-card-yaml:` section.

{% include admonition.html type="tip" title="Merging UIX styling" body="If you already have `uix-card:` theme section and need to migrate to `uix-card-yaml` you need to place any existing under the root key `.:`." %}

📝 Boilerplate Theme YAML

```yaml
my-awesome-theme:
  uix-theme: my-awesome-theme
  uix-card-yaml: |
    "hui-card-features $": |
      hui-card-feature {
        /* your styles for hui-card-feature */
      }
```

Theme styling in existing theme

```yaml
UIX Test:
  uix-theme: UIX Test

  uix-card-yaml: |
    "hui-card-features $": |
      hui-card-feature {
        --feature-height: 20px;
      }
```

{% include admonition.html type="homeassistant" title="Styled tile card feature height" body="![Styled tile card feature height](/assets/elements/2026-03-29-tile-card-feature-height.png)" %}
