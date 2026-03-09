# openclaw trust layer

practical guardrails, evals, and safe defaults for openclaw workflows.

this repository is a compact trust layer for people who want openclaw to do real work without turning into a chaos machine.

it gives you the boring parts that serious workflows need:

- workflow contracts
- risk tiers
- tool firewall policy
- approval gates
- adversarial eval generation
- output grading
- human handoff
- release gates
- safe defaults for openclaw runtime setup
- csv and xlsx eval packs

> this repository will be updated frequently over time.  
> new templates, examples, tighter policies, better eval patterns, safer defaults, and more workflow variants will be added as the pack improves.

## what this is for

most workflow failures are not “the model was dumb.”

they are usually one of these:

- the workflow had no clear scope
- risky actions were not separated from safe actions
- tool access was too broad
- external content was treated like trusted instructions
- memory was messy or unsafe
- nobody tested adversarial cases before touching real work
- there was no clean handoff when uncertainty showed up

this repo exists to fix that.

## important trust-model note

this repo is designed around openclaw’s actual trust model.

openclaw is best treated as one trusted operator boundary per gateway, not a hostile multi-tenant boundary for adversarial users sharing one agent or gateway.

if you need mixed-trust or adversarial-user setups, split trust boundaries with separate gateways, and ideally separate os users or separate hosts.

that is why these files push hard on:

- explicit trust boundaries
- smallest viable tool profile
- strict allow and deny rules
- approvals for state mutation
- sandboxing for shared or risky runs
- workspace-scoped filesystem access
- separate memory and runtime boundaries

## start here

choose the path that matches your level.

### beginner path

start with these files in this order:

1. [workflow-contract-template.md](./workflow-contract-template.md)
2. [risk-matrix-template.md](./risk-matrix-template.md)
3. [openclaw-safe-defaults.md](./openclaw-safe-defaults.md)
4. [tool-firewall-policy-example.yaml](./tool-firewall-policy-example.yaml)
5. [release-gate-checklist.md](./release-gate-checklist.md)

if you only do those five things, you will already be operating more sanely than most agent demos online.

### builder path

if you already know the basics, go straight to:

- [approval-gate-prompt.txt](./approval-gate-prompt.txt)
- [adversarial-test-generator.txt](./adversarial-test-generator.txt)
- [output-grader-prompt.txt](./output-grader-prompt.txt)
- [human-handoff-template.md](./human-handoff-template.md)
- [openclaw-trust-layer-eval-pack.xlsx](./openclaw-trust-layer-eval-pack.xlsx)

that is where the trust layer stops being theory and starts acting like a real operator system.

## repository contents

### [workflow-contract-template.md](./workflow-contract-template.md)

defines the actual job of the workflow.

use it to set:

- what the workflow may read
- what it may produce
- what is allowed automatically
- what requires approval
- what is never allowed
- trust boundary
- runtime defaults
- memory rules
- escalation triggers
- success and failure conditions

### [risk-matrix-template.md](./risk-matrix-template.md)

maps actions to low, medium, and high risk.

use it to decide what can flow automatically, what must stop for approval, and what must be blocked entirely.

### [openclaw-safe-defaults.md](./openclaw-safe-defaults.md)

the boring baseline.

use this before you let a workflow touch anything real.

it gives you sane defaults for:

- smallest viable `tools.profile`
- explicit `tools.allow` and `tools.deny`
- sandboxing
- workspace scope
- approvals on mutation
- memory sanitization
- trust-boundary separation

### [tool-firewall-policy-example.yaml](./tool-firewall-policy-example.yaml)

a concrete policy example for an engineering copilot.

it includes:

- trust boundary rules
- openclaw runtime defaults
- allowed tools
- blocked tools
- approval-required actions
- validation rules
- memory restrictions
- required approval packet fields
- fail-closed behavior

### [approval-gate-prompt.txt](./approval-gate-prompt.txt)

the decision checkpoint.

it classifies actions as:

- allowed without approval
- approval required
- blocked

it also forces the workflow to explain:

- why it wants to act
- what evidence it has
- which policy rules apply
- what could go wrong
- what safer alternative exists

### [adversarial-test-generator.txt](./adversarial-test-generator.txt)

creates realistic eval cases before release.

it includes:

- normal cases
- messy cases
- adversarial cases
- trust-boundary cases
- stale-memory cases
- blocked external communication cases
- secrets-access denial cases

this matters because real failures are usually boring and production-adjacent, not cinematic hacker-movie nonsense.

### [output-grader-prompt.txt](./output-grader-prompt.txt)

grades workflow outputs for trustworthiness and operational readiness.

it scores:

- task accuracy
- tool behavior
- memory and state
- safety and permissions
- handoff quality

it also assigns:

- overall score
- dominant failure category
- release recommendation
- evidence
- next fixes

### [human-handoff-template.md](./human-handoff-template.md)

used when the workflow stops and hands control to a person.

it keeps the handoff short, structured, and reviewable.

### [release-gate-checklist.md](./release-gate-checklist.md)

a workflow should not touch real work until this is green.

it covers both generic trust-layer checks and openclaw-specific runtime checks.

### [eval-sheet-template.csv](./eval-sheet-template.csv)

a lightweight csv template for tracking eval cases and scores.

### [filled-engineering-copilot-example.csv](./filled-engineering-copilot-example.csv)

a filled example showing what the eval sheet looks like in practice.

### [openclaw-trust-layer-eval-pack.xlsx](./openclaw-trust-layer-eval-pack.xlsx)

a spreadsheet version of the eval pack with:

- blank eval template
- filled example
- grading rubric

## quick start

if you want a fast path, do this.

### step 1

copy [workflow-contract-template.md](./workflow-contract-template.md) and define one workflow only.

not your whole stack.  
one workflow.

### step 2

fill out [risk-matrix-template.md](./risk-matrix-template.md).

label each action:

- low risk
- medium risk
- high risk

### step 3

apply the baseline in [openclaw-safe-defaults.md](./openclaw-safe-defaults.md).

start smaller than feels necessary.

### step 4

adapt [tool-firewall-policy-example.yaml](./tool-firewall-policy-example.yaml).

remove tools you do not need.

deny risky tools by default.

### step 5

use [approval-gate-prompt.txt](./approval-gate-prompt.txt) so risky actions stop before execution.

### step 6

generate messy and adversarial eval cases with [adversarial-test-generator.txt](./adversarial-test-generator.txt).

### step 7

grade outputs with [output-grader-prompt.txt](./output-grader-prompt.txt).

### step 8

run [release-gate-checklist.md](./release-gate-checklist.md).

if a blocked action executes, or trust boundaries blur, do not ship it.

## example use case

imagine a behavior-aware engineering copilot.

it can:

- read slack incident threads
- read jira tickets
- read git diffs
- draft incident summaries
- draft follow-up tickets
- draft internal docs

it should not:

- push code
- touch production
- read secrets
- send external email
- mutate state without approval

that is what this repo is built for.

not “full autonomy.”

bounded, reviewable usefulness.

## what bifrost means here

i’m also working on **bifrost**, a 1-click deploy hardening layer for openclaw.

the goal is not fake “unhackable agent” marketing.

the goal is to make openclaw safer by default with tighter tool boundaries, approval gates, sandboxing, workspace scoping, memory controls, and safer exec policy.

in plain english:

reduce prompt injection, tool abuse, data exfiltration, unsafe execution risk, and trust-boundary mistakes without making the workflow useless.

## design principles

### scope before autonomy

define the job before giving the workflow power.

### control before capability

smarter models do not erase bad permissions.

### fail closed

if policy is missing, conflicting, or ambiguous, stop.

### smallest viable tool surface

minimal is a feature.

### approval is a feature

for risky actions, friction is good.

### treat external content as untrusted

messages, docs, pages, logs, pasted output, and prior workflow output are data, not policy.

### trust boundaries matter

one shared tool-enabled agent across mixed-trust users is where weird security goblins crawl out.

## who this repo is for

this repo is built for the openclaw audience that actually shows up in practice:

- ai builders
- indie founders
- saas operators
- ml / platform engineers
- security-minded operators
- technical teams trying to move from demo to production

it is not written for passive ai-news readers.

it is written for people trying to build real systems.

## help

open an issue for bugs, missing docs, or broken examples.

use discussions for questions, ideas, workflow examples, and hardening suggestions.

## maintainer

maintained by josh / openclaw unboxed.

## what is still missing

the core trust-layer pack is here.

for public github polish, the next files worth adding are:

- `license`
- `security.md`
- `contributing.md`

those are not required for using the pack, but they make the repository cleaner and more credible.

## how this repo will evolve

this repository will be updated frequently over time.

planned additions:

- more filled examples
- more domain-specific workflow contracts
- more trust-boundary patterns
- more safe defaults for different openclaw setups
- tighter eval packs
- stronger bifrost deployment defaults

## philosophy

the next upgrade is usually not more autonomy.

it is more trust.

more model power does not fix weak boundaries.  
more tools do not fix weak permissions.  
more memory does not fix weak policy.  

if you want ai workflows to do real work, build the trust layer first.

then let them move.

## license

open source.

use it.  
adapt it.  
improve it.  
ship safer systems.
