---
layout: home-no-banner
title: Home
---

# Welcome to UI eXtension Guides

Welcome to UI eXtension Guides! This site is your comprehensive resource for learning about and mastering [UI eXtension Styling](https://uix.lf.technology/using/) (UIX Styling), [UI eXtension Forge](https://uix.lf.technology/forge/) (UIX Forge) and [UI eXtension Broker](https://uix.lf.technology/broker) (UIX Broker), powerful tools for customizing Home Assistant dashboards.

## What is UIX Styling?

UIX Styling allows you to apply custom CSS styling to (almost) every UI element of Home Assistant.

- Customize the appearance of any card
- Apply themes and styling to match your design preferences
- Create unique and personalized dashboard layouts
- Override default styles with precision

## What is UIX Forge?

UIX Forge (`custom:uix-forge`) is a custom Lovelace element that combines template-driven configuration with additional behaviours called sparks. Use it to:

- Forge any standard Home Assistant element from templates, allowing the entire element config to react to entity states, user, browser and other template variables.
- Add sparks — self-contained behaviours that augment the forged element.
- Apply UIX Styling to the forged element, exactly like any other element. Additionally, any spark variables are made available in `uixForge` template variables.

## What is UIX Broker?

UIX Broker turns browser events, keyboard shortcuts, and Home Assistant event-bus events into declarative interactions. An interaction selects a browser element, checks optional rules, then runs directives in their configured order.

`Realm → Listen → Interaction anchor → Rules (Optional anchors) → Directives (Optional anchors)`

Use UIX Broker when an interface behaviour can be configured rather than written as a custom card, script, or patch. UIX Broker can react to a click, customise an event before redispatching it, focus an element, update an object property, invoke a safe element method, add an interactive button, and run JavaScript actions with interaction variables available.

## Contributing

If you would like to contribute a guide, or have a guide idea that you need assistance with, please submit a [UIX Q&A discussion](https://github.com/Lint-Free-Technology/uix/discussions) via Lint Free Technology GitHub.

## Resources

- [UIX website](https://uix.lf.technology)
- [UIX on GitHub](https://github.com/Lint-Free-Technology/uix).

---

*This site is maintained by [Lint Free Technology](https://lf.technology) and the UIX community. All content on this site has been specifically contributed by contributors for inclusion in this site.*
