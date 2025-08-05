# Shopify Theme Management with Shopkeeper CLI

This guide outlines the workflow for managing Shopify themes using the `shopkeeper` CLI, including bucket operations, theme settings, and integration with the standard Shopify CLI.

---

## 🚀 Initial Setup

### Create a New Bucket

```bash
npx shopkeeper bucket create --bucket bv-usa
```

### Switch to Production Bucket (without deleting local files)

```bash
npx shopkeeper bucket switch --bucket production --nodelete
```

---

## 💾 Save Theme Settings

Originally, to save theme settings from the `theme/` folder to the `shopkeeper` bucket:

```bash
npx shopkeeper bucket save --bucket production
```

---

## ⬇️ Download Theme Settings

```bash
npx shopkeeper theme settings download
```

### Save the Downloaded Settings Again

```bash
npx shopkeeper bucket save --bucket production
```

---

## 📂 Theme Snapshots

You may see the following theme versions in your dashboard:

```
 Updated copy of Dawn             [live]                  #148026327205
 green                            [unpublished]           #148042219685
```

---

## 🔄 Switch to Custom Bucket (bv-usa)

To work with your custom environment and prepare for development:

```bash
npx shopkeeper bucket switch --bucket bv-usa --nodelete
```

> This will:
> - Copy environment variables to the main folder.
> - Copy theme settings from `.shopkeeper/` to the `theme/` folder.
> - Make your project compatible with standard Shopify CLI workflows.

---

## 🛠️ Standard Shopify CLI Workflow

### Pull the Latest Theme Code

```bash
shopify theme pull
```

> Note: This pulls all files, but `git status` will only show changes to files (excluding `.json` files).

---

## 📤 Save & Deploy Workflow

### Save the Current Theme State to bv-usa Bucket

```bash
npx shopkeeper bucket save --bucket bv-usa
```

### Deploy Theme Settings (Only Settings, Not Liquid Files)

```bash
npx shopkeeper theme deploy
```

> This:
> - Downloads settings from the currently **live** theme.
> - Copies **only the settings** to the `theme/` folder (ignoring liquid/template files).
> - Uploads the final `theme/` folder to a **non-live** theme using the `shopify theme upload` command.

---

## ✅ Summary

This setup allows you to:

- Manage different environments via buckets (`bv-usa`, `production`, etc.)
- Separate logic for **live theme settings** and **dev theme settings**
- Use both `shopkeeper` and `shopify CLI` smoothly together
