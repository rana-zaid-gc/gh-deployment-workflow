# gh-deployment-workflow — Deploy a Static Site to GitHub Pages with GitHub Actions

A simple Continuous Deployment project: a **GitHub Actions** workflow that automatically deploys a static website to **GitHub Pages** whenever `index.html` is changed and pushed to the `main` branch.

> Project URL: https://roadmap.sh/projects/github-actions-deployment-workflow

## Live site

Once deployed, the site is available at:

```
https://<your-username>.github.io/gh-deployment-workflow/
```

## What it does

- A static `index.html` page saying "Hello, GitHub Actions!"
- A GitHub Actions workflow (`.github/workflows/deploy.yml`) that:
  - Triggers **only** when `index.html` changes on a push to `main`
  - Builds and deploys the site to GitHub Pages automatically
- Every change to `index.html` redeploys the site — no manual steps

## How it works

```
push to main (changes index.html) → GitHub Actions runs → deploys to GitHub Pages → site is live
```

The workflow runs on GitHub's own servers (a "runner") — no server, SSH, or web server to manage. GitHub handles the hosting.

### The workflow (`.github/workflows/deploy.yml`)

```yaml
on:
  push:
    branches: [ main ]
    paths:
      - 'index.html'      # only deploy when index.html changes
```

The `paths` filter is the key requirement — the workflow only triggers when `index.html` is modified, not on every push.

The job then:
1. **Checks out** the repository code
2. **Configures** GitHub Pages
3. **Uploads** the site files as a Pages artifact
4. **Deploys** the artifact to GitHub Pages

## Setup

1. Create a repository called `gh-deployment-workflow`.
2. Add `index.html`, this `README.md`, and `.github/workflows/deploy.yml`.
3. In the repo: **Settings → Pages → Build and deployment → Source → "GitHub Actions"**.
4. Push a change to `index.html` on `main` — the workflow runs and deploys.
5. Visit `https://<your-username>.github.io/gh-deployment-workflow/`.

## Concepts demonstrated

- **GitHub Actions** — CI/CD built into GitHub
- **GitHub Pages** — free static site hosting
- **Continuous Deployment** — push → automatic deploy
- **Path-filtered triggers** — running a workflow only when specific files change

## What I learned

- Writing a GitHub Actions workflow from scratch (YAML)
- Triggering workflows on specific branches and file paths
- Deploying to GitHub Pages with the official Pages actions
- The difference between Jenkins (self-hosted CI/CD) and GitHub Actions (hosted CI/CD)

---

*A CI/CD project from my DevOps learning journey — using GitHub Actions instead of Jenkins.*
