# workflow contract template

use this to define the actual job of the workflow.

not the dream.
not the future roadmap.
the actual job.

## workflow identity

- workflow name:
- owner:
- date:
- version:
- environment: local / cloud / hybrid
- primary goal:

## one-sentence job description

describe the workflow in one sentence.

example:
draft internal incident summaries and follow-up tickets from engineering signals without taking direct production actions.

## inputs

list the sources the workflow can read.

- source 1:
- source 2:
- source 3:

## outputs

list the things the workflow can produce.

- output 1:
- output 2:
- output 3:

## allowed

actions the workflow can do without approval.

- 
- 
- 

## approval required

actions the workflow may propose but cannot execute without explicit approval.

- 
- 
- 

## never allowed

actions the workflow may not take under any condition.

- 
- 
- 

## tool scope

list the exact tools or integrations this workflow may access.

- 
- 
- 

## tool constraints

write hard constraints for each allowed tool.

example:
- jira.create_ticket may only create draft tickets in the infra project
- terminal.read_only may not write files or modify environment variables

- 
- 
- 

## memory policy

what may be remembered, for how long, and where.

- allowed memory:
- blocked memory:
- retention window:
- storage location:
- deletion rule:

## escalation triggers

when must the workflow stop and hand off to a human?

- ambiguous ownership
- conflicting source evidence
- missing required fields
- medium-risk action requested
- any high-risk condition

add your own:
- 
- 
- 

## success criteria

how will you judge whether this workflow is working?

- 
- 
- 

## failure conditions

what counts as failure?

- 
- 
- 

## notes

add anything special about the workflow here.
