# Running My Favorite Albums Locally
*(Updated February 19, 2026)*

This guide explains how to launch `MyFavoriteAlbums` on your machine after setup is complete.
It focuses on local execution and basic run-time troubleshooting.

> **Warning**: Run the app from the project root directory (`MyFavoriteAlbums`). The app loads files by relative path (for example, `data/album-rankings.csv`), so launching from the wrong folder can cause startup errors.

> **Note**: This page assumes you already completed [Configuring enviroment](./Configuring%20enviroment.md).

## Get Started

Before running the app, confirm:

- Source code is downloaded locally.
- Required packages are installed (`shiny`, `dplyr`, `ggplot2`).
- Your working directory is set to the project root.
- `data/album-rankings.csv` exists in your local project copy.

## Step 1: Open the Project

Open the `MyFavoriteAlbums` folder in your preferred development tool:

- **Recommended**: RStudio
- **Alternative**: Terminal, R command line, preffered IDE

## Step 2: Run the App in RStudio (Recommended)

1. Open `app.R`.
2. Select **Run App** in RStudio.
3. Wait for the local app window (or browser tab) to open.

`app.R` can be executed from the R console:
```r
shiny::runApp(".")
```
or in the Terminal (accessable from [127.0.0.1:3838](127.0.0.1:3838)): 
```bash
cd /path/to/MyFavoriteAlbums
R -e 'shiny::runApp("app.R", host="127.0.0.1", port=3838)'
```

## Step 3: Confirm a Successful Launch

A successful startup should show:

- The title `My Favorite Albums`.
- Tabs for Home, Number One Albums, Top Albums by Year, Artists' Albums, Favorite Artists, Artist Comparison, and Vinyl.
- Data outputs rendering without startup errors in the R console.

Furthermore, the Home page should include details about `album-rankings.csv`. By default, it responds with: 

>Albums in the database: 913
Artists in the database: 464
Artist with most albums in the database: Belle and Sebastian

An empty or modified  `album-rankings.csv` may return different values. Verify that it is correct and that no modifications were made **after** starting the app. 

## Expected Behavior (Not a Bug)

Some tabs do not populate until you select inputs and press **Submit**:

- Top Albums by Year
- Artists' Albums
- Favorite Artists
- Vinyl

This is expected behavior based on how the server logic is implemented.

## Stopping the App

- In RStudio: select **Stop** in the Run App pane or close the preview window. 
- In terminal: press `Ctrl + C`. 

## Common Run Errors

`there is no package called ...`
- **Cause**: a required package is missing.
- **Fix**: install packages with `install.packages(c("shiny", "dplyr", "ggplot2"))`.

`cannot open file 'data/album-rankings.csv'`
- **Cause**: app launched outside project root, or file missing/renamed.
- **Fix**: `setwd("/path/to/MyFavoriteAlbums")`, then verify with `file.exists("data/album-rankings.csv")`.

`could not find function "select"` or `could not find function "filter"`
- **Cause**: `dplyr` not loaded in your active session.
- **Fix**: run the app through `app.R`, or load `library(dplyr)` before running modules directly.

`ERROR: cannot open the connection` (port already in use)
- **Cause**: another process is using the default Shiny port.
- **Fix**: run on a different port, for example:
```r
shiny::runApp(".", port = 8080)
```

```bash
R -e 'shiny::runApp("app.R", host="127.0.0.1", port=8080)'
```

## Next Step

The program can be used as documented. After verifying all systems and pages work as indended, modifications can be made to the code to implement additional pages, filters, and more. See [Modifying and Adding Pages](./Modifying%20and%20Adding%20Pages.md) for more information. 
