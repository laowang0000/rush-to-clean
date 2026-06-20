# Unity Project Repository Cleanup Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a cloneable Unity project to `laowang0000/rush-to-clean` with all runtime assets and configuration, but without generated local data.

**Architecture:** Keep the established Unity project root at `Final MIP/`; Unity resolves assets through their folder paths and `.meta` GUID files. Commit the untracked environment and tree assets together with their metadata, retain `Packages/` and `ProjectSettings/`, and describe exact opening steps in a root README.

**Tech Stack:** Unity `2021.3.23f1`, Git, GitHub.

---

### Task 1: Add reproducible-project instructions

**Files:**
- Create: `README.md`
- Read: `Final MIP/ProjectSettings/ProjectVersion.txt`

- [ ] **Step 1: Read the recorded Unity version**

Run: `Get-Content 'Final MIP/ProjectSettings/ProjectVersion.txt'`

Expected: Output names the Unity editor version used by the project.

- [ ] **Step 2: Create the root README**

Write `README.md` with these sections: project title and one-line description; requirements (Unity Hub and the exact editor version); clone, Unity Hub Open, package restoration, Main Menu scene, and Play instructions; an explanation of `Assets`, `Packages`, and `ProjectSettings`; and a statement that Unity regenerates `Library`, `Logs`, and `UserSettings`.

- [ ] **Step 3: Verify the README contains the editor version**

Run: `rg '2021.3.23f1' README.md`

Expected: The README contains the recorded editor version.

- [ ] **Step 4: Commit documentation**

Run: `git add README.md; git commit -m "docs: add Unity project setup guide"`

Expected: A commit containing only `README.md`.

### Task 2: Stage only required Unity assets

**Files:**
- Add: `Final MIP/Assets/Enviroment.meta`
- Add: `Final MIP/Assets/Enviroment/`
- Add: `Final MIP/Assets/Tree.prefab`
- Add: `Final MIP/Assets/Tree.prefab.meta`
- Add: `Final MIP/Assets/Tree_Textures.meta`
- Add: `Final MIP/Assets/Tree_Textures/`
- Read: `.gitignore`

- [ ] **Step 1: Confirm generated folders are ignored**

Run: `git status --short --ignored`

Expected: `Final MIP/Library/`, `Final MIP/Logs/`, and `Final MIP/UserSettings/` show with `!!` and are not staged.

- [ ] **Step 2: Stage the complete untracked asset groups**

Run: `git add -- "Final MIP/Assets/Enviroment.meta" "Final MIP/Assets/Enviroment/" "Final MIP/Assets/Tree.prefab" "Final MIP/Assets/Tree.prefab.meta" "Final MIP/Assets/Tree_Textures.meta" "Final MIP/Assets/Tree_Textures/"`

Expected: `git status --short` displays only `A` entries beneath these paths.

- [ ] **Step 3: Validate Unity metadata pairing and staging scope**

Run: `git diff --cached --name-only; git diff --cached --check`

Expected: Staged paths are limited to the listed environment and tree asset groups, including their `.meta` files. Unity-generated YAML may report trailing whitespace; retain it because altering serialized prefab or `.meta` text solely for whitespace cleanup can change imported asset content.

- [ ] **Step 4: Commit the required game assets**

Run: `git commit -m "assets: add environment and tree resources"`

Expected: A commit containing the new environment and tree resources, with their `.meta` files.

### Task 3: Publish to the user's repository

**Files:**
- Modify: `.git/config` through `git remote set-url`

- [ ] **Step 1: Replace the origin URL**

Run: `git remote set-url origin https://github.com/laowang0000/rush-to-clean.git; git remote -v`

Expected: Both fetch and push URLs target `laowang0000/rush-to-clean`.

- [ ] **Step 2: Fetch and inspect the target branch**

Run: `git fetch origin main; git log --oneline --left-right main...origin/main; git status --short --branch`

Expected: The commit relationship between local and remote `main` is visible before any push.

- [ ] **Step 3: Push without overwriting remote history**

Run: `git push -u origin main`

Expected: Git reports `main -> main`. If Git rejects a non-fast-forward push, stop before using any force option and reconcile the remote history explicitly.

- [ ] **Step 4: Verify the published tracking state**

Run: `git status --short --branch; git log --oneline -3`

Expected: `main...origin/main` has no ahead/behind count and the cleanup commits appear at the top of history.
