# How we work

These are the house rules for every Vebses repository. A repository may add its own `CONTRIBUTING.md` with project-specific details.

## Before your first commit: install the git guards

GitHub's Free plan cannot enforce branch protection or secret scanning on our private repositories, so every developer installs two small git hooks once (from the `vebses-com-setup/git-hooks` folder, `./install.sh`). They apply only to Vebses-com repositories:

- **pre-push** refuses a direct push to `main`; push a branch and open a pull request. Owners can override once with `ALLOW_MAIN_PUSH=1`.
- **pre-commit** refuses `.env` and key files and lines that look like live credentials. Override a false positive once with `ALLOW_SECRETS=1`.

## Branches

- `main` is always deployable and is protected: changes land through pull requests, never by pushing to it directly.
- Branch from `main` and name the branch by purpose: `feat/<short-name>`, `fix/<short-name>`, `chore/<short-name>`.
- Delete the branch after the merge (GitHub does this automatically).

## Commits and pull-request titles

- Use [Conventional Commits](https://www.conventionalcommits.org/): `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`.
- We squash-merge, and the squash commit takes the pull request title and body, so write the PR title the same way: `feat: add checkout page`.

## Pull requests

- Keep them small and focused on one change.
- Fill in the template; link the task and the preview deployment.
- Ask one other developer for a review. Resolve every review thread before merging.
- CI must be green: lint, typecheck, build.
- Merge with **Squash and merge** (default). Use **Enable auto-merge** when you are waiting for CI.

## Secrets and environments

- Never commit `.env` files, keys or credentials. Keep `.env.example` up to date instead.
- Production and preview secrets live in the hosting provider (Vercel project environment variables); CI secrets live in GitHub Actions secrets.
- If a secret leaks, rotate it first, then clean up the history.

## Dependencies

- Dependabot alerts and security updates are on in every repository. Fix **high** and **critical** alerts within a week.
- For regular version updates copy `templates/dependabot.yml` from the organisation's `.github` repository into the project as `.github/dependabot.yml`.

## Starting a new repository

1. Create it under the **Vebses-com** organisation (private by default).
2. Add the `developers` team with **Write** access.
3. Add a CI workflow from the Actions tab (**Node CI (Vebses)** template) or copy one from a similar project.
4. Add `.github/dependabot.yml`, a `README.md` with setup steps, and `.env.example`.
