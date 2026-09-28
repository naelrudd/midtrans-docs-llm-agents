---
updatedAt: 2026-09-28T08:57:52.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Feature Guide

These features can be selected and configured during project creation:

## Auth Feature

#### &#x20;(Available only during creation) *\[Refer:&#x20;*<https://docs.midtrans.com/reference/seamless-login-v2>*]*

  The **Auth** feature provides the authentication and container configuration required by mini apps running inside the GoPay host app.

* **When selected, prompts:**

```Plain
When to fetch auth code?
● Before app renders
○ After app renders
```

* Before: The app waits for the Auth Code before showing the UI. Use this when authentication is required to load the app.
  * Example: A travel app where the user's profile is required to render the initial UI, such as showing their name, preferences or personalized travel information.
* After: The app shows the UI first, and the Auth Code can be fetched whenever needed by calling the auth function. Use this when authentication is not required to show the initial UI.
  * Example: A game app where the current user's profile is not required initially, so the game can render first and fetch the Authcode later when the user profile is needed.

***

## JSAPIs Management

Mini Apps communicate with the native Host app via a "JSAPIs". [https://docs.midtrans.com/reference/command-reference/#jsapis-commands](https://docs.midtrans.com/reference/command-reference/#jsapis-commands "https://docs.midtrans.com/reference/command-reference/#jsapis-commands")

```Bash
minikit-cli jsbridge:add <class_name> <method_name> --cache
minikit-cli jsbridge:remove <class_name> <method_name>
```

***

## i18n Feature

The **i18n feature** supports multiple languages in the app. It provides two translation sources:

[**Command:** `minikit-cli i18n:add`](https://docs.midtrans.com/reference/command-reference)

***

## Payment Integration Using Snap

[**Snap Checkout**](https://docs.midtrans.com/reference/miniapp-x-snap-checkout-payment) enables Mini Apps to accept payments through Midtrans.

[**Command:** `minikit-cli snap:add`](https://docs.midtrans.com/reference/command-reference)

***

## Debug Tools

**Debug Tools** help developers debug the Mini App during development. After selecting **vConsole**, it is enabled automatically in development mode. When you run the Mini App on a mobile device, the vConsole button appears in the bottom-right corner of the screen.

[**Command:** `minikit-cli vconsole:add`](https://docs.midtrans.com/reference/command-reference)

***

#