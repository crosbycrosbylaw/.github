# Example: an issue with sub-issues

Rewritten from [nushell-mcp#8](https://github.com/zaynram/nushell-mcp/issues/8), which was filed as one issue. It is split here to show how the sections divide between a parent and its sub-issues: the parent states the outcome, and each sub-issue carries its own deliverables.

## The parent

| Outside the body | Value |
| --- | --- |
| Title | `windows-portability` |
| Type | chore |
| Milestone | `v0.3.0` |
| Parent | None |
| Evidence | Deliverable |

### Context

The test suite assumes a POSIX host. Under Windows Bun, tests fail for reasons unrelated to the code they cover: temp paths handed to nu in double quotes are read as escape sequences, `--include-path` fragments drive-letter paths, and one test spawns the `sleep` external, which Windows lacks.

### Deliverables

None of its own. Each sub-issue lists its deliverables.

### Actionables

None.

### Criteria

- [ ] `bun test` passes under Windows Bun (1.4.x, nu 0.114.x) run from the WSL share with `--cwd`
- [ ] No test is skipped or weakened to get there

### Excluded

- Changes to behavior on POSIX hosts

## One of its sub-issues

| Outside the body | Value |
| --- | --- |
| Title | `include-dirs-separator` |
| Type | patch |
| Milestone | None; a sub-issue takes its parent's |
| Parent | `windows-portability` |
| Evidence | Deliverable |

### Context

`includeDirs` reaches nu through the `--include-path` flag, which fragments drive-letter paths on Windows.

### Deliverables

- [ ] `src/env.ts` - `withIncludeDirs`: `includeDirs` prepended to `NU_LIB_DIRS` with the platform separator, replacing the flag
- [ ] `test/env.test.ts` - unit coverage: the platform separator, precedence over an existing `NU_LIB_DIRS`, and case-insensitive key reuse on Windows

### Actionables

None.

### Criteria

- [ ] The raw-vehicle `includeDirs` test passes from a UNC working directory
