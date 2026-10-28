# Single-run automation trial

## Scope

On 2026-10-28, the original counter script from
[spacegpu/pull-shark-automation](https://github.com/spacegpu/pull-shark-automation)
was evaluated locally at commit
`b97a88a3cc243ef9f02b00320d5f0098a17c3855`.

The trial runs the upstream Python script once, then uses one manually initiated
pull request to record these findings. It does not install or enable the
upstream GitHub Actions workflows, upload a token as a repository secret, or
schedule further pull requests. The script receives no GitHub credential.

## Observed result

The local test fixture started with a count of 9. A separate GitHub search had
returned 9 public, authored, merged pull requests for this account at the start
of the trial. This search result is not an achievement progress API.

Running the unchanged upstream `main.py` with Python 3.15.1 produced:

```text
10 pull requests merged<br>Currently:<br>![pull-shark](images/pull-shark-default.png)
```

The output matched the expected string. No pull request had been created by
that script execution: the count changed entirely within the local fixture.
The image path above belongs to the upstream checkout, not this repository.

## What the automation does

- `main.py` reads a local number, increments it, and chooses a badge image using
  local thresholds. It does not query GitHub for merged PRs or awarded badges.
- The upstream update workflow schedules a run every six minutes and uses a
  repository secret named `PAT` to open a PR.
- A separate workflow uses that secret to merge PRs for a hard-coded sender.
  These workflows were inspected but were not executed in this trial.

Source files at the inspected revision:

- [Counter script](https://github.com/spacegpu/pull-shark-automation/blob/b97a88a3cc243ef9f02b00320d5f0098a17c3855/main.py)
- [Scheduled update](https://github.com/spacegpu/pull-shark-automation/blob/b97a88a3cc243ef9f02b00320d5f0098a17c3855/.github/workflows/update.yaml)
- [PR merge workflow](https://github.com/spacegpu/pull-shark-automation/blob/b97a88a3cc243ef9f02b00320d5f0098a17c3855/.github/workflows/merge.yaml)

## Verification limits

A local counter or badge image is not proof of a GitHub achievement. The PR
record and public profile must be checked independently after a merge.
One successful merge cannot establish the current achievement eligibility
rules or guarantee a higher tier. No background automation remains enabled
by this trial.
