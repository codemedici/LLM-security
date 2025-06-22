# Agent Behavior Trees and Failure Analysis

## Common Vulnerabilities

* **Unvalidated Fallback Branches**\
  Some agents use default branches for unknown responses, e.g., “try again with less context” — this may reintroduce rejected prompts.
* **Overlapping Roles**\
  If leaf nodes execute critical actions but skip role authentication, users can reach privileged behavior paths by indirect navigation.
* **Looping without Exit**\
  Behavior trees that fail to limit retry loops or planner-executor calls can be DOS’d or tricked into undesired tasks.

## Real-World Mapping (LangChain/CrewAI)

```yaml
root:
  - plan_task
    - if_success: execute_tool
    - if_fail: replan
```

If `replan` retries include old memory state, and `plan_task` uses insecure summarization, users can craft a poisoned goal that survives multiple tree traversals.

## Testing Recommendations

* **Branch-specific guards**: Add authentication or content validation checks at _every_ conditional branch.
* **Retry counter hooks**: Log and limit fallback loops per session.
* **Tree visualizers**: Render trees to detect hidden escalation paths.

## Defensive Engineering Patterns

* Use precompiled trees with frozen node types
* Avoid dynamic policy routing between roles
* Include tree integrity signatures in orchestrators
