# HubSpot CMS Deploy Action — **React CMS Edition** <!-- omit in toc -->

[![react-cms](https://img.shields.io/badge/✅%20React%20CMS-ready-orange)](https://developers.hubspot.com/docs/guides/cms/react/overview)
[![draidel-fork](https://img.shields.io/badge/Fork%20by-Draidel%20LLC%20%E2%80%93%20HubSpot%20Partner-0A7AFF)](https://draidel.com)

> **This fork adds full support for HubSpot → React CMS Developer Projects**  
> (`hs project upload`), while keeping backward compatibility with classic "theme‐only" uploads.

Deploy any HubSpot CMS **React project** or traditional theme to your portal 🚀

---

- [Quick Start](#quick-start)
- [Deploying to a staging account](#deploying-to-a-staging-account)
- [Integrating into an existing workflow](#integrating-into-an-existing-workflow)
- [Action Spec](#action-spec)

---

## Quick Start

1. **Secrets & variables**
   | Key | Store in | Purpose |
   |-----|----------|---------|
   | `HUBSPOT_PERSONAL_ACCESS_KEY` | **Secrets** | Your personal CMS access key |
   | `HUBSPOT_ACCOUNT_ID` | **Variables** | Your HubSpot **Account ID** |

2. **Workflow**

<details>
<summary><strong>A) React CMS / Developer Project</strong></summary>

```yaml
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy React CMS Project
        uses: Draidel/hubspot-cms-deploy-action@v2
        with:
          src_dir: .                  # root where hsproject.json lives
          force_create: true          # create the Project on first run
          account_id: ${{ vars.HUBSPOT_ACCOUNT_ID }}
          personal_access_key: ${{ secrets.HUBSPOT_PERSONAL_ACCESS_KEY }}
```

</details>

<details>
<summary><strong>B) Classic HubSpot Theme</strong></summary>

```yaml
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy Theme
        uses: Draidel/hubspot-cms-deploy-action@v2
        with:
          src_dir: src                # local theme folder
          dest_dir: my-theme          # target path in HubSpot
          account_id: ${{ vars.HUBSPOT_ACCOUNT_ID }}
          personal_access_key: ${{ secrets.HUBSPOT_PERSONAL_ACCESS_KEY }}
```

</details>

> **Why two modes?**
> *React CMS* projects bundle build tooling, serverless functions, extensions UI, etc. and require `hs project upload`.
> Traditional themes are flat code/assets and use the older `hs upload`.

---

## Deploying to a staging account

<details>
<summary>Show example</summary>

```yaml
# same action, different branch & account
on:
  push:
    branches: [qa]
jobs:
  deploy-staging:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Draidel/hubspot-cms-deploy-action@v2
        with:
          src_dir: .
          force_create: true
          account_id: ${{ vars.HUBSPOT_ACCOUNT_ID }}   # staging ID
          personal_access_key: ${{ secrets.HUBSPOT_PERSONAL_ACCESS_KEY }}
```

</details>

---

## Integrating into an existing workflow

```yaml
- name: Deploy to HubSpot (React CMS)
  uses: Draidel/hubspot-cms-deploy-action@v2
  with:
    src_dir: .
    force_create: true
    account_id: ${{ vars.HUBSPOT_ACCOUNT_ID }}
    personal_access_key: ${{ secrets.HUBSPOT_PERSONAL_ACCESS_KEY }}
```

---

## Action Spec

| Input                 | Required | Description                                         |
| --------------------- | -------- | --------------------------------------------------- |
| `src_dir`             | ✔        | Root of the **React CMS project** *or* theme folder |
| `dest_dir`            | —        | Only for classic themes (`hs upload`)               |
| `force_create`        | —        | `true` → creates the Project if it doesn't exist    |
| `account_id`          | ✔        | HubSpot Account ID                                  |
| `personal_access_key` | ✔        | HubSpot personal access key                         |

---

Made with ❤️ by **[Draidel LLC – HubSpot Gold Partner](https://www.draidel.com)**

Feel free to open issues or PRs!

### Key Changes

* **Title and badge**: immediately highlight "React CMS Edition"
* **One-line intro**: explains that `hs project upload` compatibility was added
* **Collapsible sections**: clearly separate React CMS vs. classic theme workflows
* **Input table** and examples focused primarily on *React CMS*

Copy this block to your `README.md`, commit, and you're ready to go! 🟢
