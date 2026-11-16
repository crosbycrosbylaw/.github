# Example: a work item that ends in artifacts

Rewritten from [nushell-mcp#2](https://github.com/zaynram/nushell-mcp/issues/2).

| Outside the body | Value |
| --- | --- |
| Title | `pathext-omission` |
| Type | bug |
| Milestone | `v0.2.5` |
| Parent | None |
| Evidence | Deliverable |

## Body

### Context

On Windows, the nu children this server spawns cannot resolve external commands by bare name: `^where` fails while `^where.exe` succeeds. The MCP TypeScript SDK launches stdio servers with a fixed environment whitelist that omits `PATHEXT`, `COMSPEC` and `TMP`, and every spawn site here passes the inherited environment through unchanged.

Reproduced on 2026-09-04 with nu 0.114.2-nightly.2 and bun 1.4.1: under the SDK's whitelist, `which nu` is empty, and adding `PATHEXT` alone restores resolution.

### Deliverables

- [ ] `src/env.ts` - an environment builder that backfills the Windows-essential variables with Windows defaults when the host omits them, used at every nu spawn site
- [ ] `test/env.test.ts` - regression coverage for the builder
- [ ] `https://www.npmjs.com/package/nushell-mcp/v/0.2.5` - the published patch release

### Actionables

None.

### Criteria

- [ ] Bare-name external commands resolve in Nushell executions on Windows without the caller supplying environment overrides
- [ ] `PATHEXT`, `COMSPEC` and `TMP` are present in every nu child on Windows: the one-shot default, env-layered and `cleanEnv` paths, and the long-lived `nu --mcp` children
- [ ] Regression tests assert the presence of the essential variables per platform, and bare-name resolution of a known binary
- [ ] The release notes document the resolution semantics

### Constraints

- `cleanEnv` leaks nothing from the host beyond the explicit allowlist
- Behavior on POSIX hosts is unchanged; the allowlist applies on Windows only
- Each variable takes the host's value when present and a Windows default otherwise, matched case-insensitively
