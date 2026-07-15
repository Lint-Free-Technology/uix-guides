---
title: Using UIX Forge more-info combining with UIX actions
description: A guide to using more-info spark together in a vertical stack with heading and badges using UIX actions
excerpt_image: /assets/forge/2026-07-15-forge-more-info-header.png
tags:
  - forge
  - sparks
  - more-info spark
  - actions
  - more-info action
---

Elements used:

- UIX Forge [more-info spark](https://uix.lf.technology/forge/sparks/more-info/)
- more-info [UIX action](https://uix.lf.technology/extras/uix-actions/#more-info-show-home-assistant-more-info-for-an-entity-with-starting-view)

A vertical-stack is used with a heading card containing badges that use [UIX actions](https://uix.lf.technology/extras/uix-actions/) to show specific more-info pages - history, settings and related.

The example yaml is for a grid section in a Sections dashboard.

```yaml
type: grid
cards:
  - type: vertical-stack
    cards:
      - type: heading
        icon: mdi:weather-partly-cloudy
        heading: Weather
        badges:
          - type: button
            icon: mdi:chart-box-outline
            tap_action:
              action: fire-dom-event
              uix:
                action: more-info
                data:
                  entity: weather.demo_weather_south
                  view: history
          - type: button
            icon: mdi:cog-outline
            tap_action:
              action: fire-dom-event
              uix:
                action: more-info
                data:
                  entity: weather.demo_weather_south
                  view: settings
          - type: button
            icon: mdi:information-outline
            tap_action:
              action: fire-dom-event
              uix:
                action: more-info
                data:
                  entity: weather.demo_weather_south
                  view: details
        tap_action:
          action: more-info
          entity: weather.demo_weather_south
        heading_style: title
      - type: custom:uix-forge
        forge:
          mold: card
          sparks:
            - type: more-info
              entity: weather.demo_weather_south

```

{% include admonition.html type="homeassistant" title="More-info spark in vertical stack with heading card and more-info action badges" body="![more-info spark in vertical stack with heading card and more-info action badges](/assets/forge/2026-07-15-forge-more-info-header.png)" %}
