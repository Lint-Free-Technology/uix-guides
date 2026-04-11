---
title: Testing dialogs in the browser console
description: A one-stop reference for triggering and testing Home Assistant dialogs and UIX notifications from the browser developer console
tags:
  - dialogs
  - testing
---
When developing or troubleshooting UIX dialog styles it is useful to be able to trigger dialogs on demand without navigating to the relevant part of the UI. This guide provides a centralized, linkable reference of browser console snippets that let you do exactly that.

Open the browser developer tools with `F12` (or `Cmd ⌥ I` on macOS) and paste any of the snippets below into the **Console** tab.

## Trigger a UIX update notification

The following dispatches a persistent `hass-notification` event on the `<home-assistant>` root element, simulating the banner that appears when UIX has been updated.

```console
document.querySelector("home-assistant").dispatchEvent(new CustomEvent("hass-notification", { detail: { message: "UIX has been updated", duration: -1, dismissable: true }, bubbles: true, composed: true }));
```

`duration: -1` keeps the notification visible until it is manually dismissed. Change the `message` value to test other notification texts.

## Trigger an alert dialog

`window.cardHelpers` exposes the same dialog helpers that Home Assistant cards use internally. The following opens an alert dialog:

```console
window.cardHelpers.showAlertDialog(document.querySelector("home-assistant"), { title: "Restart Home Assistant?", text: "Some text" });
```

Replace `title` and `text` with the values you want to test. The dialog type class reported in the DOM will be `type-dialog-box`, which you can use to scope CSS in your UIX theme.

{% include admonition.html type="tip" title="Finding the dialog type class" body="With the dialog open, open the **Elements** panel in developer tools and inspect the last child of the `<home-assistant>` shadow root. The outer element is the dialog parent (e.g. `<dialog-box>`). Its type class (e.g. `type-dialog-box`) can be used to scope your UIX theme CSS." %}

## Trigger a confirmation dialog

A confirmation dialog (with **Cancel** and **Confirm** buttons) can be opened with `showConfirmationDialog`:

```console
window.cardHelpers.showConfirmationDialog(document.querySelector("home-assistant"), { title: "Restart?", text: "Are you sure you want to restart Home Assistant?", confirmText: "Restart", dismissText: "Cancel" });
```

## Inspect UIX variables on a dialog element

Once a dialog is open and visible in the **Elements** panel, select the inner dialog element (e.g. `ha-dialog`) and run the following in the **Console** to see all UIX variables including `params`:

```console
$0._uix[0].variables
```

`$0` refers to the currently selected element in the Elements panel. The `params` object contains the values passed to the dialog, such as `title` and `text`, which you can use in UIX Jinja2 templates to target a specific dialog.

{% include admonition.html type="info" title="Using params in templates" body="See the [Styling dialogs]({% post_url dialogs/2026-02-27-styling-dialogs %}) guide for a full example of using `params` in a UIX template to target a specific dialog." %}

## Styling the dialogs you are testing

For a complete guide on how to style dialogs using UIX themes — including template examples and shadow DOM targeting — see [Styling dialogs with UI eXtension]({% post_url dialogs/2026-02-27-styling-dialogs %}).
