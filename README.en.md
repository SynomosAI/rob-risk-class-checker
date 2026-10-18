# rob-risk-class-checker · Robot risk class & safety safeguard domain

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Domain: rob](https://img.shields.io/badge/domain-rob-9cf.svg)](domain.manifest.json)
[![Status: RESERVED](https://img.shields.io/badge/status-RESERVED-orange.svg)](domain.manifest.json)

> **Status: RESERVED (placeholder · open for adoption)** — This repo scaffolds the
> industry-access four-file skeleton per the platform profile and awaits a qualified
> operator to claim it and fill in real rules.

Turns "what risk class is this robot, and are safeguards in place" into verifiable attributes:
the AI only surfaces prerequisites, it never hands down a run-approval verdict.

**Keywords**: robot risk class · safety safeguard · emergency stop · collaborative operation ·
human oversight · GB 11291.1 · ISO 10218 · robot safety · risk assessment · attribute
verification · red lines · gate-map · privacy-by-default · regulatory compliance · MCP checker

## What this domain covers

Robot risk classification and safety safeguard verification. Risk assessment, guarding and
the emergency-stop function directly affect human safety, especially in collaborative scenarios.
The checker lays out risk factors and safeguard configuration — risk classification must be
done and archived by qualified personnel.

## Domain identity

| Item | Value |
|---|---|
| Domain ID | `rob` (globally unique, never reused) |
| Domain name | Robotics · risk class & safety safeguards |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved since | 2026-09-12 |

## Attribute catalogue

| Key | Type | Meaning |
|---|---|---|
| `rob.risk_class` | enum | low/medium/high/very_high/undetermined |
| `rob.safeguard_measure` | enum | fixed_guard/interlocked_guard/speed_and_separation/power_and_force_limiting/none |
| `rob.emergency_stop_status` | enum | functional/untested/faulty/unknown |
| `rob.collaborative_operation` | boolean | human-robot collaboration present |
| `rob.human_oversight` | enum | none/monitored/supervised/human_decides |

## Red lines (machine-readable)

1. Risk class must be assessed and archived by qualified personnel; AI must not classify it.
2. Never output "ready to run" while safeguard effectiveness is unconfirmed.
3. Never suggest disabling, bypassing or weakening safety functions (E-stop, interlocks, speed limits).

## The four-file access kit

| File | Role |
|---|---|
| `domain.manifest.json` | Domain declaration: attributes, issuer requirements, TTL, red lines |
| `gate-map.json` | Friction per action: silent / warn / confirm / block / require-owner |
| `privacy.json` | Privacy statement: off by default, minimization, withdrawable, erasable |
| `checker.io.json` | Checker MCP tool I/O contract — shows & verifies only, never judges |

## Quick Start

```bash
git clone https://github.com/SynomosAI/rob-risk-class-checker.git
cd rob-risk-class-checker

# Validate the four JSON files with the Python stdlib
python -m json.tool domain.manifest.json > /dev/null
python -m json.tool gate-map.json > /dev/null
python -m json.tool privacy.json > /dev/null
python -m json.tool checker.io.json > /dev/null
```

## Examples

```bash
# List declared attribute keys and allowed values
python -c "import json;m=json.load(open('domain.manifest.json',encoding='utf-8'));[print(a['key'],'->','/'.join(a.get('values',['bool']))) for a in m['attributes']]"
```

```json
{
  "subject_ref": "mpp:cn:9f2c1a7b",
  "attribute_keys": ["rob.risk_class", "rob.emergency_stop_status"],
  "evidence": ["tsa:2026-09-12#sha256:3b1f..."],
  "request_id": "req-20260912-0001"
}
```

The checker answers only with `shown / missing / expired / unverifiable` plus the
provenance chain. It never returns "ready to run", "risk classified", or safety approval.

## Core principles

The platform is an arena, not a shelf. The checker answers only "is this claim verifiable,
and what prerequisite is missing" — never "is this compliant, should it be done".

## How to adopt

This domain is open to qualified operators: fork the repo, fill in `operator` and
`checker_endpoint`, align attributes and red lines with current rules, run the platform
self-checker (all five criteria must pass), then open a PR with credentials.

## License

Code and configuration are MIT-licensed. Documentation copyright remains with SynomosAI.
See [LICENSE](LICENSE).

© 2026 SynomosAI. All rights reserved.
