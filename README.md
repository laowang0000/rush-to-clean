# Rush to Clean

Rush to Clean is a Unity game project.

## Requirements

- Unity Hub
- Unity 2021.3.23f1

## Run locally

1. Clone this repository.
2. In Unity Hub, choose **Open** and select the `Final MIP` folder inside the clone.
3. Allow Unity to restore packages from `Final MIP/Packages/manifest.json`.
4. Open `Final MIP/Assets/Scenes/Main Menu/MainMenuScene.unity`.
5. Press Unity's **Play** button.

## Repository layout

- `Final MIP/Assets` contains game scripts, scenes, prefabs, materials, and art assets.
- `Final MIP/Packages` contains the Unity package manifest and lock file.
- `Final MIP/ProjectSettings` contains the project and editor settings.

Unity recreates `Library`, `Logs`, and `UserSettings` locally after the project is opened, so those generated folders are intentionally not versioned.
