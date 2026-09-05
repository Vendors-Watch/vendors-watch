# Default branch protection

The `main` branch must require pull requests and at least one approving review
before changes can merge. Reviews from code owners are required.

This makes the ownership rules in [CODEOWNERS](./CODEOWNERS) enforceable:

- `.github/dependabot.yml` requires approval from
  `@Vendors-Watch/vendor-watch-maintainers`.
- `.github/workflows/*` requires approval from
  `@Vendors-Watch/vendor-watch-maintainers`.

## Required GitHub settings

In **Settings → Branches → Branch protection rules → `main`**, keep these
settings enabled:

- **Require a pull request before merging**
- **Require approvals**: `1`
- **Dismiss stale pull request approvals when new commits are pushed**
- **Require review from Code Owners**
- **Require conversation resolution before merging**
- **Do not allow bypassing the above settings** (administrators included)

Force pushes and branch deletion must remain disabled.

## Verify after changing the rule

1. Open the `main` branch protection rule and confirm **Require review from Code
   Owners** is selected with one required approval.
2. Open a test pull request that changes either `.github/dependabot.yml` or a
   file under `.github/workflows/`.
3. Confirm GitHub requests `@Vendors-Watch/vendor-watch-maintainers` and blocks
   merging until an eligible code owner approves.
4. Push another commit after approval and confirm the stale approval is
   dismissed.

Repository administrators can also verify the API response for
`GET /repos/{owner}/{repo}/branches/main/protection`: the
`required_pull_request_reviews.require_code_owner_reviews.enabled` value must be
`true`, and `required_approving_review_count` must be at least `1`.