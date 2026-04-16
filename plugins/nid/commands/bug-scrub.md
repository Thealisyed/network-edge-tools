---
description: Analyze untriaged NID bugs in OCPBUGS and post AI triage comments directly on each issue before bug scrub meetings
argument-hint: "[--since last-week] [--issue OCPBUGS-XXXXX] [--dry-run]"
---

## Name
nid:bug-scrub

## Synopsis
```
/nid:bug-scrub [--since last-week] [--issue OCPBUGS-XXXXX] [--dry-run]
```

## Description
The `nid:bug-scrub` command prepares the NID (Network Ingress & DNS) team for bug scrub meetings by analyzing untriaged bugs and posting structured triage comments **directly on each Jira issue**. Instead of generating a separate document, the analysis lives where the team will see it -- on the bug itself.

This is a thin wrapper around `/bug-triage:scrub` (from the `bug-triage` plugin in ai-helpers) with NID team configuration pre-filled.

Run this before your standing bug scrub meeting. When someone opens a bug during the meeting, the AI triage comment is already there with routing checks, importance signals, duplicate candidates, and a recommended action.

## Implementation

This command delegates to `/bug-triage:scrub` with NID-specific arguments pre-filled:

```
/bug-triage:scrub --team "Network Ingress and DNS" --team-docs plugins/nid/team-docs [--since {since}] [--issue {issue}] [--dry-run]
```

1. **Resolve team-docs path**: The `--team-docs` path is relative to the network-edge-tools repo root. Resolve it to an absolute path before passing to `/bug-triage:scrub`.

2. **Forward arguments**: Pass through all user-provided arguments (`--since`, `--issue`, `--dry-run`) unchanged.

3. **Execute**: Run the general `/bug-triage:scrub` command which handles:
   - Team lookup from `team_component_map.json` (components: "Networking / router", "Networking / DNS")
   - Loading NID team docs (sub-areas, routing guide) from `plugins/nid/team-docs/`
   - Full triage analysis per the `bug-triage` plugin's SKILL.md
   - Comment posting with `nid-ai-triaged` label for idempotency

### Prerequisites

- The `bug-triage` plugin from ai-helpers must be installed: `/plugin install bug-triage@ai-helpers`
- `jira` CLI must be installed and authenticated
- OCPBUGS project access (view, comment, edit labels)

### Team Docs

NID-specific documentation is in `plugins/nid/team-docs/`:

| File | Purpose |
|------|---------|
| `sub-areas.md` | NID sub-area taxonomy (Router/HAProxy, CIO, CoreDNS, ExternalDNS, Gateway API, Route Controller Manager) |
| `routing-guide.md` | Keywords for detecting bugs misrouted to NID (OVN/SDN, MetalLB, Service Mesh, etc.) |
| `context/` | Optional: FAQs, AGENTS.md copies, additional context docs |

## Return Value
- **Per-issue**: A structured triage comment posted directly on each Jira issue
- **Terminal**: Summary of all bugs analyzed with counts by category
- **Labels**: `nid-ai-triaged` added to each processed issue

## Examples

1. **Triage a single issue (demo/testing)**:
   ```
   /nid:bug-scrub --issue OCPBUGS-83283
   ```

2. **Dry run on a single issue** (preview comment without posting):
   ```
   /nid:bug-scrub --issue OCPBUGS-83283 --dry-run
   ```

3. **Triage all untriaged bugs from the last week**:
   ```
   /nid:bug-scrub --since last-week
   ```

4. **Triage all untriaged bugs from the last 2 weeks**:
   ```
   /nid:bug-scrub --since last-2-weeks
   ```

5. **Default run** (last week, no dry-run):
   ```
   /nid:bug-scrub
   ```

## Arguments

- **--issue** *(optional)*
  A specific OCPBUGS issue key to triage. When provided, skips the JQL query and operates on this single issue only. Useful for demos and testing.
  Example: `--issue OCPBUGS-83283`

- **--since** *(optional)*
  Time window for querying untriaged bugs.
  Options: `last-week` (default) | `last-2-weeks` | `last-month` | `YYYY-MM-DD`
  Example: `--since last-2-weeks`

- **--dry-run** *(optional)*
  Preview triage comments in the terminal without posting them to Jira or adding labels. Use this to review output before enabling live posting.

## See Also
- `plugins/nid/team-docs/` -- NID-specific team documentation for triage
- `/bug-triage:scrub` -- General bug triage command (ai-helpers)
- `/jira:grooming` -- Generic Jira grooming agenda generator
