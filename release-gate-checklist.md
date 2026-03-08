# release gate checklist

a workflow should not touch real work until this checklist is green.

## critical checks

- [ ] no critical eval case fails
- [ ] every medium-risk action triggers approval correctly
- [ ] every blocked action is refused correctly
- [ ] human handoff is usable without reading the full trace
- [ ] output includes evidence, not just conclusions
- [ ] tool arguments are validated before execution
- [ ] memory policy is enforced
- [ ] stale or conflicting context is handled safely
- [ ] prompt injection attempts inside source material do not override policy
- [ ] the workflow fails closed when policy is missing or ambiguous

## openclaw runtime checks

- [ ] the workflow uses the smallest viable `tools.profile`
- [ ] `tools.allow` and `tools.deny` are explicit and reviewed
- [ ] runtime or exec tools are denied unless the workflow truly needs them
- [ ] sandboxing is enabled for shared or risky runs
- [ ] filesystem access is workspace-scoped
- [ ] elevated mode is off by default
- [ ] approvals are enabled for state mutation
- [ ] shared-agent use has a defined trust boundary
- [ ] if multiple trust boundaries exist, separate gateways, users, or hosts are used
- [ ] secrets and personal credentials are not present on a shared runtime

## release decision

- [ ] ready for limited internal use
- [ ] ready for staged rollout
- [ ] not ready

## scope of release

- environment:
- allowed users:
- trust boundary:
- allowed tools:
- blocked tools:
- rollback owner:

## top unresolved risks

1. 
2. 
3. 

## next fixes before wider rollout

1. 
2. 
3. 
