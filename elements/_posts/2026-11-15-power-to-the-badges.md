---
title: Power to the badges
description: How to use forge and sparks to modify all three elements of a heading badge
excerpt_image: /assets/elements/2026-11-15-badges.png
tags: 
  - badge
  - forge
  - sparks
---

The heading badge only has three elements but can show key information in very little space. As standard however it allows little customisation, we can override `name`, choose an `icon` and choose the icon `color`. We cannot change the state and we cannot use templates. In this guide we will show how to add templating capability to all three elements (icon, name and state).

The badges below show the current temperature as reported by a weather service, the first one is a standard badge.

{% include admonition.html type="homeassistant" title="Standard and modified heading badges" body="![Standard and modified weather badges](/assets/elements/2026-11-15-badges.png)" %}

UIX can forge `name` and `icon` and add template capability to both, but not the state because the badge has no entry key for the state. We can get around this limitation by using the search spark, which can look for a specific text and change it into a different text (which can be a template). For this to work the state needs to be a fixed string so the search spark knows what to look for. The only way to achieve this is by setting `state_content: name` and setting this to a fixed string `name: LookForThis`. Take a look at the second badge to see what this achieves.

Now we can add two sparks to change both the state and the name to something else, in this example:
- The state shows the current temperature, unless current wind speed is 40 or higher, in which case we show wind speed
- We show the (abbreviated) name of the weather institute, unless it issued a warning for severe weather, in which case we show the warning 

{% raw %}

```YAML
type: custom:uix-forge
forge:
  mold: badge
  sparks:
    - type: search
      for: hui-entity-badge $
      query: state-display
      actions:
        replace_text:
          find: LookForThis
          replace: >
            {% if not states('sensor.tulpenlaan_current_temperature') in
            ['unavailable', 'unknown'] %}
              {% if states('sensor.tulpenlaan_current_wind_speed') | float(0) < 40 %}          
                {{ states('sensor.tulpenlaan_current_temperature', with_unit=true) }}
              {% else %}
                {{ states('sensor.tulpenlaan_current_wind_speed') | float(0) | round(0) ~ ' kph'}}
              {% endif %}
            {% else %}
              {{ ' °C' }}      
            {% endif %}
    - type: search
      for: hui-entity-badge $ ha-badge $
      query: span.label
      actions:
        replace_text:
          find: LookForThis
          replace: >
            {% set warnings =
            state_attr('binary_sensor.weather_warning_tulpenlaan',
              'active_warnings_friendly_names') | lower %}
            {% if warnings == "" %}  {{ 'KMI' }}   {% else %}    {{
            warnings[0:9] }} {% endif %}
element:
  type: entity
  entity: sensor.tulpenlaan_current_temperature
  state_content: name
  show_name: true
  name: LookForThis
```

{% endraw %}

{% include admonition.html type="tip" title="DOM navigation" body="To learn more on how to find where the spark should search refer see <a href='https%3A%2F%2Fuix.lf.technology%2Fconcepts%2Fdom%2F%23uix_style_path0-specific-helper'>UIX Docuemntation</a>" %}

Next, we will dynamically change the icon based on the current weather (this requires a template sensor which gets its data from your favourite weather integration using `action: weather.get_forecasts`). This does not require a spark, we can template `icon` directly and add the following

{% raw %}

```YAML
  icon: |-
    {%
     set condition = state_attr('sensor.tulpenlaan_forecast_hourly', 'forecast') | selectattr('datetime', '>', (now() - timedelta(hours=0.5)).isoformat()) | 
    selectattr('datetime', '<=',  (now() + timedelta(hours=0.5)).isoformat()) | 
    map(attribute='condition') | list %}
    {%
     set day = state_attr('sensor.tulpenlaan_forecast_hourly', 'forecast') | selectattr('datetime', '>', now().isoformat()) | 
    selectattr('datetime', '<=',  (now() + timedelta(hours=1)).isoformat()) | 
    map(attribute='is_daytime') | list %}
    {% if condition == ['cloudy'] %}
    {{ 'local:material-symbols-light--cloud-outline-rounded' }}
    {% elif condition == ['partlycloudy'] and day == [true] %}
    {{ 'local:material-symbols-light--partly-cloudy-day-outline-rounded' }}
    {% elif condition == ['partlycloudy'] and day == [false] %}
    {{ 'local:material-symbols-light--partly-cloudy-night-outline-rounded' }}
    {% elif condition == ['sunny'] %}
    {{ 'local:material-symbols-light--wb-sunny-outline-rounded' }}
    {% elif condition == ['partly-rainy'] %}
    {{ 'local:material-symbols-light--rainy-light-outline-rounded' }}
    {% elif condition == ['rainy'] %}
    {{ 'local:material-symbols-light--rainy-outline-rounded' }}
    {% elif condition == ['pouring'] %}
    {{ 'local:material-symbols-light--rainy-heavy-outline-rounded' }}
    {% elif condition == ['clear-night'] %}
    {{ 'local:material-symbols-light--moon-stars-outline-rounded' }}
    {% elif condition == ['partly-snowy'] %}
    {{ 'local:material-symbols-light--sunny-snowing-outline-rounded' }}
    {% elif condition == ['snowy'] %}
    {{ 'local:material-symbols-light--weather-snowy-outline-rounded' }}
    {% elif condition == ['fog'] %}
    {{ 'local:material-symbols-light--mist-outline-rounded' }}
    {% elif condition == ['hail'] %}
    {{ 'local:material-symbols-light--weather-hail-outline-rounded' }}
    {% elif condition == ['lightning'] %}
    {{ 'local:material-symbols-light--thunderstorm-outline-rounded' }}
    {% elif condition == ['lightning-rainy'] %}
    {{ 'local:material-symbols-light--thunderstorm-outline-rounded' }}
    {% elif condition == ['snowy-rainy'] %}
    {{ 'local:material-symbols-light--weather-snowy-outline-rounded' }}
    {% elif condition == ['windy'] %}
    {{ 'local:material-symbols-light--air-outline-rounded' }}
    {% elif condition == ['windy-variant'] %}
    {{ 'local:material-symbols-light--air-outline-rounded' }}
    {% elif condition == ['exceptional'] %}
    {{ 'local:material-symbols-light--cyclone-outline-rounded' }}
    {% else %}
    {{ 'local:material-symbols-light--partly-cloudy-day-outline-rounded' }}
    {% endif %}
```

{% endraw %}

{% include admonition.html type="tip" title="Icons" body="The example above uses material-symbols-light icons, but you can use whatever you prefer; the default MDI icon set also includes all weather symbols." %}

With this the badge looks like the third one above, and all three elements change dynamically. To get to the fourth, which changes the text color for warnings to orangered, we need to add one more thing

{% raw %}

```YAML
  uix:
    style:
      ha-badge $: >

        {% if  states('binary_sensor.weather_warning_tulpenlaan') not in ['off',
        'unavailable', 'unknown'] %}
          .label, slot[name="name"] {
            color: orangered !important;
          }
        {% endif %}
```

{% endraw %}
