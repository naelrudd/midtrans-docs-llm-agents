---
updatedAt: 2026-09-28T08:47:37.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Troubleshooting

1. ### Command not found: minikit-cli

This happens due to CLI not installed or not in PATH. Use the following command to fix it:

```Plain
which minikit-cli
which bun
source ~/.zshrc && npm install -g @gopay/minikit-cli
```

2. ### Not a mini-app project

This happens due to running commands outside generated projects. Check .minikit.json and package.json whether present in the current repo.

3. ### Feature not working

This happens due to features not being installed or dependencies missing. Use the following command to fix it:

```Bash
minikit-cli <feature>:add && pnpm install && pnpm dev
```

4. ### Feature already set up

This happens due to running feature command when it's already installed in the project. Check .minikit.json to see if the feature is already listed.

5. ### vConsole not appearing

This happens due to `VITE_ENABLE_VCONSOLE` being disabled. Use the following command to fix it:

```Bash
# Set in .env: VITE_ENABLE_VCONSOLE=true
pnpm dev
```

6. ### Missing environment variables

This happens due to the `.env` file being missing or incomplete. Use the following command to fix it:

```Plain
cp .env.example .env && nano .env
```