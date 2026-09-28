---
updatedAt: 2026-09-28T08:48:16.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Command Reference

## create

Scaffold a new Mini App project.

```Plain
minikit-cli create [project-name] [options]
```

| **Option**           | **Description**                             |
| -------------------- | ------------------------------------------- |
| --no-install         | Skip installing dependencies                |
| --project-dir <path> | Parent directory for the scaffolded project |

```Plain
minikit-cli create my-app
minikit-cli create my-app --no-install
minikit-cli create my-app --project-dir /tmp/scaffolds --no-install
```

When **Auth** is selected, the following files are added or modified during the `create` operation.

| File/Directory                       | Added/Modified      | Purpose & Change                                                                       |
| ------------------------------------ | ------------------- | -------------------------------------------------------------------------------------- |
| src/bridge/handlers/get-auth-code.ts | Added               | GPBase.getAuthCode bridge handler                                                      |
| src/hooks/useAuthCode.ts             | Added (conditional) | Custom hook for auth code. Only added with "fetch before render" option                |
| src/api/fetch-user-data.ts           | Added (conditional) | API layer for user data. Only added with "fetch before render" option                  |
| src/pages/home.tsx                   | Modified            | Adds an auth handler demo; fully replaced in fetch-before-render mode                  |
| src/pages/layout.tsx                 | Modified            | Calls useAuthCode() and logs result in development when fetch-before-render is enabled |

![](https://files.readme.io/0aeb17132ca86341414f1df9d4176b541db3164247191e1ef47c15208aa1070d-img_v3_0215v_e85b0983-c83e-47c7-a029-9604b3b6behu.png)

***

## JSAPIs Commands

Below are the commands for adding and removing JSAPIs. Refer to view the complete [list of available JSAPIs](https://docs.midtrans.com/reference/frontend-v2#jsapis-specification-v100) and learn more about each one

***Note:****&#x20;*`className`*&#x20;represents the category and starts with the&#x20;*`GP`*&#x20;prefix.&#x20;*`methodName`*&#x20;represents the main function being invoked.*

### jsbridge:add

Add a Host App method to call from your Mini App.

```Plain
minikit-cli jsbridge:add [className] [methodName] [options]
```

| **Argument** | **Format** | **Example**          |
| ------------ | ---------- | -------------------- |
| className    | PascalCase | GPAuth, GPWallet     |
| methodName   | camelCase  | getToken, getBalance |

Both arguments are optional — omit either to be prompted.

| **Option** | **Alias** | **Description**                           |
| ---------- | --------- | ----------------------------------------- |
| --cache    | -c        | Cache the result for the session lifetime |

```Plain
minikit-cli jsbridge:add
minikit-cli jsbridge:add GPAuth getToken --cache
```

![](https://files.readme.io/352bfc34ba28a76c01b468a925b0c57cf38e4e0c2103beb471d3b381cc8fe13d-image.png)

| **File/Directory**   | **Added/Modified** | **Purpose & Change**                                             |
| :------------------- | :----------------- | :--------------------------------------------------------------- |
| src/bridge/          | Added              | Core JSBridge module for native communication                    |
| src/bridge/handlers/ | Added              | All bridge handler files (device.ts, and more added by features) |

***

### jsbridge:remove

Remove a previously added JS Bridge method and its generated hook.

```Plain
minikit-cli jsbridge:remove [className] [methodName]
```

Both arguments are optional — omit either to pick from a list.

```Plain
minikit-cli jsbridge:remove
minikit-cli jsbridge:remove GPAuth getToken
```

![](https://files.readme.io/5a4d1617bdff23476a657088b07b3544dbc75aecbd4adb9730ee43abb9ce2ed5-image.png)

***

## i18n:add

Add multi-language support.

```Plain
minikit-cli i18n:add [options]
```

| **Option** | **Values** | **Description**                          |
| ---------- | ---------- | ---------------------------------------- |
| --source   | json       | Translation source. Omit to be prompted. |

```Plain
minikit-cli i18n:add
```

![](https://files.readme.io/7223e72bcaac50fdbc34b5f1245ee1f1b7e85c4f881d56ccc6ea4f01bcca8a30-image.png)

| **File/Directory**      | **Added/Modified** | **Purpose & Change**                                             |
| ----------------------- | ------------------ | ---------------------------------------------------------------- |
| src/constants/locale.ts | Added              | Supported locales configuration                                  |
| project.inlang/         | Added              | Inlang project configuration for managing translations           |
| messages/               | Added              | Paraglide message catalogs for storing translations              |
| src/globals.d.ts        | Modified           | Adds i18n type definitions                                       |
| src/bridge/types.ts     | Modified           | Adds Locale and LocaleResponse types for bridge communication    |
| src/bridge/index.ts     | Modified           | Registers GPBase.getLocale bridge handler                        |
| vite.config.ts          | Modified           | Adds Paraglide Vite plugin for compilation                       |
| package.json            | Modified           | Adds compile:messages script and @inlang/paraglide-js dependency |
| src/pages/layout.tsx    | Modified           | Synchronizes active locale on app load                           |

***

## snap:add

Add Snap Checkout (Midtrans) payment integration.

```Plain
minikit-cli snap:add
```

![](https://files.readme.io/5518c8baddbad05038c52bfb75648326c0115291a11a634d3016a7ae0ac67240-image.png)

| **File/Directory**                     | **Added/Modified** | **Purpose & Change**                                             |
| -------------------------------------- | ------------------ | ---------------------------------------------------------------- |
| src/snap-checkout/                     | Added              | Snap Checkout integration module directory                       |
| src/snap-checkout/fetch-request.ts     | Added              | Request fetching logic for Snap API                              |
| src/snap-checkout/use-fetch-request.ts | Added              | Custom hook for managing fetch requests                          |
| src/snap-checkout/types.ts             | Added              | TypeScript type definitions for Snap Checkout                    |
| src/snap-checkout/snap-checkout.tsx    | Added              | Main Snap Checkout component                                     |
| src/snap-checkout/index.ts             | Added              | Module exports for Snap Checkout                                 |
| src/pages/snap-checkout.tsx            | Added              | Page component for Snap Checkout flow                            |
| src/pages/routes.ts                    | Modified           | Registers the /snap-checkout route                               |
| src/pages/home.tsx                     | Modified           | Adds CTA (Call-to-Action) linking to /snap-checkout              |
| .env.example                           | Modified           | Adds VITE\_MIDTRANS\_SNAPJS\_URL and VITE\_MIDTRANS\_CLIENT\_KEY |
| src/vite-env.d.ts                      | Modified           | Adds TypeScript types for Midtrans environment variables         |

***

## vconsole:add

Add vConsole, an in-app debug panel.

```Plain
minikit-cli vconsole:add
```

![](https://files.readme.io/da3381814459deece40eef3b5a3a47b8a94fb500895985ea1db8a0e286a6ec8c-image.png)

| **File/Directory**    | **Added/Modified** | **Purpose & Change**                                       |
| --------------------- | ------------------ | ---------------------------------------------------------- |
| src/debug/vconsole.ts | Added              | vConsole initialization and setup logic                    |
| src/main.tsx          | Modified           | Imports and calls initVConsole() before app renders        |
| package.json          | Modified           | Adds vconsole npm dependency                               |
| .env.example          | Modified           | Adds VITE\_ENABLE\_VCONSOLE environment variable           |
| src/vite-env.d.ts     | Modified           | Adds TypeScript type definition for VITE\_ENABLE\_VCONSOLE |

***

## update

Update the MiniKit CLI itself to the latest published version.

```Plain
minikit-cli update [options]
```

| **Option**  | **Description**                                                                   |
| ----------- | --------------------------------------------------------------------------------- |
| --check     | Report current vs. latest version without installing                              |
| --tag <tag> | dist-tag to resolve. Defaults to beta for prerelease installs, latest for stable. |

```Plain
minikit-cli update
minikit-cli update --check
minikit-cli update --tag latest
```

Run minikit-cli migrate inside each project after updating, to apply project-level migrations.

![](https://files.readme.io/e8afb1db99106c5e53412ceb8427390731ffacb9740be478ac07c3daf4bf375a-image.png)

***

## docs

List or search documentation links.

```Plain
minikit-cli docs [keyword]
```

```Plain
minikit-cli docs
```

Search is case-insensitive, matches document names and titles.

***

## --help

Every command supports --help for inline usage info:

```Plain
minikit-cli --help
minikit-cli create --help
minikit-cli jsbridge:add --help
minikit-cli i18n:add --help
minikit-cli litmus:add --help
```

***

#