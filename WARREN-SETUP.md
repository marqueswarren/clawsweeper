# Clawsweeper — Warren Group Setup

## What you need to do (one-time, ~10 min)

### 1. Create the GitHub App
Go to: https://github.com/settings/apps/new

Fill in:
- **App name**: `clawsweeper-warren`
- **Homepage URL**: `https://github.com/marqueswarren/clawsweeper`
- **Webhook**: Active → URL: leave blank for now (Actions fallback handles it)
- **Permissions (Repository)**:
  - Contents: Read & Write
  - Issues: Read & Write
  - Pull requests: Read & Write
  - Checks: Read & Write
  - Commit statuses: Read & Write
  - Metadata: Read-only (required)
- **Subscribe to events**: `Pull request`, `Issue comment`, `Pull request review`
- **Where can this app be installed?** → Only on this account

Click **Create GitHub App**. You'll get an **App ID** and a **Client ID** (format: `Iv23l...`).

Download the private key (.pem file) from the App settings page.

### 2. Install the App on your repos
From the App settings page → Install App → Install on `marqueswarren` →
Select repositories: `sterling-intelligence-platform`, `warren-group-website`, `madwine-com`

### 3. Add secrets to this repo
Go to: https://github.com/marqueswarren/clawsweeper/settings/secrets/actions

Add:
- `OPENAI_API_KEY` — your OpenAI key
- `CLAWSWEEPER_APP_PRIVATE_KEY` — paste the full contents of the downloaded .pem file

### 4. Tell Sterling the Client ID
Reply with the **Client ID** (format: `Iv23l...`) — Sterling will update the workflow files.

## How automerge works after setup

1. Sterling (or you) adds `Brief: BRIEF-...` to a PR body
2. Once CI is green, comment `@clawsweeper automerge` on the PR
3. Clawsweeper verifies the BRIEF ref + CI + mergeability, then merges

For repos with `enforce_admins: true`, add clawsweeper-warren as a bypass actor in branch protection:
Settings → Branches → main → Edit → Bypass list → Add `clawsweeper-warren[bot]`
