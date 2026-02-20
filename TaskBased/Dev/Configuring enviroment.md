# Configuring Environment
*(Updated February 19, 2026)*

This guide configures your local development environment for `MyFavoriteAlbums` after downloading the source code. It focuses on preparing tools and dependencies before launching the app. Read [Downloading Source Code](./Downloading%20Source%20Code.md) before continuing.

> **Warning**: If your R setup is incomplete, the app may fail during startup even when the source code is downloaded correctly.

> **Note**: This is developer-focused documentation, but key terms are explained for users who are new to R.

## Defining "Environment"

In this project, the environment includes:

- **R runtime**: the R version installed on your machine.
- **R packages**: external libraries used by the app (`shiny`, `dplyr`, `ggplot2`).
- **Working directory**: the folder R uses as the base path for relative file access.
- **Editor/IDE (Integrated Development Environment)**: usually RStudio for running and debugging local code. Other editors can also be used (for example, VS Code), but they may require extra setup.

## Get Started

Before configuring anything, make sure you have:

- A local copy of this repository.
- Internet access (needed for installing packages from CRAN).
- Permission to install packages on your machine.
- A terminal or RStudio console available.

If you have not downloaded the source yet, complete [Downloading Source Code](./Downloading%20Source%20Code.md) first.

## Step 1: Confirm R Is Installed

In your terminal, run:

```bash
R --version
```

If installed correctly, R prints its version information. The output should resemble the following:

```bash
user@Device MyFavoriteAlbums % R --version

R version X.Y.Z (YYYY-MM-DD) -- "..."
Copyright (C) YYYY The R Foundation for Statistical Computing
Platform: <your-platform>

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```
If the command fails, install R from [CRAN](https://cran.r-project.org/) before continuing.

## Step 2: Open the Project in RStudio (Recommended)

Open the local `MyFavoriteAlbums` folder in RStudio.

RStudio is an IDE. It combines an editor, console, and project tools in one place. It is the preferred tool for most contributors.


Other IDEs can be used; however, extensions and additional configuration may be needed. To start an instance of R in the command line, run:
```bash
user@Device MyFavoriteAlbums % R
```

This opens an interactive R session in your terminal where you can run R commands.

## Step 3: Set and Verify Your Working Directory

The app uses relative file paths such as `data/album-rankings.csv`.
If the working directory is wrong, file loading will fail.

In the R console:

```r
getwd()
setwd("/path/to/MyFavoriteAlbums")
file.exists("data/album-rankings.csv")
```

Expected result: `file.exists(...)` should return `TRUE`.

> **Warning**: If this check fails, your working directory is likely incorrect. Set it again with `setwd("/path/to/MyFavoriteAlbums")` and re-run `file.exists(...)`.

## Step 4: Install Required R Packages

A package is a reusable library of R functions.
This project requires three packages:

- `shiny` for the web app framework.
- `dplyr` for data filtering and transformations.
- `ggplot2` for chart rendering.

Install them in the R console:

```r
install.packages(c("shiny", "dplyr", "ggplot2"))
```

Alternatively, packages can be installed from any terminal (useful when working outside RStudio):
```bash
R -e 'install.packages(c("dplyr","ggplot2","shiny"), repos="https://cloud.r-project.org")'
```

## Step 5: Verify Package Loading

In the R console, verify by running:

```r
library(shiny)
library(dplyr)
library(ggplot2)
```

If no errors appear, your package environment is ready.

## Common Setup Errors

`there is no package called ...`
- **Cause**: dependency not installed.
- **Fix**: rerun `install.packages(...)` and try again.

`cannot open file 'data/album-rankings.csv'`
- **Cause**: working directory is not the project root.
- **Fix**: run `setwd("/path/to/MyFavoriteAlbums")` and verify the file exists.

`could not find function "select"` or `could not find function "filter"`
- **Cause**: `dplyr` was not loaded in your current R session.
- **Fix**: run `library(dplyr)` before executing module files directly.

## Environment-Ready Checklist

You are ready for local execution when all of the following are true:

- R is installed and accessible from terminal or RStudio.
- `shiny`, `dplyr`, and `ggplot2` install and load without errors.
- Working directory points to the `MyFavoriteAlbums` project root.
- `data/album-rankings.csv` is detected from that directory.

## Next Step

Continue to [Running My Favorite Albums locally](./Running%20My%20Favorite%20Albums%20locally.md) to learn how to run a local instance of `MyFavoriteAlbums`.
