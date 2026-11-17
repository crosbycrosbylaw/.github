# Example: A Work Item without Deliverables

This showcases an example of a work item that leaves no artifact, with both optional sections.

It was rewritten from an issue in a separate repository.

**Fields:**

```json
{
  "title": "issue-status-backfill",
  "type": "chore",
  "milestone": "v0.4.1",
  "parent": null,
  "evidence": "actionable"
}
```

**Body:**

```md
### Context

Closed issues #3 and #4 carry `status = 'completed'` while every task under them reads `completed = false`. The records no longer show what was done, so completion state does not survive past the session that produced it.

### Deliverables

None.

### Actionables

- [ ] Set every task and subtask under each closed issue to its true completion state
- [ ] Record the actual closure date on each completed task

### Criteria

- [ ] Every task and subtask under a closed issue reflects its true completion state
- [ ] Task completion carries a closure date, not a boolean

### Constraints

- Metadata correction only: no issue's definition or scope is altered

### Excluded

- Issues that are still open or were aborted
```
