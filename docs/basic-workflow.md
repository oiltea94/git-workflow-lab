# Basic Git workflow

Practice a complete pull request with a small README change. You need Git and
permission to push to this repository. Authenticate using a credential manager
or SSH; never put access tokens in files.

## 1. Get the repository

For a new checkout:

```sh
git clone https://github.com/oiltea94/git-workflow-lab.git
cd git-workflow-lab
```

For an existing checkout, open its directory and run `git status`. Commit or
stash unfinished work before switching branches; do not discard it.

## 2. Create a branch

```sh
git switch main
git pull --ff-only origin main
git switch -c docs/update-readme
```

Choose another branch name if this one exists. If the pull reports diverged
branches, inspect the history before proceeding.

## 3. Edit and check

Make a useful clarification in README.md, then inspect and commit it:

```sh
git diff -- README.md
git diff --check
git add README.md
git diff --cached
git commit
```

Enter a descriptive commit message in the editor, then save and close it.
If Git requests an identity, configure your own name and email for this
repository. A GitHub-provided noreply email can protect your personal email.
Do not commit credentials, generated files, or unrelated changes.

## 4. Push and open a pull request

```sh
git push -u origin docs/update-readme
```

On GitHub, open a pull request with `main` as the base and
`docs/update-readme` as the compare branch. Describe the change and checks.
Inspect the Files changed tab to confirm the PR contains only the intended
README update.

## 5. Merge and sync

Wait for any required checks and reviews. Follow repository protection rules
and merge only when the change is ready. In a personal practice repository
without required reviews, the owner can inspect and merge a documentation PR.

After GitHub reports that the PR is merged:

```sh
git switch main
git pull --ff-only origin main
git status
```

Keep the practice branch until its changes are confirmed on main. This
workflow does not require force pushes or bypassing repository rules.
