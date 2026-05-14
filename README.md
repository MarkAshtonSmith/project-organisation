# Device and GitHub Organisation Division of Labour

Last reviewed: 2026-05-13

This note summarises the realistic split between the NiPoGi mini-PC and the ThinkPad across the current GitHub organisation partition.

It is intentionally practical rather than idealised. The NiPoGi should be treated as a small, persistent machine layer. The ThinkPad should remain the human authority, review, coding, dashboard and mobile working layer.

The core operating principle is:

```text
Public framework ≠ live implementation.
```

Public repositories should contain reusable code, specifications, templates, schemas, public documentation and sanitised examples.

Private node repositories should contain real operating assumptions, connector configuration, weekly reviews, AH-MAS workflows, Action / Clarify Intent histories and deployment-specific details.

---

## Current GitHub Organisation Partition

| Organisation | Role in the ecosystem | Current repository pattern | Ground-truth role |
|---|---|---|---|
| `Mindware-Lab` | Commercial product, product websites, app delivery, IQ Mindware protocols and applied Trident-G product work | `trident-g-platform`, `mindware-ground-truth` or `trident-g-ground-truth`, `Zone-Coach`, `IQ-Coach`, product/collaboration repos | Applied product/protocol truth for IQ Mindware products |
| `Kastel-Stack` | Supervised adaptive operating system, public framework, node template and private business node deployments | `.github`, `kastel-ground-truth`, `kastel-stack`, `kastel-node-template`, private node repos such as `kastel-node-iqmindware` and `kastel-node-alex-AH-MASship` | Anti-capture, human-supervised operating-system truth |
| `Trident-Alpha-Lab` | Private computational trading lab for market research, alpha signals, backtesting, paper/live separation, execution-support systems and risk controls | trading strategy repos, market-data pipelines, backtesting notebooks, execution/risk tooling and `trident-alpha-ground-truth` | Private trading research, risk and execution-boundary truth |
| `Trident-Cloud-Lab` | Public Trident-G theory, open methods, research-facing material and public lab framing | `Trident-G-theory`, `Cloud-Lab-Ground-Truth`, `research-platform` | Canonical public theory and research truth |

The main conceptual boundary is:

```text
Trident-Cloud-Lab = canonical public theory
Mindware-Lab = applied commercial product/protocol layer
Kastel-Stack = anti-capture business operating-system layer
Trident-Alpha-Lab = private computational trading layer
```

Do not let `Mindware-Lab` and `Trident-Cloud-Lab` both become the master source for Trident-G theory.

Use:

```text
Trident-Cloud-Lab = public theory and research layer
Mindware-Lab = applied product and protocol implementation
```

---

## GitHub Organisation Profile Repositories

Each public-facing GitHub organisation should have a `.github` profile repository.

Recommended:

```text
Mindware-Lab/.github
Kastel-Stack/.github
Trident-Cloud-Lab/.github
```

Optional or private/minimal:

```text
Trident-Alpha-Lab/.github
```

Each `.github` organisation profile should include:

```text
profile/README.md
CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
ISSUE_TEMPLATE/
```

The organisation profile README should answer:

```text
what the organisation is for
which repos matter first
what is public versus private
where the ground-truth repo lives
how contributors should engage, if relevant
```

For `Kastel-Stack`, the public profile should explicitly include the anti-capture posture:

```text
Kastel Stack is an open, human-supervised, anti-capture adaptive scaling OS for sovereign, digitally legible enterprises.
```

---

## Constitutional Split

```text
NiPoGi = machine layer
ThinkPad = human authority layer
GitHub = code, config and specification truth
Cloud services = source-of-truth systems for their own domains
Password manager / encrypted vault = secrets and identity truth
```

The NiPoGi should prepare, run, observe, snapshot and queue.

The ThinkPad should decide, review, edit, approve, publish and administer.

A shorter rule:

```text
NiPoGi may compute, ingest, simulate, monitor and report.
ThinkPad decides, approves, interprets and authorises.
```

---

## Device Roles

| Area | NiPoGi mini-PC | ThinkPad |
|---|---|---|
| Primary role | Persistent runtime node | Human cockpit and mobile workstation |
| Best at | Always-on services, scheduled jobs, Docker, webhooks, local runners, lightweight background processing | Coding, writing, browser dashboards, visible browser automation, GitHub Projects, review and approvals |
| Should avoid | Becoming the business dashboard, holding broad personal/admin sessions, storing unnecessary identity or recovery material | Hosting critical always-on services that fail when the laptop sleeps, travels or is offline |
| Working style | Headless or mostly headless; accessed by SSH, remote VS Code/Cursor, tunnel or private network | Interactive; browser profiles, IDE, admin dashboards, meetings, writing and manual review |
| Failure assumption | Can be rebooted/rebuilt from GitHub, Docker files and service secrets | Can be replaced if GitHub, password manager, cloud services and backups are healthy |

---

## Organisation-by-Organisation Allocation

### `Mindware-Lab`

Purpose: commercial product and delivery layer.

`Mindware-Lab` contains the applied IQ Mindware product ecosystem. It should not be the canonical source for all Trident-G theory. It should hold the applied product, protocol, claims, app delivery and commercial implementation layer.

ThinkPad owns:

- Product coding and review in `trident-g-platform`, `Zone-Coach`, `IQ-Coach` and related product repos.
- Website copy, product pages, proof pages, claims-sensitive wording and public positioning.
- Cloudflare, Supabase, Stripe, Brevo and GitHub dashboard review.
- GitHub Projects, issues, pull requests and release decisions.
- App architecture decisions and public product-roadmap judgement.
- Pricing, offers, product bundles and customer-facing claims.

NiPoGi owns:

- Local runtime services that support product operations.
- Webhook receivers and background jobs where they are not better hosted on Cloudflare/Supabase.
- Scheduled snapshots for CRM, product activation, telemetry summaries and deployment checks.
- Optional self-hosted GitHub Actions runner work for build/test jobs that are safe to run locally.
- Repeatable product-support jobs that prepare summaries for ThinkPad review.

Practical rule:

```text
Mindware product truth can be public-facing,
but admin decisions stay on the ThinkPad.
NiPoGi may run the plumbing, not the commercial judgement.
```

---

### `Kastel-Stack`

Purpose: supervised automation framework, anti-capture infrastructure and private node operations.

`Kastel-Stack` should make the anti-capture posture explicit. It is not just a business-automation framework. It is a human-supervised, source-of-truth-grounded, polycentric operating system designed to help independent operators grow without surrendering judgement to black-box platforms, hyperscaler lock-in, venture-capital growth logic or unsupervised agentic automation.

Recommended organisation structure:

```text
Kastel-Stack/
├─ .github                         public organisation profile
├─ kastel-ground-truth             public canonical design truth
├─ kastel-stack                    public framework / reference implementation
├─ kastel-node-template            public starter for private Kastel nodes
├─ kastel-node-iqmindware          private live IQ Mindware / HRP Lab node
└─ kastel-node-alex-AH-MASship    private AH-MASship node
```

Recommended AH-MASship node structure:

```text
kastel-node-alex-AH-MASship
├─ ventures/
│  ├─ flow-zone/
│  └─ cognitive-longevity/
├─ shared-policies/
├─ shared-connectors/
├─ shared-AH-MAS-crm/
└─ shared-weekly-reviews/
```

This pattern can be extended to other AH-MASships:

```text
kastel-node-[AH-MAS-name]-AH-MASship
```

or, where the venture rather than the AH-MAS is the organising unit:

```text
kastel-node-[venture-name]
```

ThinkPad owns:

- Human review of weekly Action / Clarify Intents.
- Editing framework docs, policy packs, node templates and public-facing explanatory material.
- GitHub Projects and issue triage.
- Decisions involving claims, payments, privacy, AH-MASships, publishing, customer data or strategy.
- Public/private boundary decisions.
- Anti-capture, governance and human-supervision wording.
- AH-MAS governance decisions.

NiPoGi owns:

- The private node runtime for `kastel-node-iqmindware`.
- Later, selected runtime jobs for `kastel-node-alex-AH-MASship`, if appropriate.
- Docker services, scheduled jobs, kernel monitor, orchestrator and delayed-review checks.
- Metric snapshot collection and candidate intent generation.
- Local service folders such as orchestrator, webhook receiver and consolidation jobs.
- Draft generation and queue preparation for ThinkPad review.

Practical rule:

```text
Kastel is the strongest use case for the NiPoGi.
But its outputs should be proposals for ThinkPad review,
not autonomous business decisions.
```

Anti-capture rule:

```text
Kastel must preserve human judgement, source-of-truth discipline,
polycentric governance, dependency replaceability and public/private boundaries.
It must not drift into generic automation, surveillance tooling or centralised agentic control.
```

---

### `Trident-Alpha-Lab`

Purpose: private computational trading research and execution-support layer.

`Trident-Alpha-Lab` should be private by default. It is financially sensitive and should have the strongest boundaries around automation, credentials, broker access, live execution, leverage, capital allocation and records.

ThinkPad owns:

- Trading research judgement, strategy specification, hypothesis review and sensitive market notes.
- Interactive notebooks, backtest interpretation, chart review, model design and architecture choices for trading systems.
- Broker, exchange, data-vendor and trading dashboard sessions.
- Risk decisions, position-sizing assumptions, live/paper trading review, P&L review and tax/accounting records.
- Approval of anything that moves from research into paper trading, live execution or reusable infrastructure.
- Any decision involving broker access, capital allocation, withdrawals, leverage or production trading infrastructure.

NiPoGi owns:

- Reproducible backtests, walk-forward evaluations and scheduled strategy checks where background compute is useful.
- Market-data ingestion, normalisation, cache refreshes and read-only data quality checks.
- Paper-trading or simulation services that do not require broad admin access.
- Monitoring, alerts and reports that queue findings for ThinkPad review.
- Deterministic scripts for feature generation, signal scans and risk reports.

Practical rule:

```text
Alpha Lab is private and financially sensitive by default.
NiPoGi may run repeatable data and evaluation plumbing,
but trading authority, broker access, capital allocation and live execution decisions stay on the ThinkPad.
```

Hard boundaries:

```text
No live execution authority on NiPoGi by default.
No broker withdrawal authority on NiPoGi.
No leverage or capital-allocation automation without explicit human approval.
No private market-data vendor material in public repos.
No P&L, tax records or broker records in public repos.
No research output should be treated as live trading authority.
```

If execution infrastructure is ever developed, separate:

```text
research
paper trading
execution support
live execution
risk review
```

with stricter gates at each step.

---

### `Trident-Cloud-Lab`

Purpose: public research/theory/lab-facing materials.

`Trident-Cloud-Lab` should be the canonical public Trident-G theory and research home.

ThinkPad owns:

- Public theory writing, repo curation, diagrams, review and publication decisions.
- Any manual edits to public-facing research material.
- Browser-based work involving external research platforms, publishing or academic accounts.
- Decisions about what becomes public-facing theory, methods or evidence material.

NiPoGi owns:

- Optional scheduled checks, static build checks, link checks and lightweight publication support.
- Local mirrors or backups of public artefacts where useful.
- Reproducible public artefact generation where no private or sensitive data is involved.

Practical rule:

```text
Cloud Lab can be public and inspectable,
but publication judgement remains on the ThinkPad.
```

Keep out of public Cloud Lab repos:

```text
private student data
commercial app telemetry
customer data
AH-MAS materials
sensitive business notes
unreviewed clinical-style claims
private protocol iterations not ready for public interpretation
```

---

## Workload Placement Rules

Use the NiPoGi for:

- Docker services.
- Scheduled jobs and cron-style checks.
- Webhook receivers.
- Metric snapshots.
- Read-only API polling.
- Local runners.
- Embedding/index generation.
- Deterministic scripts.
- Draft generation and queue preparation.
- Lightweight publication checks.
- Backtest and data-quality runs where safe.
- Anything useful when running overnight or while the ThinkPad is closed.

Use the ThinkPad for:

- GitHub organisation settings.
- GitHub Projects and issue boards.
- Pull request review and merge decisions.
- Product copy, claims and proof language.
- Stripe, Brevo, Supabase, Cloudflare and account dashboards.
- Password manager and admin sessions.
- Browser automation that needs a visible browser.
- Writing, research judgement and public release decisions.
- AH-MAS discussions and relationship-sensitive material.
- Broker, exchange and trading-dashboard sessions.
- Anything involving money, identity, customer data, compliance, claims, AH-MASships, reputation, broker access or live trading authority.

---

## What Should Live Where

| Item | Source of truth | NiPoGi | ThinkPad |
|---|---|---|---|
| Code and specs | GitHub | Clone runtime repos only | Clone active repos |
| Public product content | GitHub | Build/check where useful | Edit/review/publish |
| Public theory content | GitHub / public research platforms | Static checks, link checks | Write/review/publish |
| Private node config | Private GitHub repo plus service secrets | Runtime copy | Admin/review copy |
| Production secrets | Password manager / cloud secret manager | Service-only secrets | Admin access |
| Customer/payment data | Stripe, Brevo, Supabase or accounting system | Read-only/specific API access if needed | Dashboard/admin review |
| Trading data and records | Broker, exchange, data vendor, accounting system or private Alpha Lab repo | Read-only ingestion, local caches, simulations and reports | Broker dashboards, P&L review, risk decisions, tax/accounting review |
| Research notes | Appropriate private/public repo or vault | Optional reproducible artefacts | Primary writing and judgement |
| Build artefacts | Recreated from source | Temporary only | Temporary only |
| Local caches | Disposable | Allowed | Allowed |
| Official identity details | Password manager / encrypted vault | Avoid | Encrypted vault only |
| Recovery codes | Password manager plus offline backup | Avoid | Encrypted and offline backup |

---

## Near-Term Operating Pattern

1. Work interactively on the ThinkPad.
2. Keep GitHub clean: commit and push meaningful changes.
3. Pull selected runtime repos onto the NiPoGi.
4. Let NiPoGi run scheduled checks, local services and draft/snapshot generation.
5. Have NiPoGi write outputs back as files, issues, logs or summaries.
6. Review those outputs on the ThinkPad.
7. Only after review should outputs become public content, product changes, customer actions, AH-MAS communications, trading decisions or business decisions.

For Kastel specifically:

```text
NiPoGi generates candidate Action / Clarify Intents.
ThinkPad reviews and approves the weekly priority list.
NiPoGi may execute only low-risk, reversible, evidence-backed Auto actions.
Draft, Escalate and Blocked actions remain human-gated.
```

---

## Capacity-Based Reality Check

The NiPoGi is valuable because it is persistent, not because it is the most powerful machine. Treat it as a low-power server:

- Good for small Docker services, webhooks, cron jobs, static checks and lightweight local automation.
- Acceptable for small local models or embedding jobs if latency is not critical.
- Useful for scheduled backtests, snapshots and reproducible reports if workloads are modest.
- Poor fit for heavy interactive IDE work, Android Studio, graphics-heavy design tools, large local model workloads or anything that benefits from a screen and fast human iteration.

The ThinkPad is valuable because it is the control surface:

- Good for daily coding, writing, browser dashboards, review, approval and visible automation.
- Acceptable for local development servers, builds and tests.
- Best for public release decisions, product judgement, AH-MAS judgement, trading judgement and claim-sensitive review.
- Poor fit for always-on production-ish services because sleep, travel, updates and battery state make it unreliable as infrastructure.

---

## Guardrails

- Do not put broad admin browser sessions on the NiPoGi.
- Do not copy the same private SSH key everywhere; use device-specific keys.
- Do not commit `.env` files or local secrets.
- Do not automate outbound email, payment changes, customer-data operations or public claims without ThinkPad review.
- Do not automate live trading, broker account changes, withdrawals, leverage changes or capital allocation without ThinkPad review and explicit approval.
- Do not let local device folders become the hidden source of truth. If it matters, put the safe version in GitHub or the appropriate cloud system.
- Do not move private node details into public repos without sanitising them first.
- Do not move trading strategies, market-data vendor material, broker records or P&L details into public repos.
- Do not place raw customer data or private payment exports in ChatGPT or Claude project sources.
- Do not upload broker credentials, recovery codes, live account details or sensitive P&L exports to ChatGPT or Claude.
- Do not let Mindware-Lab and Trident-Cloud-Lab diverge into competing versions of Trident-G theory.

---

## Workspace Folder Structure

Use the same four-organisation prefixes across ChatGPT, Claude Pro, browser bookmarks and Google Drive/Workspace. This keeps thinking work, navigation and documents aligned with GitHub rather than creating another hidden taxonomy.

Top-level structure:

```text
00 Inbox - Triage
01 Active This Week
10 Mindware-Lab - Product and Commercial
20 Kastel-Stack - Automation and Node Ops
30 Trident-Alpha-Lab - Computational Trading
40 Trident-Cloud-Lab - Public Research and Theory
50 Shared Assets - Brand, Legal, Finance, Admin
90 Archive
```

---

## Mindware-Lab Workspace Structure

```text
10 Mindware-Lab
  01 Trident-G Platform
  02 Applied Product Ground Truth
  03 IQ Coach / IQ Pro App
  04 IQMindware Website
  05 Capacity Gym
  06 Zone Coach
  07 G Tracker / Assessments
  08 Resilience Coach
  09 Pricing, Stripe, Entitlements
  10 Claims, Safety, Evidence
  11 Substack and Marketing
  12 CRM, Brevo, Customer Ops
  13 Deployment - Cloudflare, Supabase, GitHub Pages
```

---

## Kastel-Stack Workspace Structure

```text
20 Kastel-Stack
  01 Kastel Framework
  02 Kastel Ground Truth
  03 kastel-node-iqmindware
  04 kastel-node-alex-AH-MASship
  05 Weekly Review / Action Queue
  06 Webhooks and Scheduled Jobs
  07 Private Node Config
  08 Policies and Guardrails
  09 Anti-Capture and Governance
  10 NiPoGi Runtime Notes
```

For the Alex AH-MASship node:

```text
kastel-node-alex-AH-MASship
  ventures
    flow-zone
    cognitive-longevity
  shared-policies
  shared-connectors
  shared-AH-MAS-crm
  shared-weekly-reviews
```

---

## Trident-Alpha-Lab Workspace Structure

```text
30 Trident-Alpha-Lab
  01 Market Research
  02 Trading Strategies
  03 Alpha Signals
  04 Backtesting
  05 Execution / Broker APIs
  06 Risk, Position Sizing, Drawdown
  07 Data Pipelines
  08 Notebooks and Experiments
  09 Paper Trading
  10 Live Trading Ops
  11 Compliance / Tax / Records
  12 Archive - Retired Strategies
```

---

## Trident-Cloud-Lab Workspace Structure

```text
40 Trident-Cloud-Lab
  01 Trident-G Theory
  02 Cloud Lab Ground Truth
  03 Open Methods and Ethics
  04 Public Research Platform
  05 Publications / Diagrams
  06 Public Evidence Packs
```

---

## Recommended ChatGPT Projects

Create ChatGPT Projects by operating context, not by every repository.

Use separate projects when the brand, governance, claims, AH-MAS obligations or source files differ.

Recommended structure:

```text
00 Inbox - Fast Triage
01 Active - This Week

ML - Product Cockpit
ML - Claims and Evidence
ML - Content and Conversion

AH-MAS - Flow Zone and Cognitive Longevity

KS - Kastel Framework
KS - Kastel Node Ops
KS - Anti-Capture and Governance

TA - Trading Cockpit
TA - Strategy and Backtesting
TA - Risk and Execution

TC - Trident-G Theory
TC - Cloud Lab and Open Methods
```

### `00 Inbox - Fast Triage`

Purpose:

```text
quick sorting
rough notes
where-does-this-belong decisions
repo/project routing
turn messy notes into tasks
```

Sources:

```text
one-page organisation map
device and GitHub organisation division-of-labour note
```

Keep this light.

### `01 Active - This Week`

Purpose:

```text
current weekly priorities across all organisations
current blockers
current Action / Clarify Intent queues
what needs review this week
```

Sources:

```text
current weekly review
current priority list
current roadmap snapshot
current open questions
device/org division-of-labour note
```

Keep this current, not archival.

### `ML - Product Cockpit`

Purpose:

```text
IQ Mindware / HRP Lab product ecosystem
product architecture
app-roadmap decisions
website priorities
offer and pricing decisions
```

Sources:

```text
Mindware-Lab applied ground truth
IQ Mindware product ecosystem overview
Trident-G applied protocol docs
Zone Coach protocol
IQ Coach protocol
Resilience Coach protocol
G Tracker / proof architecture
current product roadmap
current app repo READMEs
pricing / offer architecture notes
```

### `ML - Claims and Evidence`

Purpose:

```text
claims boundaries
proof pages
evidence summaries
protocol validation
research-to-product translation
```

Sources:

```text
Trident-G theory core document
transfer theory summary
protocol and applications document
proof-page plan
claims ladder
research / theory references
evidence and validation roadmap
public protocol docs
ethics and algorithmic transparency notes
```

This project should prevent overclaiming.

### `ML - Content and Conversion`

Purpose:

```text
IQ Mindware content generation
channel strategy
Brevo sequences
Substack
YouTube
LinkedIn
feeder-site routing
```

Sources:

```text
IQ Mindware content strategy
iqmindware.com site architecture
Substack positioning
Brevo segment strategy
YouTube content plan
LinkedIn B2B content plan
highiqpro.com feeder strategy
i3mindware.com feeder strategy
proof-page summary
product page summaries
```

### `AH-MAS - Flow Zone and Cognitive Longevity`

Purpose:

```text
Alex AH-MASship ventures
Flow Zone
Cognitive Longevity
shared B2B / AH-MAS route
non-IQ branding
AH-MASship governance
```

Sources:

```text
kastel-node-alex-AH-MASship ground truth
Flow Zone business model / protocol notes
Cognitive Longevity business model / protocol notes
AH-MAS governance note
shared AH-MAS CRM structure
shared claims boundaries
B2B pilot offer architecture
weekly AH-MASship review template
current AH-MASship roadmap
Trident-G transfer summary
protocol-and-applications summary
Kastel state–niche fit summary
Kastel Action / Clarify Intent summary
```

Do not upload the full IQ Mindware commercial strategy unless the specific AH-MASship decision needs it.

### `KS - Kastel Framework`

Purpose:

```text
public Kastel Stack framework
schemas
docs
templates
contributor-facing material
```

Sources:

```text
kastel-ground-truth
kastel-stack/docs/KASTEL_STACK_GROUND_TRUTH.md
architecture docs
G Kernel spec
state–niche fit spec
Action Intent spec
Clarify Intent spec
script banking rules
weekly priority engine spec
minimal schema section
public/private boundary doc
```

### `KS - Kastel Node Ops`

Purpose:

```text
private node implementation
NiPoGi runtime
weekly reviews
action queues
connector config
deployment planning
```

Sources:

```text
kastel-node-iqmindware ground truth
INITIAL_FOUR_LEVERS.md
WEEKLY_PRIORITY_PROCESS.md
source-of-truth-map.yaml
gates.yaml
weekly-prioritisation.yaml
NiPoGi runtime notes
device and GitHub organisation division-of-labour note
current weekly reviews
current Action / Clarify Intent templates
```

Treat this as private.

### `KS - Anti-Capture and Governance`

Purpose:

```text
anti-capture posture
shark tooth sovereignty
source-of-truth discipline
human supervision
public/private boundaries
AH-MAS governance
```

Sources:

```text
kastel-ground-truth anti-capture docs
shark tooth sovereignty doc
human supervision doctrine
public/private boundary doc
source-of-truth registry
security and privacy policy
polycentric management model
AH-MAS governance templates
```

Core instruction:

```text
Preserve anti-capture, human-supervised, source-of-truth-grounded, polycentric platform sovereignty principles.
```

### `TA - Trading Cockpit`

Purpose:

```text
high-level trading research cockpit
hypothesis review
market notes
trading journal interpretation
weekly alpha review
```

Sources:

```text
trident-alpha-ground-truth
risk doctrine
research boundaries
paper/live trading separation policy
trading journal template
market research taxonomy
data source map
```

Do not upload broker credentials, live account details, recovery codes, payment details or sensitive P&L exports.

### `TA - Strategy and Backtesting`

Purpose:

```text
strategy design
backtest interpretation
feature engineering
evaluation discipline
```

Sources:

```text
strategy design templates
backtesting protocol
walk-forward validation rules
data pipeline docs
feature generation docs
risk metric definitions
notebook README files
```

### `TA - Risk and Execution`

Purpose:

```text
risk controls
execution boundaries
paper/live separation
operational safeguards
```

Sources:

```text
risk doctrine
position sizing boundaries
drawdown rules
execution gating policy
paper trading policy
live execution approval checklist
broker/API boundary notes
tax/accounting record policy
```

Core instruction:

```text
Never treat research output as live trading authority.
Require explicit human approval for anything involving broker access, live execution, leverage, withdrawals, capital allocation or production trading infrastructure.
```

### `TC - Trident-G Theory`

Purpose:

```text
canonical public Trident-G theory development
```

Sources:

```text
Trident-G theory of general adaptive intelligence
transfer theory summary
Trident-G psychopathology framework if relevant
core references
glossary
theory roadmap
diagram notes
paper drafts
```

This should be the canonical theory project, not Mindware-Lab.

### `TC - Cloud Lab and Open Methods`

Purpose:

```text
public research/lab-facing materials
open protocols
ethics
public evidence packs
```

Sources:

```text
Cloud Lab ground truth
open methods docs
ethics and transparency notes
public protocol docs
research platform docs
public evidence pack templates
publication roadmap
```

Keep this public-clean.

Avoid uploading:

```text
private app telemetry
customer data
student data
AH-MAS materials
sensitive business notes
```

---

## ChatGPT Project Source Strategy

Use this rule:

```text
Each ChatGPT project gets:
1. one ground-truth file
2. one current roadmap or priority file
3. one glossary or source-of-truth map
4. only the live docs it needs
```

Do not upload everything everywhere. Too much context makes each project less sharp.

For each project, use sources like this:

```text
ground truth = stable doctrine
roadmap = current direction
schema/map = working structure
weekly review = live priority
```

---

## Recommended Claude Pro Projects

Use the same project names as ChatGPT where possible.

Claude Pro is especially useful for:

```text
long-form theory drafts
policy documents
claims review
careful document restructuring
large context synthesis
```

Recommended Claude projects:

```text
ML - Claims and Evidence
ML - Content and Conversion
AH-MAS - Flow Zone and Cognitive Longevity
KS - Kastel Framework
KS - Anti-Capture and Governance
TC - Trident-G Theory
TC - Cloud Lab and Open Methods
TA - Strategy and Backtesting
TA - Risk and Execution
```

---

## Recommended Bookmark Folders

```text
00 Daily Cockpit
  GitHub Dashboard
  GitHub Projects
  Cloudflare
  Supabase
  Stripe
  Brevo
  ChatGPT
  Claude
  Google Drive

10 Mindware-Lab
  GitHub Repos
  Cloudflare Pages
  Supabase Projects
  Stripe Products
  Brevo Lists
  IQMindware Site
  Product References

20 Kastel-Stack
  GitHub Repos
  Node Dashboards
  Automation Docs
  Logs / Monitoring

30 Trident-Alpha-Lab
  Broker / Exchange
  Market Data
  Research
  Charting
  Economic Calendar
  Backtesting Tools
  GitHub Repos
  Journals / Logs
  Tax / Accounting

40 Trident-Cloud-Lab
  Public Repos
  Research Publishing
  Open Methods
```

---

## Recommended Google Drive / Workspace Folders

```text
Trident-G Workspace
  00 Inbox - Unsorted
  01 Active This Week

  10 Mindware-Lab
    Product Specs
    Website Copy
    Pricing and Offers
    Claims and Evidence
    Customer / CRM Exports
    Marketing and Substack
    Meeting Notes

  20 Kastel-Stack
    Node Ops
    Automation Policies
    Weekly Reviews
    Private Runbooks
    AH-MAS Node Notes

  30 Trident-Alpha-Lab
    Research Notes
    Strategy Specs
    Backtest Reports
    Trading Journal
    Risk Reviews
    Data Vendor Docs
    Broker / Exchange Docs
    Tax and Accounting
    Screenshots / Charts
    Archive

  40 Trident-Cloud-Lab
    Public Theory
    Open Methods
    Publication Drafts
    Diagrams

  50 Shared Assets
    Brand
    Logos
    Screenshots
    Legal
    Finance
    Admin
    Identity - encrypted only

  90 Archive
```

Source-of-truth rule:

```text
GitHub remains the durable source of truth for code, specifications and safe configuration.
Google Drive/Workspace is for editable business documents, trading records, screenshots and working drafts.
ChatGPT and Claude Pro are thinking workspaces.
Bookmarks are navigation only.
Password manager / encrypted vault is the truth for secrets and identity material.
Cloud systems remain source-of-truth systems for their own operational domains.
```

---

## Local Machine Folder Structure

On the NiPoGi Ubuntu runtime node:

```text
~/kastel/
├─ repos/
│  ├─ kastel-stack/
│  ├─ kastel-node-template/
│  ├─ kastel-node-iqmindware/
│  └─ kastel-node-alex-AH-MASship/
│
├─ services/
│  ├─ kastel-orchestrator/
│  ├─ kernel-monitor/
│  ├─ webhook-receiver/
│  ├─ embedding-service/
│  ├─ consolidation-jobs/
│  └─ n8n/
│
├─ secrets/
│  ├─ kastel-node-iqmindware.env
│  ├─ kastel-node-alex-AH-MASship.env
│  ├─ stripe-webhooks.env
│  ├─ brevo.env
│  ├─ supabase.env
│  └─ cloudflare.env
│
├─ logs/
├─ backups/
└─ runtime/
```

On the ThinkPad:

```text
C:\Users\Mark\repos\
├─ kastel-ground-truth\
├─ kastel-stack\
├─ kastel-node-template\
├─ kastel-node-iqmindware\
└─ kastel-node-alex-AH-MASship\
```

The ThinkPad remains your:

```text
coding cockpit
GitHub Projects UI
dashboard/admin UI
human review layer
writing and documentation layer
```

The NiPoGi remains your:

```text
persistent Docker runtime
webhook receiver
scheduled jobs host
kernel/orchestrator host
service layer
```

---

## Short Version

```text
Mindware-Lab       = product and commercial delivery
Kastel-Stack       = anti-capture supervised operating kernel and private node runtime
Trident-Alpha-Lab  = private computational trading lab
Trident-Cloud-Lab  = public theory, research and lab-facing materials

NiPoGi             = always-on machine layer
ThinkPad           = human cockpit and authority layer
GitHub             = durable code/spec/config truth
Cloud services     = operational truth for their own domains
Password manager   = secrets and identity truth
```
