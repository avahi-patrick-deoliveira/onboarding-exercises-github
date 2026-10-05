# TKK-003 — Merge Conflict: Create, Trigger, and Resolve

This document records how a merge conflict was created, triggered and resolved.

## 1. Create two branches from `main`

Both branches start from the same commit and edit **line 1 of `README.md`**, the file changed in TKK-002.

```bash
git checkout main
git checkout -b tkk-003-merge-conflict
# line 1 -> "# Onboarding Exercises - Module 4 (edit from branch A)"
git commit -am "TKK-003 - Change README title (branch A)"

git checkout main
git checkout -b tkk-003-conflicting-branch
# line 1 -> "# Git Onboarding Exercises - Module 4 (edit from branch B)"
git commit -am "TKK-003 - Change README title (branch B)"
```

Same line, different content: Git cannot decide automatically which one wins.

## 2. Trigger the conflict

```bash
git checkout tkk-003-merge-conflict
git merge tkk-003-conflicting-branch
```

Output:

```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

`git status` shows `README.md` as `UU` (both modified, unmerged).

## 3. Inspect the conflict markers

```
<<<<<<< HEAD
# Onboarding Exercises - Module 4 (edit from branch A)
=======
# Git Onboarding Exercises - Module 4 (edit from branch B)
>>>>>>> tkk-003-conflicting-branch
```

- `<<<<<<< HEAD` to `=======`: the version on the current branch (A).
- `=======` to `>>>>>>>`: the version from the branch being merged (B).

## 4. Resolve manually

I edited `README.md`, removed the markers and wrote the final line:

```
# Git Onboarding Exercises - Module 4 (resolved merge)
```

## 5. Stage and commit

```bash
git add README.md
git commit -m "TKK-003 - Resolve merge conflict in README.md"
```

## Takeaways

- A conflict happens when two branches change the same lines differently.
- Git stops the merge and leaves markers in the file; nothing is lost.
- Resolving means editing the file, then `git add` to mark it resolved, then `git commit`.
- `git merge --abort` cancels the merge if you want to start over.
