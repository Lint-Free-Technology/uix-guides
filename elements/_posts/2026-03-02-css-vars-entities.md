---
title: Using custom CSS variables to simplify code across templates
excerpt_image: /assets/elements/2026-03-02-css-vars-entities.png
tags:
  - entities
  - card
  - templates
---
UI eXtension (UIX) templates are confined to a set of style rules, either the default style (string or `.:` key) or child style. There is no concept of variable sharing across templates, and it would be too inefficient for this to be coded into UIX with lots of tracking and regeneration of template to the backend when variables change.

Consider the following where you may wish to use a concept of `isDark` across multiple entities rows, but not all rows.

{% raw %}

```yaml
type: entities
entities:
  - entity: sun.sun
    uix:
      style: |
        {% set isDark = is_state('sun.sun','below_horizon') %}
        hui-generic-entity-row {
          background: {{ 'darkslateblue' if isDark else 'inherit' }};
          color: {{ 'slategrey' if isDark else 'inherit' }};
          --state-icon-color: {{ 'slategrey' if isDark else 'inherit' }};
        }
  - entity: sun.sun
    uix:
      style: |
        {% set isDark = is_state('sun.sun','below_horizon') %}
        hui-generic-entity-row {
          background: {{ 'yellow' if not isDark else 'inherit' }};
          color: {{ 'orange' if not isDark else 'inherit' }};
          --state-icon-color: {{ 'orange' if not isDark else 'inherit' }};
        }
```

{% endraw %}

The `isDark` calculation here is pretty simple. However, repeating what may be a complex template calculation twice can be quite repetitive and probe to error when you need to adjust.

One method to simplify this, and make it better, uses custom CSS variables on `:host` reducing the templates used from two to one.

{% raw %}

```yaml
type: entities
uix:
  style: |
    :host {
      {% set isDark = is_state('sun.sun','below_horizon') %}
      --darkslateblue-if-dark: {{ 'darkslateblue' if isDark else 'inherit' }};
      --slategrey-if-dark: {{ 'slategrey' if isDark else 'inherit' }};
      --yellow-if-not-dark: {{ 'yellow' if not isDark else 'inherit' }};
      --orange-if-not-dark: {{ 'orange' if not isDark else 'inherit' }};
    }
entities:
  - entity: sun.sun
    uix:
      style: |
        hui-generic-entity-row {
          background: var(--darkslateblue-if-dark);
          color: var(--slategrey-if-dark);
          --state-icon-color: var(--slategrey-if-dark);
        }
  - entity: sun.sun
    uix:
      style: |
        hui-generic-entity-row {
          background: var(--yellow-if-not-dark);
          color: var(--orange-if-not-dark);
          --state-icon-color: var(--orange-if-not-dark);
        }
```

{% endraw %}

{% include admonition.html type="homeassistant" title="Style entities rows using custom CSS variables" body="![Styled dialog](/assets/elements/2026-03-02-css-vars-entities.png)" %}
