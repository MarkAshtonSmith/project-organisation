# Acer to ThinkPad and NiPoGi Migration Guide

Last reviewed: 2026-05-13

This runbook moves the working setup from the current Acer machine into a two-machine operating model:

```text
ThinkPad = daily coding, writing, browser dashboards, review and approval
NiPoGi mini-PC = persistent runtime, Docker services, scheduled jobs and runners
GitHub = code, config and specification truth
Cloud services = source of truth for their own data
```

Use this alongside `DEVICE_ORG_DIVISION_OF_LABOUR.md`.

## Migration Principle

Do not clone the Acer by copying everything onto both new machines. Most important state should either already be in GitHub or recreated from cloud services, password manager entries, `.env.example` files and documented setup.

The migration target is:

- ThinkPad can build, edit, test, commit and push the active repos.
- NiPoGi can run selected service/runtime repos without holding broad personal or admin sessions.
- Acer can be retired only after all important local work, secrets and recovery paths are accounted for.

## Core Repo Carry-Over

| Item | Value |
|---|---|
| Main repo | `https://github.com/Mindware-Lab/trident-g-platform` |
| Main branch | `main` |
| IQ Pro app path | `products/trident-g-iq/apps/iq-pro` |
| IQMindware website path | `products/trident-g-iq/websites/iqmindware` |
| Known IQ Pro fix anchor | `be30ab9 Fix zone route resume button` |

The `be30ab9` commit is a useful continuity marker, not the only commit that needs to exist on the new machines. Always clone or pull the current `main`.

## Stage 1: Freeze and Audit the Acer

Before moving work, check what is local-only on the Acer.

From each important project folder:

```powershell
git status --short
git branch --show-current
git remote -v
```

For this repo, the expected remote is:

```text
https://github.com/Mindware-Lab/trident-g-platform
```

If `git status --short` shows modified or untracked files, decide whether each item should be:

- committed and pushed,
- copied into a secure backup,
- moved into a password manager or cloud dashboard, or
- discarded because it is generated/cache state.

Do not wipe or repurpose the Acer until the active project folders are either clean or deliberately backed up.

## Stage 2: Back Up What GitHub Does Not Hold

Back up or recreate these before moving:

| Item | Best destination |
|---|---|
| `.env` files with real values | Password manager or encrypted admin backup |
| API keys and webhooks | Password manager, Cloudflare/Supabase/Stripe/Brevo dashboards |
| SSH keys | Prefer new per-device keys; back up old keys only if needed |
| Browser bookmarks | Browser sync or export |
| Obsidian/Zotero/research files | Their sync service, GitHub repo, or encrypted backup |
| n8n workflows, if local | Export workflow/credential backup |
| Docker compose files not in GitHub | Commit safe versions or copy securely |
| Docker volumes/local DBs, if services were local | Service-specific backup |
| Recovery codes | Password manager plus offline sealed backup |

Do not put secrets, customer exports, identity documents or recovery codes into this repo.

## Stage 3: Do Not Transfer These Directly

Do not copy these from the Acer as migration artefacts:

- `node_modules/`
- `dist/`
- Python `venv/` folders
- Docker images
- browser cached passwords
- random local `.env` files into GitHub
- browser `localStorage`, unless debugging one specific user/device state
- the same SSH private key to every machine unless there is a specific reason

Regenerate build artefacts from source and reinstall dependencies on each machine.

## Stage 4: ThinkPad Setup

The ThinkPad is the daily work and authority machine.

Install/sign in to:

- Git
- GitHub CLI or GitHub Desktop
- VS Code and/or Cursor
- Node.js/npm
- password manager
- browser profiles for business admin, personal, government/identity, social/publishing and dev testing
- Obsidian/Zotero if used

Set Git identity:

```powershell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Authenticate GitHub:

```powershell
gh auth login
gh auth status
```

Clone the main repo:

```powershell
cd $HOME\Documents\GitHub
git clone https://github.com/Mindware-Lab/trident-g-platform
cd trident-g-platform
git status --short
```

Expected result after a clean clone:

```text
no output from git status --short
```

## Stage 5: IQ Pro Local Setup on ThinkPad

From the cloned repo:

```powershell
cd products/trident-g-iq/apps/iq-pro
npm install
npm run dev
```

For production build testing:

```powershell
npm run build
```

If the app needs local environment variables, create the local file from:

```text
products/trident-g-iq/apps/iq-pro/.env.example
```

The real values should come from Cloudflare, Supabase, Stripe or the password manager. Important variables include:

```text
VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY
VITE_IQ_PRO_REQUIRED_BUNDLE
VITE_IQ_PRO_ALLOW_LOCAL_DEMO
SUPABASE_SERVICE_ROLE_KEY
STRIPE_WEBHOOK_SECRET
STRIPE_PRICE_IQ_PRO
```

Do not commit real `.env` files.

## Stage 6: IQMindware Website Setup on ThinkPad

Main website path:

```text
products/trident-g-iq/websites/iqmindware
```

Use this folder for iqmindware.com website edits unless Cloudflare Pages is confirmed to deploy from a wider repo/root project.

After edits:

```powershell
git status --short
git add <changed-files>
git commit -m "Describe the website change"
git push origin main
```

Cloudflare Pages should then deploy from GitHub `main` if the Pages project is connected correctly.

## Stage 7: Cloudflare Pages Checks

Confirm the Pages project is still connected to GitHub `main`.

For the IQ Pro app, important settings are:

```text
Project root: products/trident-g-iq/apps/iq-pro
Build command: npm run build
Build output: dist
Functions directory: functions
```

For `iqmindware.com`, check whether the Pages project deploys from:

```text
products/trident-g-iq/websites/iqmindware
```

or from the wider repo/root. That determines exactly where website edits should be made.

## Stage 8: NiPoGi Setup

The NiPoGi should be configured as a runtime/server machine, not as the main browser/admin cockpit.

Install:

- Ubuntu updates
- Git
- Docker Engine
- Node.js only where services need it
- SSH server
- optional GitHub Actions runner
- optional Tailscale/WireGuard/private tunnel

Create a service workspace, for example:

```bash
mkdir -p ~/kastel/services
mkdir -p ~/repos
```

Generate a NiPoGi-specific SSH key or authenticate GitHub using a device-specific method. Avoid copying the same private key from the Acer and ThinkPad unless necessary.

Clone only repos that NiPoGi actually needs to run:

```bash
cd ~/repos
git clone https://github.com/Mindware-Lab/trident-g-platform
```

For private runtime repos, clone only what the NiPoGi needs, such as private Kastel node repos or service repos. Keep broad browser/admin access on the ThinkPad.

## Stage 9: NiPoGi Runtime Responsibilities

Good NiPoGi workloads:

- Docker services.
- scheduled jobs.
- webhook receivers.
- metric snapshots.
- read-only API polling.
- build/test runners.
- lightweight local automation.
- embedding/index jobs where latency is not critical.
- candidate intent generation for later ThinkPad review.

Poor NiPoGi workloads:

- Stripe/Brevo/Supabase/Cloudflare dashboard administration.
- GitHub organisation settings.
- visible browser automation.
- payment, identity, tax or banking work.
- final publication decisions.
- claims-sensitive edits without review.

If a service needs secrets, deploy only the specific service secrets required by that service. Keep the master record in the password manager.

## Stage 10: Codex Context on New Machines

When starting a fresh Codex session on the ThinkPad, useful context is:

```text
Repo: trident-g-platform
Work mainly in:
- products/trident-g-iq/apps/iq-pro for IQ Pro app
- products/trident-g-iq/websites/iqmindware for iqmindware.com website
Branch: main
Deployment: Cloudflare Pages auto-deploys from main
```

For NiPoGi-related work, add:

```text
NiPoGi is the runtime/server machine.
Do not make it the admin dashboard or human review cockpit.
Use GitHub as code/config truth and keep secrets out of the repo.
```

## Stage 11: Cutover Checklist

The migration is complete when:

- ThinkPad can clone, build and run IQ Pro.
- ThinkPad can edit and push `trident-g-platform`.
- Cloudflare Pages deploys from `main`.
- IQMindware website edit path is confirmed.
- Real `.env` values are recreated securely from password manager/cloud dashboards.
- NiPoGi has Git, Docker and SSH working.
- NiPoGi has only the runtime repos it needs.
- Any NiPoGi services can be rebuilt from GitHub plus documented secrets.
- Acer has no uncommitted work in important repos.
- Acer `.env`, SSH, Obsidian, Zotero, n8n, Docker volume and recovery-code state has been handled.

## Final Acer Retirement Rule

Before wiping or demoting the Acer, verify:

```powershell
git status --short
```

in every important repo, and confirm:

- all meaningful code/content is committed and pushed,
- all secrets are in the password manager or cloud secret store,
- all recovery codes are accessible from the ThinkPad and phone,
- all local-only data has been deliberately copied or discarded,
- the ThinkPad can do daily work without the Acer,
- the NiPoGi can run the services assigned to it without the Acer.

Only then should the Acer stop being treated as the operational source machine.

