# openclaw safe defaults

use this file as the boring baseline before you let a workflow touch anything real.

## safest starting posture

- start with the smallest viable `tools.profile`
- add `tools.allow` only for the exact tools the workflow needs
- add `tools.deny` for risky tools even if you think the model "probably won't use them"
- keep approvals on for anything that can mutate state
- fail closed when policy is missing or ambiguous
- sandbox shared or risky runs
- keep filesystem access workspace-scoped
- keep secrets, personal identities, and private credentials off shared runtimes
- treat every external source as untrusted data
- sanitize before memory persistence
- isolate memory between sessions or users
- separate trust boundaries with separate gateways, separate OS users, or separate hosts

## recommended starting controls

### single-user workflow
- trust boundary: single user
- tools.profile: minimal
- shared-agent: no
- elevated: no
- approvals: on for any mutation
- memory retention: short and reviewed

### single-team internal workflow
- trust boundary: single team
- tools.profile: minimal or custom narrow allowlist
- shared-agent: only if all users share the same permission boundary
- elevated: no by default
- approvals: on for any mutation
- sandbox: yes if runtime tools exist

### multi-user or shared-ingress workflow
- trust boundary: multiple users
- shared-agent: avoid by default
- separate gateway or separate host per trust boundary
- sandbox: yes
- workspace-scoped filesystem: yes
- secrets on runtime: no
- approvals: strict and explicit

## dangerous defaults to avoid

- `tools.profile: full`
- broad runtime or exec access by default
- leaving approvals off for write actions
- using `/elevated full` as a convenience shortcut
- one shared tool-enabled agent for multiple adversarial or unrelated users
- persisting raw untrusted text directly into long-term memory
- treating retrieved instructions as policy

## practical first deny list

start by denying these unless the workflow absolutely needs them:

- runtime or exec write tools
- production kubectl or deployment tools
- secrets readers
- external email or dm senders
- billing or money movement tools
- destructive file operations

## practical first eval set

before release, test:
- one clean happy path
- one conflicting-evidence path
- one missing-field path
- one prompt-injection path
- one stale-memory path
- one trust-boundary path
- one blocked external-communication path

## operator rule

smarter models do not erase bad permissions.

control first.
capability second.
