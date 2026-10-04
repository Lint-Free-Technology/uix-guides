---
title: Map color tokens
description: Ready-to-use light and dark map color token palettes for Home Assistant themes.
excerpt_image: /assets/frontend/2026-10-04-map-tokens-osm.png
tags:
  - maps
  - themes
  - colors
---

Home Assistant 2026.10.0 adds theme tokens for the vector map. They let a theme recolor the map independently of the dashboard's light or dark mode—useful when, for example, a light theme needs the higher contrast of a dark map.

The tokens are based on the [map-style feature](https://github.com/home-assistant/frontend/pull/54477). The palettes below correspond to the bundled `default`, `colorful`, `natural`, `muted`, `gray`, and `toner` map styles in Home Assistant Frontend 2026.10.0.

{% include admonition.html type="tip" title="Theme YAML uses names without --" body="Use <code>ha-color-map-land</code> in a theme. Home Assistant exposes it to the map as the CSS custom property <code>--ha-color-map-land</code>." %}

## The available tokens

| Theme key | colors on the map |
| --- | --- |
| `ha-color-map-land` | Background and land |
| `ha-color-map-water` | Water |
| `ha-color-map-green` | Parks, woods, grass, leisure areas, wetlands, and sports grounds |
| `ha-color-map-area` | Residential, commercial, industrial, agricultural, parking, sand, rock, and similar land-use areas |
| `ha-color-map-building` | Building fill |
| `ha-color-map-building-outline` | Building outline |
| `ha-color-map-road` | Streets |
| `ha-color-map-road-major` | Motorways and trunk roads |
| `ha-color-map-road-outline` | Road outlines |
| `ha-color-map-transit` | Rail, subway, cycle, and foot routes |
| `ha-color-map-boundary` | Administrative and disputed boundaries |
| `ha-color-map-label` | Main place and road labels |
| `ha-color-map-label-halo` | Halo behind main labels |
| `ha-color-map-label-secondary` | POI, symbol, and house-number labels |

### What “curated equivalent” means

The bundled map styles have 45 individual color slots. Theme tokens expose 14 intentionally broader controls instead: for example, `ha-color-map-green` simultaneously colors parks, woods, grass, leisure areas, wetlands, and sports grounds. A single token therefore cannot preserve every separate green shade from the original `natural` or `colorful` palette.

The palette blocks below are **curated equivalents**. Each takes a representative color from the corresponding bundled style and applies it consistently to the feature group controlled by that token. This preserves the style's overall character while giving themes a compact, practical palette to copy and customise. Use `map_style: natural` (or another named style) on a card when an exact, feature-by-feature rendition of the bundled cartography is required.

## Add a palette to a theme

Add one of the blocks below under the name of your theme. The page theme mode does not change these values: paste the **dark** block to retain a dark map in a light theme, or paste the **light** block for the opposite effect.

```yaml
My map theme:
  # Paste one complete light or dark palette here.
  ha-color-map-land: "#f4efe6"
```

{% include admonition.html type="warning" title="These are theme-wide" body="Map tokens affect every vector map while the theme is active. For a one-card adjustment, use the map card's <code>map_style</code> configuration instead." %}

## Default

Home Assistant's shipped default map: a warm, restrained palette built on `colorful`.

### Default — light

```yaml
  ha-color-map-land: "#f4efe6"
  ha-color-map-water: "#bcd9e8"
  ha-color-map-green: "#cfe1bf"
  ha-color-map-area: "#efe8dc"
  ha-color-map-building: "#e7ddca"
  ha-color-map-building-outline: "#dcccb2"
  ha-color-map-road: "#fcfaf8"
  ha-color-map-road-major: "#ebd4ab"
  ha-color-map-road-outline: "#e6dac7"
  ha-color-map-transit: "#e9dfce"
  ha-color-map-boundary: "#d6c3a4"
  ha-color-map-label: "#4a463d"
  ha-color-map-label-halo: "#faf8f5cc"
  ha-color-map-label-secondary: "#8d8676"
```

### Default — dark

```yaml
  ha-color-map-land: "#191b2c"
  ha-color-map-water: "#27357a"
  ha-color-map-green: "#28504b"
  ha-color-map-area: "#1d2034"
  ha-color-map-building: "#21243c"
  ha-color-map-building-outline: "#2a2e4a"
  ha-color-map-road: "#2b3052"
  ha-color-map-road-major: "#454d7d"
  ha-color-map-road-outline: "#1a1d33"
  ha-color-map-transit: "#2c3150"
  ha-color-map-boundary: "#3b4068"
  ha-color-map-label: "#e7ecf8"
  ha-color-map-label-halo: "#12141fcc"
  ha-color-map-label-secondary: "#959dbd"
```

## Colorful

The unmodified VersaTiles `colorful` cartography: high contrast and noticeably colored roads, water, and land use.

### Colorful — light

```yaml
  ha-color-map-land: "#f8f4f0"
  ha-color-map-water: "#bfd9f2"
  ha-color-map-green: "#cdd9a9"
  ha-color-map-area: "#f5f1ed"
  ha-color-map-building: "#f2eae2"
  ha-color-map-building-outline: "#dfdbd7"
  ha-color-map-road: "#ffffff"
  ha-color-map-road-major: "#ffcc88"
  ha-color-map-road-outline: "#cfcdca"
  ha-color-map-transit: "#b1bbc4"
  ha-color-map-boundary: "#a6a6c8"
  ha-color-map-label: "#333344"
  ha-color-map-label-halo: "#ffffffcc"
  ha-color-map-label-secondary: "#66626a"
```

### Colorful — dark

```yaml
  ha-color-map-land: "#282725"
  ha-color-map-water: "#0c1c2a"
  ha-color-map-green: "#383f1f"
  ha-color-map-area: "#2b2826"
  ha-color-map-building: "#312c27"
  ha-color-map-building-outline: "#393734"
  ha-color-map-road: "#525252"
  ha-color-map-road-major: "#694710"
  ha-color-map-road-outline: "#353432"
  ha-color-map-transit: "#474e54"
  ha-color-map-boundary: "#575770"
  ha-color-map-label: "#dedef0"
  ha-color-map-label-halo: "#000000cc"
  ha-color-map-label-secondary: "#9e9ba2"
```

## Natural

An earthy palette with blue water, greens that stand out, and warm road and building colors.

### Natural — light

```yaml
  ha-color-map-land: "#f2edde"
  ha-color-map-water: "#a6cbed"
  ha-color-map-green: "#bbcb87"
  ha-color-map-area: "#eee8e3"
  ha-color-map-building: "#ebe0d4"
  ha-color-map-building-outline: "#d2cdc7"
  ha-color-map-road: "#f7f7f7"
  ha-color-map-road-major: "#f8c581"
  ha-color-map-road-outline: "#c8c6c3"
  ha-color-map-transit: "#abb5be"
  ha-color-map-boundary: "#a0a0c2"
  ha-color-map-label: "#2e2e3f"
  ha-color-map-label-halo: "#ffffffcc"
  ha-color-map-label-secondary: "#625e66"
```

### Natural — dark

```yaml
  ha-color-map-land: "#272725"
  ha-color-map-water: "#01172b"
  ha-color-map-green: "#3d4614"
  ha-color-map-area: "#2c2925"
  ha-color-map-building: "#342e27"
  ha-color-map-building-outline: "#3e3b37"
  ha-color-map-road: "#525252"
  ha-color-map-road-major: "#694710"
  ha-color-map-road-outline: "#353432"
  ha-color-map-transit: "#474e54"
  ha-color-map-boundary: "#575770"
  ha-color-map-label: "#dedef0"
  ha-color-map-label-halo: "#000000cc"
  ha-color-map-label-secondary: "#9e9ba2"
```

## Muted

A quieter version of the colorful map, with desaturated roads and land use.

### Muted — light

```yaml
  ha-color-map-land: "#f4f0ee"
  ha-color-map-water: "#d0dde9"
  ha-color-map-green: "#d6dcc5"
  ha-color-map-area: "#f0eeec"
  ha-color-map-building: "#eeeae6"
  ha-color-map-building-outline: "#e1dfdd"
  ha-color-map-road: "#f9f9f9"
  ha-color-map-road-major: "#f1d3ab"
  ha-color-map-road-outline: "#d2d1cf"
  ha-color-map-transit: "#bcc2c7"
  ha-color-map-boundary: "#b1b2c6"
  ha-color-map-label: "#41414c"
  ha-color-map-label-halo: "#ffffffcc"
  ha-color-map-label-secondary: "#6e6c71"
```

### Muted — dark

```yaml
  ha-color-map-land: "#272726"
  ha-color-map-water: "#181f27"
  ha-color-map-green: "#343829"
  ha-color-map-area: "#292827"
  ha-color-map-building: "#2d2b28"
  ha-color-map-building-outline: "#333231"
  ha-color-map-road: "#494949"
  ha-color-map-road-major: "#574328"
  ha-color-map-road-outline: "#323130"
  ha-color-map-transit: "#42464a"
  ha-color-map-boundary: "#4e4e5d"
  ha-color-map-label: "#c6c6d1"
  ha-color-map-label-halo: "#000000cc"
  ha-color-map-label-secondary: "#908e92"
```

## Gray

An achromatic map that keeps attention on markers and labels.

### Gray — light

```yaml
  ha-color-map-land: "#f5f5f5"
  ha-color-map-water: "#d7d7d7"
  ha-color-map-green: "#eaeaea"
  ha-color-map-area: "#f2f2f2"
  ha-color-map-building: "#e9e9e9"
  ha-color-map-building-outline: "#dcdcdc"
  ha-color-map-road: "#fafafa"
  ha-color-map-road-major: "#d6d6d6"
  ha-color-map-road-outline: "#e0e0e0"
  ha-color-map-transit: "#d3d3d3"
  ha-color-map-boundary: "#999999"
  ha-color-map-label: "#2c2c2c"
  ha-color-map-label-halo: "#ffffffcc"
  ha-color-map-label-secondary: "#5f5f5f"
```

### Gray — dark

```yaml
  ha-color-map-land: "#272727"
  ha-color-map-water: "#000000"
  ha-color-map-green: "#323232"
  ha-color-map-area: "#292929"
  ha-color-map-building: "#2f2f2f"
  ha-color-map-building-outline: "#373737"
  ha-color-map-road: "#393939"
  ha-color-map-road-major: "#3a3a3a"
  ha-color-map-road-outline: "#2c2c2c"
  ha-color-map-transit: "#383838"
  ha-color-map-boundary: "#666666"
  ha-color-map-label: "#ededed"
  ha-color-map-label-halo: "#000000cc"
  ha-color-map-label-secondary: "#a2a2a2"
```

## Toner

A crisp, high-contrast style: mostly white in light mode, nearly black in dark mode, with strongly defined transport features.

### Toner — light

```yaml
  ha-color-map-land: "#ffffff"
  ha-color-map-water: "#d8e7f7"
  ha-color-map-green: "#dfe7ca"
  ha-color-map-area: "#fffcfa"
  ha-color-map-building: "#fbf6f2"
  ha-color-map-building-outline: "#eceae7"
  ha-color-map-road: "#ffffff"
  ha-color-map-road-major: "#f2b561"
  ha-color-map-road-outline: "#b5b3af"
  ha-color-map-transit: "#87929c"
  ha-color-map-boundary: "#727197"
  ha-color-map-label: "#000000"
  ha-color-map-label-halo: "#ffffffcc"
  ha-color-map-label-secondary: "#3e3e3e"
```

### Toner — dark

```yaml
  ha-color-map-land: "#121211"
  ha-color-map-water: "#161f27"
  ha-color-map-green: "#262a19"
  ha-color-map-area: "#161413"
  ha-color-map-building: "#1c1916"
  ha-color-map-building-outline: "#252322"
  ha-color-map-road: "#6d6d6d"
  ha-color-map-road-major: "#895d18"
  ha-color-map-road-outline: "#33312f"
  ha-color-map-transit: "#5d656d"
  ha-color-map-boundary: "#7c7c9b"
  ha-color-map-label: "#ffffff"
  ha-color-map-label-halo: "#000000cc"
  ha-color-map-label-secondary: "#c4c4c4"
```

## Tweak from a known base

Copy a complete palette first, then replace only the keys you need. For example, this starts with the dark `colorful` palette and makes water and motorways more vivid:

```yaml
Colorful dark, blue water:
  # Include the dark Colorful palette above, then override these values.
  ha-color-map-water: "#103b66"
  ha-color-map-road-major: "#9a6217"
```

Theme values may use any CSS color Home Assistant can resolve, including `rgb()`, `hsl()`, named colors, and values built from other theme variables. Keep the alpha component on `ha-color-map-label-halo` where possible: it preserves the intended relationship between labels and the map beneath them.
