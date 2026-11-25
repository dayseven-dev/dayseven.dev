# Contributing

This file is the rulebook for working on this project. It explains how branches are named and
merged, how work moves from DEV to PROD, how commits and pull requests are written, how versions are
numbered, and how issues are reported. Read it before your first contribution; following it keeps
the history clean and reviews quick.

## Branching Strategy

### Long-lived branches

- `dev` holds the current sprint's merged work and deploys to DEV.
- `main` holds what is released and deploys to PROD. Every release is a tag on `main` (for example
  `v1.0.0`).
- Both branches keep a linear history: no merge commits on either.
- Never commit directly to `dev` or `main`. They change only through pull requests. The only
  exceptions are the release fast-forward and the hotfix rebase below, which only a maintainer
  does.

### Working branches

Name every working branch `type/branch-name`:

- `type` is one of the values below.
- `branch-name` is short, lowercase and kebab-case, and describes the change, not the author or an
  issue number alone.

| Type            | Use for                                                              |
|-----------------|----------------------------------------------------------------------|
| `feature`       | A new feature                                                        |
| `fix`           | A bug fix                                                            |
| `hotfix`        | An urgent fix to what is live on PROD                                |
| `refactor`      | A change that neither adds a feature nor fixes a bug                 |
| `perf`          | A change that makes the app faster or lighter                        |
| `revert`        | Undoing an earlier change                                            |
| `setup`         | Project and module setup: new modules, source sets, plugins, tooling |
| `build`         | Changes to the build: Gradle, dependencies, versions                 |
| `ci`            | CI configuration                                                     |
| `docs`          | Documentation only                                                   |
| `test`          | Adding or fixing tests                                               |
| `chore`         | Anything else that does not touch app behaviour                      |

Examples: `feature/contact-search`, `fix/status-filter`, `hotfix/login-crash`.

### Workflow

1. Branch off the latest `dev`.
2. Keep the branch focused on one change and short-lived.
3. Write commit messages as `type: message`, using the same types as branches, in lowercase and the
   imperative (for example `fix: correct the status filter`).
4. Sign off every commit with `git commit -s` (see [License and sign-off](#license-and-sign-off)).
5. Open a pull request into `dev`. A contributor's pull request needs a maintainer's approval
   before it is merged.
6. Merge with GitHub's **Rebase and Merge**, so `dev` stays linear.
7. Delete the branch after it is merged.
8. If the pull request conflicts with `dev`, rebase your branch on `dev`, resolve the conflicts and
   force-push your own branch with `--force-with-lease`.

### Releases

Work is planned in sprints and ships once per sprint:

1. At the end of a sprint, once DEV is tested, fast-forward `main` to `dev` from the command line
   (`git merge --ff-only dev`). GitHub's UI cannot fast-forward, and Rebase and Merge would copy
   the commits with new hashes, so `main` and `dev` would drift apart.
2. Tag the release commit on `main` with the next minor version (see [Versioning](#versioning)).

### Hotfixes

1. Branch `hotfix/...` off `main` and open the pull request into `main`.
2. Merge with **Rebase and Merge** and tag the new patch version.
3. Rebase `dev` on `main` and push it with `--force-with-lease`, so `dev` has the fix and both
   branches stay linear.

### Contributing from a fork

Fork the repository, then follow the same steps in your fork: branch off `dev` and open the pull
request against `dev`.

## Pull Requests

- One change per pull request.
- Pull requests go into `dev`. Only `hotfix/...` pull requests go into `main`.
- The title is plain sentence case in the imperative, at most 70 characters, with no type prefix
  and no full stop (for example `Add contact search to the tracker`).
- The description follows the [pull request template](.github/pull_request_template.md).
- CI must pass before merging.
- A contributor's pull request needs a maintainer's approval. A maintainer may merge their own pull
  request once CI passes.

## Versioning

This project uses [Semantic Versioning](https://semver.org) as `vMAJOR.MINOR.PATCH`, with one
version for every platform. A release ships Android, iOS, desktop, web and the backend under the
same number.

| Change                 | Bump  | Example             |
|------------------------|-------|---------------------|
| Breaking change        | MAJOR | `v1.4.2` → `v2.0.0` |
| Sprint release         | MINOR | `v1.4.2` → `v1.5.0` |
| Hotfix                 | PATCH | `v1.4.2` → `v1.4.3` |

- Versions stay at `0.x` until the first public launch, which is `v1.0.0`.
- Android's `versionCode` is derived from the version (`1.4.0` → `10400`). Never bump it by hand.

## Issues

- Search existing issues before opening a new one.
- Use the **Bug report** template (platform, version, steps to reproduce, expected and actual
  result, screenshots) or the **Feature request** template (the problem, the proposed solution).
- Questions and ideas go to GitHub Discussions, not issues.
- Every issue gets a type label (the branch types above) and a platform label (`android`, `ios`,
  `desktop`, `web`, `extension`, `backend`).

## Security

Never report a vulnerability in a public issue. Follow [SECURITY.md](SECURITY.md) to report it
privately.

## License and Sign-off

This project is licensed under [AGPL-3.0](LICENSE). By contributing, you agree that your
contribution is licensed under the same license.

Every commit must be signed off under the
[Developer Certificate of Origin](https://developercertificate.org), which states that you wrote
the change or have the right to submit it. Sign off with `git commit -s`. A pull request with
unsigned commits cannot be merged.

## Code of Conduct

Everyone taking part in this project follows the [Code of Conduct](CODE_OF_CONDUCT.md).