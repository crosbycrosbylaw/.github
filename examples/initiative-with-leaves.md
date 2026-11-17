# Example: An Initiative with Leaves

This showcases an example of a parent issue with sub-issues.

It was rewritten from a separate repository's work that contained several deliverables and was filed as a single issue.
It is split here to show how the sections divide between a parent and its sub-issues: the parent states the outcome, and each sub-issue carries its own deliverables.

## Parent

**Fields:**

```json
{
  "title": "windows-portability",
  "type": "chore",
  "milestone": "v0.3.0",
  "parent": null,
  "evidence": "deliverable"
}
```

**Body:**

```md
### Context

The test suite assumes a POSIX host. Under Windows Bun, tests fail for reasons unrelated to the code they cover: temp paths handed to nu in double quotes are read as escape sequences, `--include-path` fragments drive-letter paths, and one test spawns the `sleep` external, which Windows lacks.

### Deliverables

None of its own. Each sub-issue lists its deliverables.

### Actionables

- [ ] Close each attached sub-issue
- [ ] Verify the contents of all deliverables are acceptable

Any issues identified with the deliverables after their issues are closed are opened as separate sub-issues.

### Criteria

- [ ] `bun test` passes under Windows Bun (1.4.x, nu 0.114.x) run from the WSL share with `--cwd`
- [ ] No test is skipped or weakened to get there

### Excluded

- Changes to behavior on POSIX hosts
```

## Sub-issue

**Fields:**

```json
{
  "title": "include-dirs-separator",
  "type": "patch",
  "milestone": null,
  "parent": "windows-portability",
  "evidence": "deliverable"
}
```

**Body:**

```md
### Context

`includeDirs` reaches nu through the `--include-path` flag, which fragments drive-letter paths on Windows.

### Deliverables

- [ ] `src/env.ts` - `withIncludeDirs`: `includeDirs` prepended to `NU_LIB_DIRS` with the platform separator, replacing the flag
- [ ] `test/env.test.ts` - unit coverage: the platform separator, precedence over an existing `NU_LIB_DIRS`, and case-insensitive key reuse on Windows

### Actionables

None.

### Criteria

- [ ] The raw-vehicle `includeDirs` test passes from a UNC working directory
```
