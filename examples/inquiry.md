# Example: An Inquiry

This showcases an example of a decision to make, with its answer recorded as a file.

It was rewritten from an issue in a separate repository.

**Fields:**

```json
{
  "title": "hooks-placement",
  "type": "inquiry",
  "milestone": "v0.4.0",
  "parent": null,
  "evidence": "deliverable"
}
```

**Body:**

```md
### Question

Do the plugin's hooks live in a plugin-level `hooks.json`, or in skill-scoped frontmatter?

### Context

No hooks are shipped yet, so placement is undecided. The answer gates `nu-over-bash-hooks`: no hook is implemented before placement is settled, because changing it later means rework across every hook the plugin ships.

### Criteria

- [ ] A definite stance, with its rationale
- [ ] Recorded under `docs/decisions/`, where future contributors will find it

### Excluded

- Hook implementation, which belongs to `nu-over-bash-hooks`
```
