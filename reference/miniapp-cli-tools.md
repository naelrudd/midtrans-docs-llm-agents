---
updatedAt: 2026-09-28T09:10:21.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# MiniKit CLI: Create Your First MiniApp

## **Overview**

**MiniKit CLI** is a developer tool for scaffolding and managing the frontend of [MiniApp](https://docs.midtrans.com/reference/overview-miniapp) web applications built with *React and TypeScript* in the GoTo ecosystem. It provides a standard setup with tooling, configuration, and selected internal integrations pre-configured.

***

## **Prerequisites & Create**

**Step 1: Check Your System**

Before installing the CLI, make sure the following are in place:

<Table>
  <thead>
    <tr>
      <th>
        **Requirement**
      </th>

      <th>
        **Description**
      </th>

      <th>
        Verification Command
      </th>

      <th>
        **Install**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Git
      </td>

      <td>

      </td>

      <td>
        `git --version`
      </td>

      <td>
        If not installed, download it from [https://git-scm.com/install/](https://git-scm.com/install/).
      </td>
    </tr>

    <tr>
      <td>
        Bun.js
      </td>

      <td>
        A fast JavaScript runtime and package manager used to run the CLI.
      </td>

      <td>
        `bun --version`
      </td>

      <td>
        ```Bash
        curl -fsSL https://bun.com/install | bash -s "bun-v1.3.14"
        ```
      </td>
    </tr>
  </tbody>
</Table>

**Step 2: Install the CLI tool**

Run the following command to install the CLI globally and verify that it was installed correctly:

```Bash
bun install -g @gopay/minikit-cli@latest && minikit-cli --version
```

**Step 3: Run the Create Command**

```Plain
minikit-cli create my-first-project
```

Replace `my-first-project` with your project name (lowercase, with hyphens).

<Image src="https://files.readme.io/b705cbae037c6d9f194f3d8bf06969098056ba966620008d753672b22152653a-20260928-160941.gif" alt="Snap Embedded - Mobile Implementation via Mobile View" align="center" />

**Step 4: Select the Wizard Options**

The CLI will ask you a series of questions.

**1: Framework**

```Plain
? Choose a framework
  › React + TypeScript
```

**2: Install Dependencies**

```Plain
? Install dependencies with pnpm?
  › Yes
```

**3: Features to Include**

```Plain
? Select features (multi-select, press Space to toggle)
  ◯ Auth 
  ◯ i18n (Multi-language)
  ◯ Snap Checkout (Payments)
```

**Choose based on your MiniApp requirement:**

| **Feature**                                                                                            | **When to choose**                                            |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------- |
| [***Auth***](https://docs.midtrans.com/reference/feature-guide#auth-feature)                           | MiniApp requires seamless login.                              |
| [**i18n**](https://docs.midtrans.com/reference/feature-guide/#i18n-feature)                            | MiniApp serves users in multiple languages                    |
| [**Snap Checkout**](https://docs.midtrans.com/reference/feature-guide/#payment-integration-using-snap) | MiniApp needs payments integration                            |
| [**Debug Tools**](https://docs.midtrans.com/reference/feature-guide/#debug-tools)                      | Testing MiniApp on physical mobile or debugging in production |

**4: Debug tool to Include**

```Plain
? Select Debug Tool (press Space to toggle)
  ◯ vConsole
```

**Step 5: Run your MiniApp**

```Plain
cd my-app
source "$HOME/.nvm/nvm.sh" && nvm use
cp .env.example .env
pnpm install  # If not already done
pnpm dev
```

Open the url to the browser. You should see the default home page heading ***"Your Miniapp is ready..."***.

✅ 🎉 **Congratulations!** Your MiniApp is running.

**Next Step:** To open and test the app as a GoPay/Gojek MiniApp, deploy your changes and try it out using the GoPay/Gojek app.

## **Technical Support**

<https://docs.midtrans.com/reference/miniapp-v2#technical-assistant-and-support>

***

<br />

<br />