# Acer to ThinkPad and NiPoGi Migration Guide

**Quarter-transition version**  
**Last reviewed:** 2026-05-16

This runbook moves the working setup from the current Acer machine into a two-machine operating model that supports the next quarter’s business and product objectives.

```text
ThinkPad = daily coding, writing, browser dashboards, review and approval
NiPoGi mini-PC = persistent runtime, Docker services, scheduled jobs and runners
GitHub = code, config and specification truth
Cloud services = source of truth for their own data
Acer = fallback machine until cutover is proven
```

Use this alongside `DEVICE_ORG_DIVISION_OF_LABOUR.md`.

---

## 0. Quarter context

The migration is not a separate technical project. It should support the next-quarter operating plan:

```text
1. Keep Trident G IQ Pro commercially active and revenue-generating.
2. Publish weekly content that builds awareness, trust, education and sales.
3. Activate Brevo / CRM for existing users, previous buyers and warm leads.
4. Produce proof, onboarding and activation assets for the current IQ Pro app.
5. Scope and build IQ Coach as the next-generation replacement app.
6. Scope and build Flow Zone / HRV with Alex as a separate partnership product.
7. Start the first private Kastel node for IQ Mindware operations.
8. Use mission tools or puzzle micro-apps as free feeder assets, not core product distractions.
```

The migration must therefore be judged by one question:

```text
Does this make the weekly business engine easier to run?
```

If the migration interrupts IQ Pro revenue, Brevo activation, weekly content or product build momentum, it is being over-scoped.

---

## 1. Core migration principle

Do **not** clone the Acer by copying everything onto both new machines.

Most important state should either already be in:

```text
GitHub
Cloudflare
Supabase
Stripe
Brevo
Substack
Google Workspace
password manager
encrypted backups
```

or recreated from:

```text
GitHub repos
cloud dashboards
.env.example files
documented setup instructions
device-specific SSH keys
```

The migration target is:

```text
ThinkPad can build, edit, test, commit and push the active repos.
ThinkPad can administer the business dashboards and approve decisions.
NiPoGi can run selected runtime/service repos without broad admin sessions.
NiPoGi can generate snapshots, candidate intents and delayed-review files.
Acer can be retired only after all important local work, secrets and recovery paths are accounted for.
```

---

## 2. Target operating model

### ThinkPad

The ThinkPad is the **human cockpit**.

It owns:

```text
coding and review
website copy
product messaging
claims/proof language
GitHub Projects
pull requests and release decisions
Stripe, Brevo, Supabase and Cloudflare dashboards
Substack, YouTube, LinkedIn and other publishing decisions
pricing, offers and product bundles
partnership judgement
customer-facing decisions
password manager and admin sessions
```

### NiPoGi mini-PC

The NiPoGi is the **persistent machine layer**.

It owns:

```text
Docker services
scheduled jobs
webhook receivers
read-only API polling
metric snapshots
local runners
build/test support
Kastel node runtime
candidate Action / Clarify Intent generation
delayed-review checks
script-library preparation
```

### Acer

The Acer is the **temporary fallback**.

It should remain available until:

```text
ThinkPad can do daily work without friction.
NiPoGi can run one safe runtime loop.
GitHub/cloud/password-manager sources of truth are confirmed.
All local-only work on the Acer is either committed, backed up or discarded deliberately.
```

Do not wipe, repurpose or sell the Acer until the final retirement checklist is complete.

---

## 3. Quarter-critical workstreams and device allocation

| Workstream | ThinkPad responsibility | NiPoGi responsibility | Acer role |
|---|---|---|---|
| **IQ Pro revenue protection** | Product copy, claims boundary, sales pages, Brevo approval, pricing/offers | Optional product-usage snapshots and proof summaries | Fallback only |
| **Weekly content engine** | Substack, LinkedIn, YouTube scripts, website edits, final publication | Draft summaries, search/query snapshots, content queue files | Fallback only |
| **Conversion and CRM** | Brevo segmentation, email writing, approval and sending | Read-only campaign summaries and intent drafts | Fallback only |
| **Product activation and proof** | User guides, proof-page wording, customer-facing claims | Supabase/product event summaries, completion/drop-off snapshots | Fallback only |
| **IQ Coach build** | Product architecture, coding, review, deployment decisions | Build/test runner, scheduled issue/report generation | Fallback only |
| **Flow Zone / HRV** | Brand, website, partner materials, claims boundary, Alex review | Partnership-node folders, pilot/waitlist metric snapshots | Fallback only |
| **Free mission tools / puzzle feeders** | Design, copy, code, launch decision | Later usage snapshots or build checks | Fallback only |
| **Kastel Node: IQ Mindware** | Weekly priority approval, Action/Clarify review, script-banking judgement | Runtime node, scheduled jobs, logs, candidate intents, delayed reviews | Fallback only |

---

## 4. Migration gates

Treat the transition as a sequence of gates, not a single switch.

### Gate A — ThinkPad cockpit ready

Complete when:

```text
ThinkPad can clone, build and run IQ Pro.
ThinkPad can edit and push trident-g-platform.
ThinkPad can access GitHub, Cloudflare, Supabase, Stripe, Brevo and the password manager.
ThinkPad has the active ChatGPT / Claude / browser project structure.
ThinkPad can publish weekly content and send reviewed CRM emails.
```

### Gate B — Current business safe

Complete when:

```text
IQ Pro product page / sales path still works.
Cloudflare Pages deployment path is confirmed.
Brevo access is confirmed.
Stripe product/payment access is confirmed.
Current weekly content workflow can happen entirely from the ThinkPad.
```

### Gate C — NiPoGi runtime ready

Complete when:

```text
Ubuntu is installed and updated.
SSH is working.
Git is installed.
Docker and Docker Compose are working.
Device-specific GitHub authentication is working.
Only required runtime repos are cloned.
A safe service can run and restart.
```

### Gate D — First Kastel loop works

Complete when:

```text
NiPoGi generates one weekly snapshot file.
ThinkPad reviews the file.
At least one Action Intent and one Clarify Intent are created.
A delayed review date is recorded.
Nothing is sent, published or changed automatically.
```

### Gate E — Acer retirement safe

Complete when:

```text
Important repos on Acer are clean or deliberately backed up.
Secrets and recovery codes are in the password manager / offline backup.
ThinkPad can do daily work without the Acer.
NiPoGi can run its assigned services without the Acer.
No local-only data on Acer is still operationally required.
```

---

## 5. Core repo carry-over

| Item | Value |
|---|---|
| Main repo | `https://github.com/Mindware-Lab/trident-g-platform` |
| Main branch | `main` |
| IQ Pro app path | `products/trident-g-iq/apps/iq-pro` |
| IQMindware website path | `products/trident-g-iq/websites/iqmindware` |
| Known IQ Pro fix anchor | `be30ab9 Fix zone route resume button` |

The `be30ab9` commit is a continuity marker, not the only commit that needs to exist on the new machines. Always clone or pull the current `main`.

Potential additional repos for the quarter:

```text
Mindware-Lab/IQ-Coach
Mindware-Lab/Zone-Coach
Mindware-Lab/mindware-ground-truth
Kastel-Stack/kastel-ground-truth
Kastel-Stack/kastel-stack
Kastel-Stack/kastel-node-template
Kastel-Stack/kastel-node-iqmindware          private, if used
Kastel-Stack/kastel-node-alex-partnership    private, if used
```

Clone only what each machine needs.

---

## 6. Stage 1 — Freeze and audit the Acer

Before moving work, check what is local-only on the Acer.

From each important project folder:

```powershell
git status --short
git branch --show-current
git remote -v
```

For the main repo, the expected remote is:

```text
https://github.com/Mindware-Lab/trident-g-platform
```

If `git status --short` shows modified or untracked files, decide whether each item should be:

```text
committed and pushed
copied into a secure backup
moved into a password manager or cloud dashboard
discarded because it is generated/cache state
```

Do not wipe or repurpose the Acer until the active project folders are either clean or deliberately backed up.

---

## 7. Stage 2 — Back up what GitHub does not hold

Back up or recreate these before moving:

| Item | Best destination |
|---|---|
| `.env` files with real values | Password manager or encrypted admin backup |
| API keys and webhooks | Password manager, Cloudflare/Supabase/Stripe/Brevo dashboards |
| SSH keys | Prefer new per-device keys; back up old keys only if needed |
| Browser bookmarks | Browser sync or export |
| Obsidian/Zotero/research files | Sync service, GitHub repo, or encrypted backup |
| n8n workflows, if local | Export workflow and credential backup |
| Docker compose files not in GitHub | Commit safe versions or copy securely |
| Docker volumes/local DBs, if services were local | Service-specific backup |
| Recovery codes | Password manager plus offline sealed backup |
| Local product notes | GitHub, Obsidian sync, or encrypted archive |
| Local sales/CRM exports | Prefer source cloud system; avoid keeping raw exports locally |

Do not put secrets, customer exports, identity documents or recovery codes into GitHub, ChatGPT, Claude or public cloud folders.

---

## 8. Stage 3 — Do not transfer these directly

Do not copy these from the Acer as migration artefacts:

```text
node_modules/
dist/
Python venv/ folders
Docker images
browser cached passwords
random local .env files into GitHub
browser localStorage, unless debugging one specific user/device state
the same SSH private key to every machine unless there is a specific reason
unreviewed customer/payment exports
old build artefacts
temporary downloads
```

Regenerate build artefacts from source and reinstall dependencies on each machine.

---

## 9. Stage 4 — ThinkPad setup

The ThinkPad is the daily work and authority machine.

Install/sign in to:

```text
Git
GitHub CLI or GitHub Desktop
VS Code and/or Cursor
Node.js/npm
password manager
browser profiles
Obsidian/Zotero if used
Docker Desktop only if useful for local dev
ChatGPT / Claude / AI coding tools
```

Recommended browser profiles:

```text
Business admin
Development/testing
Publishing/social
Personal
Government/identity
Finance/tax
```

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

---

## 10. Stage 5 — IQ Pro local setup on ThinkPad

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

The real values should come from Cloudflare, Supabase, Stripe or the password manager.

Important variables may include:

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

---

## 11. Stage 6 — IQMindware website setup on ThinkPad

Main website path:

```text
products/trident-g-iq/websites/iqmindware
```

Use this folder for `iqmindware.com` website edits unless Cloudflare Pages is confirmed to deploy from a wider repo/root project.

After edits:

```powershell
git status --short
git add <changed-files>
git commit -m "Describe the website change"
git push origin main
```

Cloudflare Pages should then deploy from GitHub `main` if the Pages project is connected correctly.

Priority website work for the quarter:

```text
current IQ Pro product messaging
proof / claims-boundary page
start / quiz or starting-route page
IQ Coach waitlist or coming-soon page
Flow Zone link or separate landing route, if ready
free tools landing page, only after first tool is real
```

---

## 12. Stage 7 — Cloudflare Pages checks

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

Record the answer in:

```text
docs/deployment/cloudflare-pages-map.md
```

or another safe deployment note.

---

## 13. Stage 8 — NiPoGi Ubuntu setup

The NiPoGi should be configured as a runtime/server machine, not as the main browser/admin cockpit.

Install:

```text
Ubuntu updates
Git
Docker Engine
Docker Compose
Node.js only where services need it
SSH server
optional GitHub Actions runner
optional Tailscale/WireGuard/private tunnel
```

Create a service workspace:

```bash
mkdir -p ~/kastel/services
mkdir -p ~/kastel/outputs
mkdir -p ~/kastel/logs
mkdir -p ~/kastel/reviews
mkdir -p ~/repos
```

Generate a NiPoGi-specific SSH key or authenticate GitHub using a device-specific method. Avoid copying the same private key from the Acer or ThinkPad unless necessary.

Clone only repos that NiPoGi actually needs to run:

```bash
cd ~/repos
git clone https://github.com/Mindware-Lab/trident-g-platform
```

For private runtime repos, clone only what the NiPoGi needs, such as private Kastel node repos or service repos.

Keep broad browser/admin access on the ThinkPad.

---

## 14. Stage 9 — NiPoGi runtime responsibilities

Good NiPoGi workloads:

```text
Docker services
scheduled jobs
webhook receivers
metric snapshots
read-only API polling
build/test runners
lightweight local automation
embedding/index jobs where latency is not critical
candidate intent generation for later ThinkPad review
delayed-review reminders
```

Poor NiPoGi workloads:

```text
Stripe/Brevo/Supabase/Cloudflare dashboard administration
GitHub organisation settings
visible browser automation
payment, identity, tax or banking work
final publication decisions
claims-sensitive edits without review
customer communications without ThinkPad approval
```

If a service needs secrets, deploy only the specific service secrets required by that service. Keep the master record in the password manager.

---

## 15. Stage 10 — First NiPoGi/Kastel loop

The first NiPoGi workflow should be intentionally boring and safe.

Do **not** start with autonomous agents, automatic publishing, automatic CRM sending or full dashboard automation.

Start with:

```text
weekly IQ Mindware operating snapshot
```

### First output file

Have NiPoGi produce one Markdown file each week:

```text
~/kastel/outputs/YYYY-WW-iqmindware-snapshot.md
```

Suggested contents:

```md
# IQ Mindware Weekly Snapshot

Week:
Generated:
Reviewed on ThinkPad: no

## Revenue product
Current focus:
IQ Pro sales / activation signal:
Main issue:

## Content and surface intelligence
Published this week:
Search / platform signal:
Content opportunity:

## Conversion and CRM
Segment reviewed:
Campaign idea:
Risk / claim issue:

## Product activation and proof
User friction:
Proof asset needed:
Telemetry / usage note:

## IQ Coach
Build priority:
Open question:
Next build step:

## Flow Zone / HRV
Partnership priority:
Open question:
Next build step:

## Candidate Action Intents
1.
2.
3.

## Candidate Clarify Intents
1.
2.

## Delayed reviews due
1.
2.
```

At first, this file can be filled manually or semi-manually. Later, parts can be populated from APIs.

The first success criterion is:

```text
NiPoGi prepares the review.
ThinkPad makes the decision.
```

---

## 16. Stage 11 — Kastel node folders

If using a private Kastel node repo, start with:

```text
kastel-node-iqmindware/
  docs/
    source-of-truth-registry.md
    business-scaling-hypotheses.md
    weekly-priority-engine.md
    state-niche-fit-rubric.md
  templates/
    action-intent.md
    clarify-intent.md
    delayed-review.md
    script-bank-entry.md
  intents/
    2026-W21/
    2026-W22/
  reviews/
    delayed/
  script-library/
    crm/
    content/
    activation/
    proof/
    partnerships/
  schemas/
    action_intent.schema.json
    clarify_intent.schema.json
    semantic_event.schema.json
```

For the Alex partnership node:

```text
kastel-node-alex-partnership/
  ventures/
    flow-zone/
    cognitive-longevity/
  shared-policies/
  shared-connectors/
  shared-crm/
  shared-weekly-reviews/
```

Do not put private customer exports, private payment exports, broad secrets or relationship-sensitive raw notes in public repos.

---

## 17. Stage 12 — Weekly operating pattern after migration

Once ThinkPad and NiPoGi are stable, use this weekly pattern:

```text
1. NiPoGi prepares the weekly snapshot.
2. ThinkPad reviews and selects top priorities.
3. ThinkPad approves Action / Clarify Intents.
4. ThinkPad creates or approves content, CRM and product changes.
5. NiPoGi records delayed review dates.
6. NiPoGi prepares script-bank candidates.
7. ThinkPad decides what, if anything, becomes reusable operating doctrine.
```

This supports the three business levers:

```text
Content and Surface Intelligence
Conversion and CRM
Product Activation and Proof
```

and the two build tracks:

```text
IQ Coach
Flow Zone / HRV
```

---

## 18. Stage 13 — Codex / AI context on new machines

When starting a fresh Codex or AI coding session on the ThinkPad, useful context is:

```text
Repo: trident-g-platform
Work mainly in:
- products/trident-g-iq/apps/iq-pro for IQ Pro app
- products/trident-g-iq/websites/iqmindware for iqmindware.com website
Branch: main
Deployment: Cloudflare Pages auto-deploys from main
Current quarter priority:
- protect IQ Pro revenue
- build IQ Coach
- build Flow Zone / HRV
- support content/CRM/proof workflows
```

For NiPoGi-related work, add:

```text
NiPoGi is the runtime/server machine.
Do not make it the admin dashboard or human review cockpit.
Use GitHub as code/config truth.
Keep secrets out of the repo.
Generate candidate outputs for ThinkPad review.
Do not send CRM emails, publish content, alter payments or change claims automatically.
```

For Kastel node work, add:

```text
The first node is Kastel Node: IQ Mindware.
The node supports content/surface intelligence, CRM conversion, product activation/proof, IQ Coach build tracking and Flow Zone build tracking.
Every weekly business move should become either an Action Intent or a Clarify Intent.
Every outcome should get a delayed review.
Only repeatable, evidence-backed patterns become scripts.
```

---

## 19. Stage 14 — Cutover checklist

The migration is complete when:

```text
ThinkPad can clone, build and run IQ Pro.
ThinkPad can edit and push trident-g-platform.
ThinkPad can access Cloudflare, Supabase, Stripe, Brevo and GitHub.
Cloudflare Pages deploys from main.
IQMindware website edit path is confirmed.
Real .env values are recreated securely from password manager/cloud dashboards.
NiPoGi has Git, Docker and SSH working.
NiPoGi has only the runtime repos it needs.
NiPoGi can generate one weekly snapshot.
NiPoGi services can be rebuilt from GitHub plus documented secrets.
Acer has no uncommitted work in important repos.
Acer .env, SSH, Obsidian, Zotero, n8n, Docker volume and recovery-code state has been handled.
```

Quarter-specific cutover checks:

```text
IQ Pro revenue workflow still works.
Weekly content workflow still works.
Brevo campaign workflow still works.
IQ Coach build workflow is not blocked by migration.
Flow Zone partnership workflow is not blocked by migration.
Kastel node workflow is helpful rather than creating task overload.
```

---

## 20. Final Acer retirement rule

Before wiping or demoting the Acer, verify:

```powershell
git status --short
```

in every important repo, and confirm:

```text
all meaningful code/content is committed and pushed
all secrets are in the password manager or cloud secret store
all recovery codes are accessible from the ThinkPad and phone
all local-only data has been deliberately copied or discarded
the ThinkPad can do daily work without the Acer
the NiPoGi can run the services assigned to it without the Acer
```

Only then should the Acer stop being treated as the operational source machine.

---

## 21. Anti-scope-drift rule

The migration is successful if it creates:

```text
one reliable cockpit
one reliable runtime node
one safe weekly operating loop
```

It is not successful if it creates:

```text
a second dashboard universe
unreviewed automation
extra publishing burden
CRM risk
claims risk
secret sprawl
new local-only sources of truth
```

For the next quarter, the practical rule is:

```text
Protect the current revenue engine.
Move the cockpit to the ThinkPad.
Start the NiPoGi with one safe Kastel loop.
Only automate after the manual loop is working.
```
