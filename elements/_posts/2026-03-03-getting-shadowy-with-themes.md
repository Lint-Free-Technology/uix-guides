---
title: Getting shadowy with themes
description: How to use templates in themes to apply styling only to a specific element config type.
excerpt_image: /assets/elements/2026-03-03-getting-shadowy-with-themes.png
tags:
  - badge
  - themes
  - templates
---
When using UI eXtension themes, often you can carry out all your styling by simple CSS targeting on the hosts class type. For example, see [Styling Home Assistant 2026.3 energy now badges](/elements/_posts/2026-03-02-energy-now-badge.md) which uses a CSS target of `:host(.type-power-now)`. However this will not work if you need to target an element directly in shadow Root to target a property that is not styled with a CSS variable, or to inject keyframes into an element's light DOM.

Continuing to use the power now badge on the built-in energy dashboard, the example below will change the border of the badge to double. This can only be done by styling in shadow Root as the `.badge` class styling does not expose a CSS variable for `border-style`. Border color and width are styled on `:host(.type-power-now)` on the root element styling key `.:` showing a good example of using both root and specific yaml keys with UIX yaml selection.

{% include admonition.html type="tip" title="Config variable in templates" body="Every UIX template includes the variable `config` which is the element's config. In all but very few cases, the config will include at least the element `type` as well as any user or strategy config. For this example. `config.type == 'power-total`" %}

{% raw %}

```yaml
Badge Theme:
  uix-theme: Badge Theme
  uix-badge-yaml: |
    .: |
      :host(.type-power-now) {
        --ha-card-border-width: 3px;
        --ha-card-border-color: red;
      }
    ha-badge $: |
      {% if config.type == 'power-total' %}
      .badge {
        border-color: red !important;
        border-width: 3px !important;
        border-style: double !important;
      }
      {% endif %}
```

{% endraw %}

{% include admonition.html type="homeassistant" title="Styled power now badge" body="![Styled power now badge](/assets/elements/2026-03-03-getting-shadowy-with-themes.png)" %}
