---
title: Getting shadowy with themes - using host/element selector
description: How to use host/element selector in themes to apply styling only to a specific element class type.
excerpt_image: /assets/elements/2026-03-29-getting-shadowy-with-themes-host-element-selector.png
tags:
  - badge
  - themes
---
When using UI eXtension themes, often you can carry out all your styling by simple CSS targeting on the hosts class type. For example, see [Styling Home Assistant 2026.3 energy now badges]({% post_url /elements/2026-03-02-energy-now-badge %}) which uses a CSS target of `:host(.type-power-total)`. However this will not work if you need to target an element directly in shadow root to target a property that is not styled with a CSS variable, or to inject keyframes into an element's light DOM.

Continuing to use the power now badge on the built-in energy dashboard, the example below will change the border of the badge to double. This can only be done by styling in shadow root as the `.badge` class styling does not expose a CSS variable for `border-style`. Border color and width are styled on `:host(.type-power-total)` on the root element styling key `.:`, showing a good example of using both root and specific yaml keys with UIX yaml selection.

{% include admonition.html type="info" title="Host/element path selector" body="Applying this guide uses the `&` [Host/element path selector](https://uix.lf.technology/concepts/dom/#hostelement-path-selection)" %}

{% raw %}

```yaml
Badge Theme:
  uix-theme: Badge Theme
  uix-badge-yaml: |
    .: |
      :host(.type-power-total) {
        --ha-card-border-width: 3px;
        --ha-card-border-color: red;
      }
    "&.type-power-total ha-badge $": |
      .badge {
        border-style: double !important;
      }
```

{% endraw %}

{% include admonition.html type="homeassistant" title="Styled power now badge" body="![Styled power now badge](/assets/elements/2026-03-29-getting-shadowy-with-themes-host-element-selector.png)" %}
