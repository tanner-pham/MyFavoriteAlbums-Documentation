# UI Navigation
*(Updated February 19, 2026)*

This guide helps you orient yourself in the `MyFavoriteAlbums` interface and move between pages confidently.
It focuses on user navigation behavior only. Task-specific actions are covered in separate page guides.

> **Note**: Some tabs require clicking **Submit** before results appear. A blank table area on first load can be normal.

> **Note**: This is a non-technical guide focused on what users see and do in the app interface. To learn more about implementing custom pages, see [Modifying and Adding Pages](../Dev/Modifying%20and%20Adding%20Pages.md).

## Get Started

Before using this guide, confirm:

- The app is running and visible in your browser/app preview.
- You can see the main title: `My Favorite Albums`.
- Below the main title, you can see the top row of tabs.

## App Layout at a Glance

The interface has three main parts:

- **Title area** at the top of the page.
- **Tab row** directly under the title.
- **Content area** below the tabs, which changes based on the tab you select.

![Main My Favorite Albums interface showing title, tab row, and active content area.](../Resources/Screenshot%202026-02-19%20at%2011.24.16 PM.png)

## Navigating Between Tabs

Use the top tab row to switch pages:

- Click any tab once to switch to its view.
- Your previously selected dropdown values usually stay in place while the app session remains open.
- Some tabs refresh results immediately, while others wait for a **Submit** click.

Tabs that require **Submit** to refresh their table output:

- Top Albums by Year
- Artists' Albums
- Favorite Artists
- Vinyl

## What Each Tab Does

- **Home**: shows a welcome message and quick overview statistics from the `album-rankings.csv` data file.
- **Number One Albums**: shows top-ranked albums for the selected year range.
- **Top Albums by Year**: shows ranked albums for one selected year after user action.
- **Artists' Albums**: shows albums and summary information for one selected artist after user action.
- **Favorite Artists**: shows artists that meet selected criteria after user action.
- **Artist Comparison**: shows a side-by-side visual comparison of two selected artists.
- **Vinyl**: shows high-rated albums not currently marked as owned on vinyl after user action.

## Troubleshooting Navigation Issues

`I clicked a tab and see no table`
- Check whether that tab requires **Submit**.
- Select inputs if needed, then click **Submit**.

`I changed dropdowns and nothing happened`
- On submit-based tabs, dropdown changes do not always auto-refresh the table.
- Click **Submit** to apply your current selections.

## Next Step

Use a task-specific page for deeper guidance:

- [No1 Albums](./No1%20Albums.md)
- [Albums by Year](./Albums%20by%20Year.md)
- [Albums by Band](./Albums%20by%20Band.md)
- [Favorite Bands](./Favorite%20Bands.md)
- [Compare Bands](./Compare%20Bands.md)
- [Vinyl](./Vinyl.md)
