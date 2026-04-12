---
title: Using UIX Forge tooltip and attribute sparks for tooltips
description: A guide to adding and customising tooltips with UIX Forge tooltip and attribute sparks
excerpt_image: /assets/forge/2026-04-12-forge-tooltip-spark.png
tags:
  - forge
  - sparks
  - tooltip spark
  - attribute spark
---
[UIX Forge](https://uix.lf.technology/forge) allows you to forge an element and apply various features with [forge sparks](https://uix.lf.technology/forge/sparks). This guide uses the [attribute spark](https://uix.lf.technology/forge/sparks/attribute) and the [tooltip spark](https://uix.lf.technology/forge/sparks/tooltip) to add rich, customisable tooltips to Home Assistant cards and elements.

{% include admonition.html type="info" title="Forge elements" body="All UIX Forge documentation will describe the card, row, badge, section, picture-element as **element** as indeed, a forged element is not restricted to being a card, but can be any type supported by UIX Forge mold type" %}

The [attribute spark](https://uix.lf.technology/forge/sparks/attribute) lets you set or remove HTML attributes on elements inside a forged element's shadow DOM. The [tooltip spark](https://uix.lf.technology/forge/sparks/tooltip) adds a fully featured tooltip — with placement, delay, skidding, and CSS control — powered by UIX Forge.

## Scenario 1: Adjust a title attribute with the attribute spark

A browser will display a native tooltip for any element that has a `title` attribute. The [attribute spark](https://uix.lf.technology/forge/sparks/attribute) can target an element by CSS selector and change its `title` attribute to any value you choose.

In the example below a tile card is forged and the attribute spark targets the inner `ha-card` element. The `title` attribute is set to a custom string which will appear as the browser's native tooltip when the card is hovered.

```yaml
type: custom:uix-forge
forge:
  mold: card
  sparks:
    - type: attribute
      selector: ha-card
      attribute: title
      value: "Customised native tooltip text"
element:
  type: tile
  entity: sun.sun
```

{% include admonition.html type="homeassistant" title="Home Assistant output — adjusted title tooltip" body="![attribute spark adjusting title attribute](/assets/forge/2026-04-12-forge-tooltip-spark-1.png)" %}

## Scenario 2: Remove the title attribute and add the tooltip spark

Native browser tooltips have limited styling and behaviour options. A better approach is to use the [attribute spark](https://uix.lf.technology/forge/sparks/attribute) to remove the existing `title` attribute first, then add the [tooltip spark](https://uix.lf.technology/forge/sparks/tooltip) to provide a fully featured replacement.

In this example the attribute spark removes the `title` attribute from the `ha-card` element, then the tooltip spark adds a custom tooltip with its own content.

```yaml
type: custom:uix-forge
forge:
  mold: card
  sparks:
    - type: attribute
      selector: ha-card
      attribute: title
      remove: true
    - type: tooltip
      content: "This is a UIX Forge tooltip"
element:
  type: tile
  entity: sun.sun
```

{% include admonition.html type="homeassistant" title="Home Assistant output — tooltip spark replacing native title" body="![tooltip spark replacing native title attribute](/assets/forge/2026-04-12-forge-tooltip-spark-2.png)" %}

{% include admonition.html type="tip" title="Removing the title attribute first" body="Always remove the native `title` attribute before adding the tooltip spark to avoid both appearing at the same time." %}

## Scenario 3: Adjust tooltip show and hide delay times

The tooltip spark provides `show_delay` and `hide_delay` options (in milliseconds) to control how quickly the tooltip appears and disappears. This is useful when tooltips should only show after intentional hover, or should linger longer after the cursor leaves.

```yaml
type: custom:uix-forge
forge:
  mold: card
  sparks:
    - type: attribute
      selector: ha-card
      attribute: title
      remove: true
    - type: tooltip
      content: "I appear after a short pause and stay a little longer"
      show_delay: 600
      hide_delay: 300
element:
  type: tile
  entity: sun.sun
```

{% include admonition.html type="homeassistant" title="Home Assistant output — tooltip with custom show and hide delays" body="![tooltip spark with custom show and hide delays](/assets/forge/2026-04-12-forge-tooltip-spark-3.png)" %}

{% include admonition.html type="tip" title="Delay tips" body="A `show_delay` of 400–600 ms is a good starting point for cards where you want to avoid the tooltip flashing during normal interaction. Use a small `hide_delay` (100–200 ms) to let the cursor move away without the tooltip feeling sticky." %}

## Scenario 4: Rich CSS styles, placement, and skidding

The tooltip spark also supports placement control and positional fine-tuning with `placement`, `skidding`, and `distance` options. These allow you to position the tooltip relative to the element and nudge it along or away from the element. Custom CSS can be applied with the `style` option to create rich visual tooltip designs.

The supported placements are `top`, `bottom`, `left`, and `right` (with optional `-start` and `-end` variants such as `top-start` or `bottom-end`).

```yaml
type: custom:uix-forge
forge:
  mold: card
  sparks:
    - type: attribute
      selector: ha-card
      attribute: title
      remove: true
    - type: tooltip
      content: "Rich styled tooltip — bottom right"
      placement: bottom-end
      skidding: 10
      distance: 8
      show_delay: 400
      hide_delay: 150
      style: |
        background: linear-gradient(135deg, #1a1a2e, #16213e);
        color: #e0e0ff;
        border: 1px solid #4a4aff;
        border-radius: 8px;
        padding: 8px 14px;
        font-size: 0.85em;
        box-shadow: 0 4px 16px rgba(74, 74, 255, 0.4);
element:
  type: tile
  entity: sun.sun
```

{% include admonition.html type="homeassistant" title="Home Assistant output — richly styled tooltip with custom placement" body="![tooltip spark with rich styles and custom placement](/assets/forge/2026-04-12-forge-tooltip-spark-4.png)" %}

{% include admonition.html type="tip" title="Placement and skidding" body="`skidding` shifts the tooltip along the axis of the placement edge (e.g. left/right for `top` or `bottom` placements). `distance` controls how far away from the element the tooltip appears. Both accept positive and negative values." %}
