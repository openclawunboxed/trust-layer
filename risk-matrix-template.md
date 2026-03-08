# risk matrix template

use this to decide what can flow automatically, what must stop for approval, and what must be blocked entirely.

| action type | example | risk tier | allowed automatically | approval required | never allowed |
|---|---|---:|---:|---:|---:|
| read thread | slack.read_thread | low | yes | no | no |
| classify request | categorize issue | low | yes | no | no |
| draft summary | draft incident summary | low | yes | no | no |
| draft internal artifact | create jira ticket draft | medium | no | yes | no |
| write to staging | create staging config patch | medium | no | yes | no |
| post internal message | post in shared channel | medium | no | yes | no |
| draft production change request | prepare production change plan for review | high | no | yes | no |
| draft customer-facing update | prepare customer incident update for review | high | no | yes | no |
| touch production directly | kubectl apply to prod | high | no | no | yes |
| access secrets | read secret store | high | no | no | yes |
| irreversible action | delete records or rotate secrets | high | no | no | yes |
| external communication | send customer email or dm | high | no | workflow-specific | workflow-specific |

## notes

- low risk means read, summarize, classify, or draft without mutating state
- medium risk means creating internal artifacts or writing to non-production systems
- high risk means production, customer impact, money, secrets, sensitive data, external messaging, or irreversible actions
- high risk does not always mean allowed with approval. some workflows should block entire classes of actions completely
- external communication should default to blocked unless the workflow contract explicitly allows a reviewed approval path

## openclaw mapping

pair each row with the runtime control that enforces it.

| risk tier | minimum control |
|---|---|
| low | smallest possible tool profile |
| medium | explicit approval gate + validated tool arguments |
| high | explicit approval or hard block + deny list + sandbox/workspace scope |

## custom matrix

copy this table and adapt it to your workflow.

| action type | example | risk tier | allowed automatically | approval required | never allowed |
|---|---|---:|---:|---:|---:|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
