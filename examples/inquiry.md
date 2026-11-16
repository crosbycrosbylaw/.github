# Example: an inquiry

Rewritten from [nu-fluency#5](https://github.com/zaynram/nu-fluency/issues/5).

| Outside the body | Value |
| --- | --- |
| Title | `hooks-placement` |
| Type | inquiry |
| Milestone | `v0.4.0` |
| Parent | None |
| Evidence | Deliverable |

## Body

### Question

Do the plugin's hooks live in a plugin-level `hooks.json`, or in skill-scoped frontmatter?

### Context

No hooks are shipped yet, so placement is undecided. The answer gates `nu-over-bash-hooks`: no hook is implemented before placement is settled, because changing it later means rework across every hook the plugin ships.

### Criteria

- [ ] A definite stance, with its rationale
- [ ] Recorded under `docs/decisions/`, where future contributors will find it

### Excluded

- Hook implementation, which belongs to `nu-over-bash-hooks`
