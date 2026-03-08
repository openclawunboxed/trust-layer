# openclaw trust layer

practical guardrails for agent workflows.

this repository contains a minimal trust layer for ai workflows so they can safely move from demo to real work.

most agent systems fail not because the model is weak, but because the control system around the model is missing.

this repo provides that control layer.

> this repository will be updated frequently over time.  
> new templates, examples, tighter policies, better eval patterns, and more workflow variants will be added as the pack improves.

---

## who this is for

this repo is built for people trying to make ai do real work.

that includes:

- ai builders
- indie founders
- saas operators
- engineers
- technical teams
- automation-minded business operators

if you are trying to automate workflows, add guardrails, reduce fragility, or make agent systems safe enough to keep around, this repo is for you.

---

## start here

choose the path that matches your current level.

### if you are a complete beginner

start with these 4 files in order:

1. `workflow-contract-template.md`
2. `risk-matrix-template.md`
3. `tool-firewall-policy-example.yaml`
4. `release-gate-checklist.md`

that is enough to understand the basic trust layer.

### if you are intermediate or advanced

jump straight to:

- `approval-gate-prompt.txt`
- `adversarial-test-generator.txt`
- `output-grader-prompt.txt`
- `human-handoff-template.md`

those files are where the workflow gets pressure-tested and made production-safer.

---

## what this repository is

a set of small building blocks that let an ai workflow:

- know what it is allowed to do
- know when it must ask for approval
- refuse dangerous actions
- escalate to humans
- test itself before touching real work
- avoid pretending confidence when evidence is weak

these pieces form a simple architecture:

workflow contract  
↓  
risk matrix  
↓  
tool firewall  
↓  
approval gate  
↓  
eval system  
↓  
human handoff  
↓  
release gate  

if these layers exist, workflows become far more useful and far less chaotic.

---

## what problem this solves

most ai agents fail for boring reasons:

- unclear permissions
- unsafe tool execution
- weak memory discipline
- no approval gates
- no evaluation
- no clean handoff to humans
- no release process
- too much autonomy too early

this repo fixes those gaps.

---

## repository contents

### 1. workflow contract

file: `workflow-contract-template.md`

this is the job description for the workflow.

it defines:

- what the workflow is
- what it reads
- what it produces
- what actions are allowed
- what requires approval
- what is never allowed
- what memory is permitted
- when escalation must happen

use this first.

if the workflow contract is vague, everything downstream gets worse.

---

### 2. risk matrix

file: `risk-matrix-template.md`

this maps action types to risk levels.

example:

- read data → low risk
- draft internal artifact → medium risk
- modify production → high risk and often blocked

the point is simple.

not every action deserves the same level of trust.

---

### 3. tool firewall

file: `tool-firewall-policy-example.yaml`

this is the hard policy layer.

it defines:

- allowed tools
- blocked tools
- which actions require approval
- validation rules
- memory boundaries
- fail-closed behavior

this is where a lot of real safety comes from.

not vibes.  
not “the model should know better.”  
actual boundaries.

---

### 4. approval gate

file: `approval-gate-prompt.txt`

this is the decision checkpoint.

it decides whether an action is:

- allowed
- approval required
- blocked

it should never execute the action itself.

it should return a decision packet a human can scan quickly.

this is how you stop “trust me bro” automation from touching real systems.

---

### 5. adversarial test generator

file: `adversarial-test-generator.txt`

this generates test cases for the workflow.

it includes:

- normal cases
- messy cases
- adversarial cases

the goal is not to make the system look smart.

the goal is to find where it breaks before reality finds out first.

---

### 6. output grader

file: `output-grader-prompt.txt`

this grades workflow outputs.

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
- next fixes

this is useful because polished nonsense should not pass just because it sounds confident.

---

### 7. human handoff

file: `human-handoff-template.md`

this is used when the workflow must stop and pass control to a person.

it explains:

- what happened
- what was already checked
- what is still uncertain
- what decision is needed
- what should happen next

good handoff is part of the product.

bad handoff turns automation into extra work.

---

### 8. release gate

file: `release-gate-checklist.md`

this is the final sanity check.

before a workflow touches real work, it should pass checks like:

- no critical eval case fails
- blocked actions are refused correctly
- approval triggers work correctly
- handoff is readable
- stale context is handled safely
- policy ambiguity fails closed

if those are not true, do not ship it yet.

---

## quick start

if you want to get value from this repo fast, do this.

### beginner quick start

step 1  
copy `workflow-contract-template.md`

fill in:

- allowed actions
- approval-required actions
- never-allowed actions

step 2  
copy `risk-matrix-template.md`

label your workflow actions as:

- low
- medium
- high

step 3  
adapt `tool-firewall-policy-example.yaml`

remove tools you do not need.  
block anything risky by default.

step 4  
run your workflow through the `release-gate-checklist.md`

if it fails the checklist, do not deploy.

that alone will put you ahead of most agent demos.

---

## first real implementation example

imagine an engineering copilot.

it reads:

- slack threads
- jira tickets
- git diffs

it produces:

- incident summaries
- draft jira tickets
- internal docs

it may be allowed to:

- read sources
- summarize incidents
- draft internal artifacts

it may require approval to:

- create a jira ticket
- create a draft doc
- post to a shared team channel

it may never be allowed to:

- push code
- touch production
- read secrets
- send external email

that is the trust layer in practice.

---

## how beginners should use this repo

do not try to wire up every file at once.

do this instead.

phase 1  
define scope

- fill out the workflow contract
- fill out the risk matrix

phase 2  
define enforcement

- adapt the tool firewall
- add the approval gate

phase 3  
define testing

- generate messy and adversarial eval cases
- grade the outputs

phase 4  
define release

- use the handoff template
- use the release checklist

small and boring beats complex and fragile.

---

## how advanced users should use this repo

this repo is intentionally minimal.

it is meant to be extended.

common extensions:

multi-agent systems

use one trust layer across multiple agents:

- planner
- researcher
- writer
- executor

the trick is not more agents.

the trick is shared policy and clean boundaries.

ci-based eval pipelines

you can wire the eval flow into a build pipeline:

1. generate eval cases  
2. run workflow  
3. grade outputs  
4. fail the pipeline below threshold  

domain-specific variants

the same trust layer can be reused for:

- engineering ops
- brokerage ops
- finance-sensitive workflows
- ecommerce workflows
- healthcare admin workflows
- internal copilots

different workflows.  
same control logic.

---

## design principles

this repository follows a few simple rules.

scope before autonomy  
define the job before giving the workflow power.

fail closed  
if policy is missing or ambiguous, stop.

risky actions need friction  
approval is a feature, not a bug.

evals matter more than confidence  
a workflow that sounds smart and breaks policy is still broken.

handoff quality matters  
if humans cannot quickly understand what happened, the workflow is not production-ready.

boring failures are the real failures

missing fields  
stale context  
bad tool arguments  
weak state handling  
sloppy permissions  

that is where real systems usually break.

---

## what success looks like

a good workflow using this repo should:

- stay inside its role
- avoid unauthorized tools
- escalate uncertainty
- request approval for risky actions
- resist prompt injection inside source material
- produce reviewable outputs
- hand off cleanly to humans
- pass its release gate before touching real work

---

## what this repo is not

this is not:

- a generic ai tutorial
- a one-click agent framework
- a promise of full autonomy
- a shortcut around evaluation
- a replacement for engineering judgment

it is a practical control layer.

---

## recommended file order

if you want the cleanest reading order:

1. `workflow-contract-template.md`  
2. `risk-matrix-template.md`  
3. `tool-firewall-policy-example.yaml`  
4. `approval-gate-prompt.txt`  
5. `adversarial-test-generator.txt`  
6. `output-grader-prompt.txt`  
7. `human-handoff-template.md`  
8. `release-gate-checklist.md`  

---

## how this repo will evolve

this repository will be updated frequently.

planned additions include:

- more filled examples
- more domain-specific workflow contracts
- better adversarial test packs
- tighter policy patterns
- versioned eval recipes
- more beginner-safe walkthroughs
- more advanced production patterns

the goal is simple.

make this repo more useful over time for both beginners and serious operators.

---

## philosophy

the next upgrade is usually not more autonomy.

it is more trust.

more model power does not fix weak boundaries.  
more tools do not fix weak permissions.  
more memory does not fix weak policy.  

if you want ai workflows to do real work, build the trust layer first.

then let them move.

---

## license

open source.

use it.  
adapt it.  
improve it.  
ship safer systems.
