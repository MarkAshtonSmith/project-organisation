# Trident Alpha Two-Computer Allocation

## Decision

Run Trident Alpha as a two-computer system:

```text
Computer 1: Blue Rail engineering workstation
Computer 2: Red Rail local research node
```

This mirrors the Kastel Stack hardware guidance. The Blue Rail computer can be
tool-rich and internet-facing. The Red Rail computer should be more restricted,
encrypted, and used for sensitive strategy, private evidence, local databases,
and broker-adjacent work.

## Computer 1: Blue Rail Engineering Workstation

Use this computer for:

- VS Code/Codex/Cursor work on public or low-sensitivity repo files,
- GitHub commits, pull requests, issues, and project management,
- documentation and architecture edits,
- public web research,
- non-sensitive strategy notes,
- synthetic-data tests,
- dashboards that do not expose secrets or private broker/account data,
- cloud tooling setup,
- CI and repo maintenance,
- public/publishable summaries after review.

Allowed Alpha tasks:

```text
edit trident-alpha-ground-truth docs
edit trident-g-kernel code and tests
edit strategy-research templates and redacted reports
run unit tests with synthetic data
review diffs
prepare GitHub issues
draft cockpit UI
draft public-safe macro summaries
```

Do not use this computer as the durable home for:

- live broker credentials,
- private account exports,
- private paper-fill logs linked to account identity,
- raw proprietary market datasets,
- private strategy evidence not ready for Git,
- unredacted research archive,
- local vector indexes over private strategy material.

## Computer 2: Red Rail Local Research Node

Use this computer for:

- local Postgres/TimescaleDB,
- private market data cache,
- private strategy test records,
- paper-execution logs,
- broker API credentials, if any are used,
- local notebooks with private inputs,
- local vector/graph store for sensitive strategy material,
- local inference or redaction proxy,
- profitability evidence packets before redaction,
- risk and capital assumptions,
- encrypted backups.

Allowed Alpha tasks:

```text
run Docker Compose runtime
run market ingest jobs
run criticality scans over local data
run backtests and walk-forward tests
run paper-trading adapters
store private paper order outcomes
store private profitability reports
run slippage/stake/regime stress tests
generate redacted reports for GitHub
```

The Red Rail node is the correct place for anything that could create financial,
privacy, strategy, or account-security risk if leaked.

## Cloud / External Services

Use cloud services for:

- GitHub as code/config truth,
- CI on synthetic or redacted fixtures,
- broker paper APIs where needed,
- public or licensed market-data APIs,
- public-safe dashboards only after review.

Do not put these in cloud by default:

- unredacted broker credentials,
- private account statements,
- private strategy evidence,
- raw proprietary data,
- private embeddings,
- unpublished high-sensitivity strategy notes.

## Workflow

### Code and docs

```text
Blue Rail workstation
-> edit code/docs
-> commit to GitHub
-> pull to Red Rail node for private runtime tests
```

### Private research run

```text
Red Rail node
-> ingest data
-> run scan/backtest/paper test
-> write private evidence packet
-> produce redacted summary
-> Blue Rail workstation commits redacted summary if safe
```

### Strategy banking

```text
Red Rail node
-> evidence ladder review
-> wrapper/stake/macro tests
-> delayed review
-> bank/revise/retire decision
-> redacted Phi-script metadata may be mirrored to GitHub
```

## Task Matrix

| Task | Blue Rail workstation | Red Rail local node |
|---|---|---|
| Ground-truth docs | primary | mirror if needed |
| Runtime code edits | primary | pull/test |
| Unit tests with synthetic fixtures | primary | secondary |
| Docker runtime | optional light test | primary |
| Local Postgres/TimescaleDB | optional dev only | primary |
| Market data cache | no private cache | primary |
| Broker paper adapter | no secrets | primary |
| Broker/live credentials | never | restricted, if ever approved |
| Backtests with public samples | allowed | primary for serious runs |
| Backtests with proprietary/private data | no | primary |
| Paper execution logs | redacted only | primary |
| Profitability reports | redacted only | primary |
| GitHub push | primary | only if operationally necessary |
| Public-safe summaries | primary after review | source generation |
| Private strategy notebooks | no | primary |
| Local LLM/redaction | optional public | primary |

## Hard Rules

1. No live-capital execution in the MVP.
2. No AI tool on the Blue Rail computer gets broker credentials.
3. No raw private strategy/account data in GitHub.
4. No cloud CI job uses real broker secrets.
5. No macro/news signal bypasses the Trade Action Intent gate.
6. Redacted summaries must preserve claim boundaries and uncertainty.
7. The Red Rail node must have encrypted backups before serious paper testing.

