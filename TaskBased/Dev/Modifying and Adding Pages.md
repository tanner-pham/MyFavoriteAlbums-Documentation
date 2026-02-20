# Modifying and Adding Pages
*(Updated February 19, 2026)*

This guide explains how to add or modify pages in `MyFavoriteAlbums`.
It assumes you already know how to write R functions and focuses on navigation wiring and internal naming schemes.

> **Warning**: In this app, UI IDs are global. Reusing an existing input/output ID in a new tab can break unrelated pages.

## Get Started
Before adding a page, confirm:

- The app runs locally from `app.R` by default.
- You know which data fields your new page will use.
- You have a unique page "slug" name (e.g. `album_trends`).

## Runtime Flow: App Start to User Interaction

When the app starts, this is the typical execution path:

1. `app.R` loads libraries, then `source()` loads UI, server, and feature files (example with `album_trends.R`).
2. While loading `app_ui.R`, the app reads `data/album-rankings.csv` into `album_data`, builds shared vectors such as `all_years`, and creates the full `ui` object.
3. `app_server.R` registers output bindings and event handlers (including `observeEvent(...)` for pages that use a Submit button).
4. `shinyApp(ui = ui, server = server)` starts the Shiny session and serves the page.

When a user interacts with the new page:

1. User opens the tab and changes `album_trends_year` (this updates `input$album_trends_year`).
2. User clicks `album_trends_submit`, triggering `observeEvent(input$album_trends_submit, { ... })`.
3. Server calls `album_trends_table_data(input$album_trends_year)`.
4. The function filters `album_data` and returns a data frame.
5. `renderTable(...)` pushes the returned data to `tableOutput("album_trends_table")`.
6. The UI updates and displays the filtered rows.

This is why pages using `observeEvent(...)` often look blank until the first Submit click.

## Navigation Wiring

A new page requires coordinated updates in three places:

1. `app_ui.R`: Add the page as `tabPanel(<PageSlug>, ...)` entry to the `tabsetPanel(...)`.
2. `app_server.R`: add matching `output$...` and optional `observeEvent(...)` logic if your page requires user interaction.
3. `app.R`: `source("<FileName>.R")` the new page function file (if you created one).

If one layer is missing, the page can *and will eventually* render blank or throw errors at run time.

## Naming Scheme

Use one consistent slug per page and prefix all IDs with it.

>**Warning**: Avoid generic IDs like `text3` or `action_button2` for new declarations. This can make the code less readable and make cross-file references confusing. 

Example slug:
- `album_trends`

Recommended naming:

- File: `album_trends.R`
- Tab label: `"Album Trends"`
- Header output ID: `album_trends_title`
- Input IDs: `album_trends_year`, `album_trends_artist`
- Action button ID: `album_trends_submit`
- Output IDs: `album_trends_table`, `album_trends_plot`
- Function names in feature file: `album_trends_table_data()`, `album_trends_plot_data()`


## Step 1: Add the Tab to Navigation (`app_ui.R`)

Inside `tabsetPanel(...)`, add a new `tabPanel()` entry.
Order in `tabsetPanel(...)` from top &rarr; bottom controls order in the nav bar from left &rarr; right. Place the new page where appropriate.

An example `tabPanel()` has the following:

```r
tabPanel("Album Trends",
         htmlOutput("album_trends_title"),
         selectInput("album_trends_year", "Choose a year:", all_years),
         actionButton("album_trends_submit", label = "Submit"),
         tableOutput("album_trends_table"))
```

>**Warning**: Every ID string used in `htmlOutput(...)`, `selectInput(...)`, `actionButton(...)`, `tableOutput(...)`, and `plotOutput(...)` must be unique across the entire app. Duplicate IDs may break references or cause errors at runtime. 

## Step 2: Add Server Bindings (`app_server.R`)

Create outputs with exactly matching IDs. An example of the syntax is as follows:

```r
output$album_trends_title <- renderUI({
  HTML("<h2>Album Trends</h2><br>")
})

observeEvent(input$album_trends_submit, {
  output$album_trends_table <- renderTable({
    album_trends_table_data(input$album_trends_year)
  })
})
```

ID mapping must match exactly for proper functionality. For example:

- `htmlOutput("album_trends_title")` -> `output$album_trends_title`
- `actionButton("album_trends_submit", ...)` -> `input$album_trends_submit`
- `tableOutput("album_trends_table")` -> `output$album_trends_table`

## Step 3: Source Feature File (`app.R`)

If you created a new page file, add a `source()` call in `app.R`:

```r
source("album_trends.R")
```

Keep this in the same group as the other feature files.

> **Note**: `source()` order can matter when one file depends on objects or functions from another file. Keep shared dependencies (like `app_ui.R`) loaded before feature files that use them.

## Example: What Happens in `album_trends.R`

Inside an example `album_trends.R`, the feature functions usually:

1. Receive user-selected values (such as year or artist) from `app_server.R`.
2. Read from `album_data` (loaded once from `data/album-rankings.csv` in `app_ui.R`).
3. Filter/select/summarize data for the page.
4. Return a plain data frame (for `renderTable`) or a plot object (for `renderPlot`).

`album_trends.R` may look like:

```r
album_trends_table_data <- function(year.var){
  trends_table <- select(filter(album_data[order(album_data$Ranking),], Year == year.var), Ranking, Album, Artist, Rating)
}
```

## Modifying an Existing Page Safely

When renaming IDs, **you must** update both UI and server in the same change.
If you rename only one side, Shiny will fail to pair inputs and outputs correctly.

A safe rename workflow is as follows:

1. Rename IDs in `app_ui.R`.
2. Rename matching `input$...` and `output$...` references in `app_server.R`.
3. Run locally and click through the affected tab.
4. Confirm no startup errors in the console and expected the page reflects the expected output. 

## Quick Validation Checklist

After adding or modifying a page, verify:

- New tab appears in navigation.
- Header text renders.
- Inputs are visible and interactive.
- Submit button (if used) triggers expected output.
- No `object not found` or missing ID errors in console.

## Common Integration Errors

`object 'input$<id>' not found` or output never renders
- **Cause**: UI and server IDs do not match exactly.
- **Fix**: compare ID strings character-by-character.

Page loads, but output area stays blank
- **Cause**: output only renders inside `observeEvent(...)` and the button was not clicked yet.
- **Fix**: click Submit, or move output logic outside `observeEvent(...)` for automatic rendering.

`could not find function ...`
- **Cause**: new feature file not sourced in `app.R`.
- **Fix**: add `source("<your_file>.R")` and restart the app.
