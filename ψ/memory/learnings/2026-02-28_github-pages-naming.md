# Lesson Learned: GitHub Pages Naming Conventions

## Context
During the initial deployment of the Sophia Oracle travel map, we encountered a 404 error despite having an `index.html` file in the root of a repository named `heman00p.github.io`.

## Pattern
GitHub distinguishes between **User/Organization Pages** and **Project Pages**:
1. **User/Org Pages**: Must be named exactly `<username>.github.io`. These are served at `https://<username>.github.io/`.
2. **Project Pages**: Can have any name. These are served at `https://<username>.github.io/<repository-name>/`.

In our case, the GitHub account username was `heman1033p-create`, but we attempted to use `heman00p.github.io` (a secondary handle). GitHub did not recognize this as a User Page for the primary account, leading to a 404 until the repository was renamed to `heman1033p-create.github.io`.

## Resolution
- Use `gh repo rename <correct-name>` to align the repository with the owner's username.
- Update the local `git remote` URL to match the new repository name.
- Push a dummy commit or make a small change to trigger the initial Pages build.

## Strategy for Future
Always verify the current `gh auth status` or `git config user.name` before suggesting a repository name for GitHub Pages to ensure automatic deployment success.
