# Unity Project Repository Cleanup Design

## Goal

Publish a complete, reproducible Unity project to `laowang0000/rush-to-clean` so another developer can clone it, open it in the recorded Unity version, and play the game without relying on generated local files.

## Repository contents

Keep the existing `Final MIP/` project root and publish:

- `Assets/`, including scripts, scenes, prefabs, materials, required art, and every paired `.meta` file.
- `Packages/` and `ProjectSettings/`, including the Unity version declaration and package lock file.
- The new environment and tree assets currently untracked in `Assets/`.
- A concise README with the Unity version, cloning/opening instructions, and the expected play flow.

Do not publish Unity-generated or machine-local data: `Library/`, `Logs/`, `Temp/`, `obj/`, `Build*/`, `UserSettings/`, IDE caches, local installers, media tools, or command logs.

## Delivery flow

1. Audit the candidate files against the existing Unity `.gitignore`.
2. Add only the required untracked environment and tree assets.
3. Add the README and validate that the staged paths contain no generated project folders.
4. Commit the curated project state on `main`.
5. Point `origin` to `https://github.com/laowang0000/rush-to-clean.git`, reconcile any remote changes without discarding local work, then push `main`.

## Verification

- Confirm `git diff --check` has no whitespace errors.
- Confirm `git status --ignored` lists Unity-generated folders as ignored, not tracked.
- Confirm every staged Unity asset has its corresponding `.meta` file where Unity requires one.
- Confirm the README names the Unity version from `ProjectSettings/ProjectVersion.txt` and describes how to open and play the project.
- Confirm the final branch and remote URL before pushing.
