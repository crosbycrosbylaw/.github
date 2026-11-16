# Issue examples

Filled examples of the issue templates in [`.github/ISSUE_TEMPLATE`](../.github/ISSUE_TEMPLATE). They are real issues from [nushell-mcp](https://github.com/zaynram/nushell-mcp) and [nu-fluency](https://github.com/zaynram/nu-fluency), rewritten into the templates' sections. Values set outside the body, such as milestones, are illustrative.

| Example | Template | Shows |
| --- | --- | --- |
| [work-item-deliverable.md](work-item-deliverable.md) | Work item | Work that ends in artifacts, with the optional Constraints section |
| [work-item-actionable.md](work-item-actionable.md) | Work item | Work that leaves no artifact, with both optional sections |
| [initiative-with-leaves.md](initiative-with-leaves.md) | Work item | An issue with sub-issues, and one of those sub-issues |
| [inquiry.md](inquiry.md) | Inquiry | A decision to make, with its answer recorded as a file |

## The body

- Every heading in the template stays in the body, in the template's order. A section with nothing to say reads `None.`
- `Constraints` and `Excluded` are optional and follow the required sections.
- A deliverable is one line: a path or URL, then what it is. A criterion is a statement that is true or false once the work is done.
- The template's HTML comments are removed before the issue is saved.
- An issue with no milestone and no parent is a candidate. It may be free-form until it is scheduled.

## Outside the body

The template does not carry these. Each example lists them in a table above its body.

| Value | Where it is set |
| --- | --- |
| Title | A kebab-case slug, such as `pathext-omission` |
| Type | The issue type: patch, bug, feature, chore, doc or inquiry |
| Milestone | A version of the repository, `vX.Y.Z`; sub-issues carry none |
| Parent | The parent issue, for a sub-issue |
| Evidence | The issue field: Deliverable when the work ends in artifacts, Actionable otherwise |

## Filing an issue without a browser

`gh issue create --template` works only at an interactive terminal. A script or an agent reads the template through the API, fills it in, and passes the result as a file:

```sh
# The templates that apply to a repository, organization defaults included
gh api graphql \
  -f query='query($o:String!,$r:String!){repository(owner:$o,name:$r){issueTemplates{name body}}}' \
  -f o=OWNER -f r=REPO

# After filling the sections and removing the comments
gh issue create -R OWNER/REPO --title "kebab-case-slug" --body-file body.md --type patch --milestone v0.2.5
```

A sub-issue takes `--parent NUMBER` in place of `--milestone`.
