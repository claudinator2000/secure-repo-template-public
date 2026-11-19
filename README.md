# Secure repository template

A small starting point for private GitHub repositories.

## Start

1. Select **Use this template** and create the destination as **private**.
2. Replace this README with the project's own, including a private security
   contact; [`SECURITY.md`](SECURITY.md) directs reporters to it. If the
   repository is made public, also enable private vulnerability reporting
   under **Settings → Security**.
3. Add the application's own tests.
4. Review the first security workflow runs before merging product code.

## Included

- Gitleaks secret detection, with a self-test that fails if a generated
  fake token goes undetected.
- Trivy dependency and configuration scanning on changes and weekly.
- zizmor analysis of GitHub Actions.
- Read-only workflow permissions and immutable Action pins.
- Dependabot updates for GitHub Actions.
- Pull-request and private vulnerability-reporting guidance.

## Engineering guidance

[priors](https://github.com/claudinator2000/priors-public) contains cross-project
guidance for humans and coding assistants. [`AGENTS.md`](AGENTS.md) requires
compatible assistants to read it before security-relevant work, follow it, and
stop and ask when it cannot be read. CI does not fetch it. A project that does
not use priors deletes the **Engineering priors** section of `AGENTS.md`.

## Organization accounts

Gitleaks Action needs a free `GITLEAKS_LICENSE` secret when the repository
belongs to an organization; personal accounts need none. See the
[Gitleaks Action documentation](https://github.com/gitleaks/gitleaks-action#environment-variables).

## Trivy exceptions

High and Critical dependency or configuration findings fail the workflow,
including findings without a known fix. Prefer remediation. If an exception is
necessary, use a narrowly scoped `.trivyignore.yaml` entry with a reason, an
owner or tracking issue, and an expiry or review date. Review the exception in
the same pull request; do not disable the workflow or reduce its severity
threshold.

## Limits

The template does not build or scan application images. A container-producing
project supplies a build pipeline that builds once, scans that exact image with
Trivy, and publishes or deploys only the scanned digest.

Dependabot updates only GitHub Actions. Add an entry to
`.github/dependabot.yml` for each package ecosystem the project adds.

The template also does not configure repository settings or provide
application-specific tests or deployment. CodeQL is not included because
GitHub code scanning is unavailable to private personal repositories on GitHub
Free and Pro.

## Licence

[MIT](LICENSE)
