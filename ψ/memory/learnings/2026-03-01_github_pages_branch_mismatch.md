# Lesson Learned: GitHub Pages and Default Branch Mismatch

**Date:** 2026-03-01
**Tags:** #github-pages #github-actions #deployment #viem #esm

## Context
While attempting to deploy a static HTML page (`floodboy-monitor.html`) to GitHub Pages, the deployment silently failed and the site returned a 404 error, even though the code was successfully pushed to the `main` branch. Additionally, the `viem` library was causing an infinite loading spinner due to a missing UMD build.

## Key Insights
1. **GitHub Pages Default Branch Expectation:** If a repository was created under older defaults or without an explicit main branch designation, GitHub may designate `master` as the default branch at the repository metadata level. When code is pushed to `main`, GitHub Pages (and sometimes GitHub Actions) will silently ignore it since it expects the default branch to match.
2. **ES Modules for Browser APIs:** Libraries like `viem` v2 no longer provide official UMD bundles. They must be imported as ES Modules using a CDN like `esm.sh` in a `<script type="module">` block.

## Resolution
- **Viem Issue:** Replaced traditional `<script src="...">` with an ES module setup: `import { createPublicClient, http } from 'https://esm.sh/viem@2'`.
- **Pages Issue:** Updated the repository's default branch setting to `main` via the GitHub API (`gh api -X PATCH repos/{owner}/{repo} -f default_branch="main"`), which allowed both the legacy Pages engine and Actions to recognize the branch and trigger the build.
