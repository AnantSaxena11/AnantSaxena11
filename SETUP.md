# ⚙️ Setup Guide — Adding Your PAT Token

The GitHub Metrics workflow (`metrics.yml`) requires a Personal Access Token (PAT) stored as a repository secret named **`METRICS_TOKEN`**.

Follow the steps below to create the token and add it to your repository.

---

## Step 1 — Create a Personal Access Token

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)**
   - Direct link: <https://github.com/settings/tokens>
2. Click **"Generate new token (classic)"**.
3. Give it a descriptive name, e.g. `METRICS_TOKEN`.
4. Set an **expiration** that suits you (or select *No expiration*).
5. Select the following scopes:

   | Scope | Why it is needed |
   |---|---|
   | `repo` | Read repository data (stars, commits, languages, etc.) |
   | `read:user` | Read your public profile information |
   | `read:org` | Read organization membership (for `repositories_affiliations`) |

6. Click **"Generate token"** and **copy the token immediately** — you will not be able to see it again.

---

## Step 2 — Add the Token as a Repository Secret

1. Open your profile repository: **`<your-username>/<your-username>`**
2. Go to **Settings → Secrets and variables → Actions**.
3. Click **"New repository secret"**.
4. Fill in the fields:
   - **Name:** `METRICS_TOKEN`
   - **Secret:** paste the token you copied in Step 1
5. Click **"Add secret"**.

---

## Step 3 — Run the Workflow

1. Go to the **Actions** tab of your repository.
2. Select the **"GitHub Metrics"** workflow.
3. Click **"Run workflow"** → **"Run workflow"** to trigger it manually.

The workflow will generate the SVG metric files and commit them to the `main` branch automatically.

---

## Troubleshooting

| Problem | Solution |
|---|---|
| Workflow fails with `401 Unauthorized` | The token is expired or missing required scopes — regenerate it and update the secret. |
| Metrics SVGs are not updated | Make sure the `committer_branch` in `metrics.yml` matches your default branch (`main`). |
| Language stats are incomplete | Enable `plugin_languages_indepth: yes` (already set) and ensure the token has the `repo` scope. |
