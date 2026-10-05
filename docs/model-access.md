# Access Model

**Roles**
- Owner (me): Admin, because I manage the settings
- Collaborators: I added Tania Alcantara
  - Why: she can push branches and open PRs, but can't change settings

**Branch protection on main**
- Require a pull request before merging, with 1 approval
- Require status checks to pass
- Do not allow bypassing
- Why: nobody pushes straight to main, so every change is reviewed and checked first

**Secrets**
- `EXAMPLE_SECRET`
- Why: keeps sensitive values out of the code, and only admins can see them
