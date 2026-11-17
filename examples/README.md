# Examples

Filled examples of the issue templates in [`.github/ISSUE_TEMPLATE`](../.github/ISSUE_TEMPLATE) and of the [pull request template](../.github/pull_request_template.md). Each was rewritten from work in a separate repository. Values such as milestones are illustrative.

| Example | Template | Shows |
| --- | --- | --- |
| [work-item-deliverable.md](work-item-deliverable.md) | Work item | Work that ends in artifacts, with the optional Constraints section |
| [work-item-actionable.md](work-item-actionable.md) | Work item | Work that leaves no artifact, with both optional sections |
| [initiative-with-leaves.md](initiative-with-leaves.md) | Work item | A parent issue and one of its sub-issues |
| [inquiry.md](inquiry.md) | Inquiry | A decision to make, with its answer recorded as a file |
| [pull-request.md](pull-request.md) | Pull request | A pull request that leaves its issue open |

## How an example reads

Each example has two parts. **Fields** is a JSON block of the values set outside the body. **Body** is a markdown block holding the body exactly as it is saved, so everything inside that block is example content and everything outside it belongs to the example file.

## The body of an issue

- Every heading in the template stays in the body, in the template's order. A section with nothing to say reads `None.`
- `Constraints` and `Excluded` are optional and follow the required sections.
- A deliverable is one line: a path or URL, then what it is. A criterion is a statement that is true or false once the work is done.
- A parent issue has no deliverables of its own. Its actionables are to close each sub-issue and to verify their deliverables.
- The template's HTML comments are removed before the issue is saved.
- An issue with no milestone and no parent is a candidate. It may be free-form until it is scheduled.

## The fields of an issue

The template does not carry these. The keys below are the ones the examples use; they name where a value is set and are not an API payload.

| Key | Value |
| --- | --- |
| `title` | A kebab-case slug, such as `pathext-omission` |
| `type` | The issue type: `patch`, `bug`, `feature`, `chore`, `doc` or `inquiry` |
| `milestone` | A version of the repository, `vX.Y.Z`; `null` on a sub-issue |
| `parent` | The parent issue's title, or `null` |
| `evidence` | The issue field: `deliverable` when the work ends in artifacts, `actionable` otherwise |

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
