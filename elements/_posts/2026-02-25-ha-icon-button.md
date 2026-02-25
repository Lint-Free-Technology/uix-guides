---
title: ha-icon-button changes for 2026.3
excerpt_image: /assets/elements/2026-02-25-ha-icon-button.png
tags:
  - icon
  - button
---
Home Assistant 2026.3 changes `ha-icon-button` from using mdc button to webawesome (`ha-button`). This means that all uses of `--mdc-icon-button-size` need to change to `--ha-icon-button-size`.

Example:

```yaml
type: picture-glance
title: Kitchen
image: https://demo.home-assistant.io/stub_config/kitchen.png
entities:
  - entity: light.kitchen_lights
uix:
  style: |
    .wrapper {
      width: 70px;
    }
    ha-icon-button {
      --ha-icon-button-size: 70px;
      --mdc-icon-size: 54px;
      color: yellow !important;
    }
```

![example](/assets/elements/2026-02-25-ha-icon-button.png)