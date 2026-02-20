# Downloading Source Code
*(Updated February 19, 2026)*

This guide shows how to download the `MyFavoriteAlbums` source code to your machine.
It covers download only, not app configuration or execution.

> **Warning**: Before continuing, confirm your local environment is ready for R-based projects.
If your R setup is incomplete, you may be able to download the project but fail in later steps.

> **Note**: This developer guide assumes basic familiarity with Git, terminal commands, and R tooling.

## Get Started

Before the download steps, make sure you have:

- Access to GitHub and the project repository: [MyFavoriteAlbums](https://github.com/UW-Example-Student/MyFavoriteAlbums).
- A working installation of R.
- A Shiny-capable R environment (commonly RStudio).
- A local folder where you have permission to create project files.

Repository URL: [https://github.com/UW-Example-Student/MyFavoriteAlbums](https://github.com/UW-Example-Student/MyFavoriteAlbums)

## Downloading Project Files

The source code is hosted on GitHub: [MyFavoriteAlbums repository](https://github.com/UW-Example-Student/MyFavoriteAlbums)

Choose one method to download the source code:

1. [Download from web interface](#option-1-downloading-from-web-interface)
2. [Download using CLI](#option-2-downloading-using-cli)

Both methods produce a local copy of the same project files.

CLI is preferred for developers because it makes future pulls and branching easier. A ZIP download can be converted into a Git-tracked project later, but cloning is usually simpler.

### Option 1: Downloading from web interface

Use this if you want a **quick one-time copy** and do not need Git history immediately.

1. Open the repository URL in your browser.
2. Select the **Code** button near the top-right of the repository file list.
![GitHub repository Code dropdown showing Download ZIP option](../Resources/Screenshot%202026-02-19%20at%209.42.55%E2%80%AFPM.png)
3. Select **Download ZIP**.
4. Wait for the download to finish.
5. Extract the ZIP file into your chosen local directory.
6. Rename the extracted folder if needed for consistency.
Example extracted name format: `<project-name>-<branch-name>` (such as `MyFavoriteAlbums-main`).

### Option 2: Downloading using CLI

Use this if you plan to contribute, sync with updates, or manage branches.

> **Note**: This method requires Git. Follow the install guide: [git-scm.com/install](https://git-scm.com/install/)

1. Open a terminal. This may vary depending on your operating system.
Windows: PowerShell or Git Bash.
macOS/Linux: Terminal.
2. Navigate to the parent directory where you want the project folder.
```bash
cd /path/to/your/projects
```
3. Clone the repository.
```bash
git clone https://github.com/UW-Example-Student/MyFavoriteAlbums.git
```
4. Move into the project directory.
```bash
cd MyFavoriteAlbums
```
5. Confirm key files are present (`app.R`, `app_ui.R`, `app_server.R`, `data/album-rankings.csv`, etc.).

## Next Step

Continue to [Configuring enviroment](./Configuring%20enviroment.md) to install required libraries for local development.
