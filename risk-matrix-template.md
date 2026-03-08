# risk matrix template

| action type | example | risk tier | allowed automatically | approval required | never allowed |
|---|---|---:|---:|---:|---:|
| read thread | slack.read_thread | low | yes | no | no |
| classify request | categorize issue | low | yes | no | no |
| draft summary | draft incident summary | low | yes | no | no |
| create internal artifact | create jira ticket draft | medium | no | yes | no |
| write to staging | create staging config patch | medium | no | yes | no |
| post internal message | post in shared channel | medium | no | yes | no |
| draft production change request | prepare production change plan for review | high | no | yes | no |
| draft customer-facing update | prepare customer incident update for review | high | no | yes | no |
| touch production directly | kubectl apply to prod | high | no | no | yes |
| irreversible action | delete records or rotate secrets | high | no | no | yes |

## notes

- low risk means read, summarize, classify, or draft
- medium risk means create, post, or write to non-production systems
- high risk means anything involving production, customer impact, money, secrets, or irreversible actions
- high risk does not always mean allowed with approval. some workflows should block entire classes of actions completely

## custom matrix

copy this table and adapt it to your workflow.

| action type | example | risk tier | allowed automatically | approval required | never allowed |
|---|---|---:|---:|---:|---:|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
