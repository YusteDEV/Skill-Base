# Skills

opencode skill collection

## security-audit

### Contents

- **`security-audit`** — final security audit gate. It is invoked at the end of a feature or an important change, before closing it.

  - **Static**, stack-agnostic review (base: OWASP ASVS/Top 10 + CCN-STIC-140 Annex F.1).
  - Walks the code in scope through areas A-M (authentication, authorization, injection, XSS, CSRF, TLS, cryptography, sensitive data, logging, configuration, dependencies, integrity, error handling).
  - Produces a markdown report with findings grouped by severity (Critical, High, Medium, Low) and a verdict: `APPROVED`, `WITH OBSERVATIONS` or `REJECTED`.
  - **Does not modify code**: it only reports findings and proposes remediations.

### How to use it

The skill accepts an optional argument:

- Directory path: audit only that tree.
- File path: audit only that file.
- No argument: audit the whole repository (or the whole project if there is no git).

Invocation examples (from the opencode session):

- `security-audit` — audits the whole repository.
- `security-audit <path/subtree>` — only that subtree, e.g. a `src/` folder.
- `security-audit <path/file>` — only that file, e.g. a `package.json` manifest.

Always inside the workspace: paths that escape (`..`, external absolute paths, symlinks) are rejected.

Output example (verdict):

```
## Verdict
- REJECTED: there is at least one Critical or High finding.
- WITH OBSERVATIONS: no Critical or High, but there is at least one Medium or Low.
- APPROVED: there are no findings at any severity.
```