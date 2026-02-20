# Modifying Album Data
*(Updated February 19, 2026)*

This guide explains how to safely edit `data/album-rankings.csv` so the app reflects your preferred albums, ratings, and metadata.

> **Warning**: You should back up `album-rankings.csv` before editing. Formatting mistakes can prevent pages from loading correctly.

> **Note**: Data is loaded after the app is executed and the server is loaded. Restart the program after modifying data to update app. 

## Get Started

Before editing data, confirm:

- The app is closed (recommended while editing the CSV).
- You have a backup copy of `data/album-rankings.csv`.
- You can edit CSV files with a spreadsheet tool or text editor.

## Required Column Structure

Keep the header row (first line in file) exactly as:

`Year,Ranking,Album,Artist,Rating,Vinyl,EP,Live`

Column expectations:

- `Year`: numeric year value.
- `Ranking`: numeric ranking value.
- `Album`: album title text.
- `Artist`: artist name text.
- `Rating`: numeric rating value (use a consistent scale).
- `Vinyl`: use `v` for owned on vinyl, or leave blank.
- `EP`: use `EP` when applicable, or leave blank.
- `Live`: use `Live` when applicable, or leave blank.

Below is an example of editing the `album-rankings.csv` file in the spreadsheet tool *Excel*
![CSV file open in a spreadsheet tool showing required column headers and row structure.](../Resources/Screenshot%202026-02-20%20at%201.25.42 AM.png)

>**Warning**: Some spreadsheet tools might prompt you to save into a different file format (e.g. `.XLSX`, `.numbers`, ect...), make sure to save in a `.csv` format to maintain comptability. 

## How to Add or Edit Rows
1. Open `data/album-rankings.csv`.
2. Update existing rows or add new rows in the correct column order.
3. Keep one value per column in the same order as the header.
4. If album or artist names include commas, use proper CSV quoting (enclosing , in "").
5. Save the file as `.csv`.


## Reload and Validate Changes

1. Restart the app. If running on a local server, read [Running My Favorite Albums locally](../Dev/Running%20My%20Favorite%20Albums%20locally.md) to learn more.
2. Verify updates on relevant tabs:
a. Top Albums by Year (year-specific changes)
b. Artists' Albums (artist-specific changes) 
c. Vinyl (ownership markers)
d. Favorite Artists (total rating changes)
3. Confirm results match your expected edits.

## Expected Edge Cases

- CSV edits typically appear after app restart, never mid-session.
- Name variations (for example, typos or spacing differences) are treated as different artists.
- Duplicate ranking values in the same year can appear as multiple rows.

## Troubleshooting

`A tab shows missing or strange results after edits`
- Re-check column order and values in the CSV.
- Confirm no rows were shifted into the wrong columns.

`An artist appears twice unexpectedly`
- Check for spelling or spacing differences in artist names.

`A value is not reflected in the app`
- Save the CSV again and restart the app.
- Verify you edited the correct local project file.

