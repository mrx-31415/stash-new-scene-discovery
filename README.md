# New Scene Discovery

A Stash plugin that finds recently released scenes from your performers on StashDB. Opens as a dedicated page showing a feed of new scenes you don't own yet, filtered to performers in your library.

<!-- screenshots -->

## Requirements

- [Stash](https://stashapp.cc) v0.27+
- A [StashDB](https://stashdb.org) account linked in Stash (**Settings → Metadata Providers → StashBox**)
- Performers in your library must have StashDB IDs linked

## Installation

1. Download this repository (Code → Download ZIP) and extract it
2. Place the extracted folder inside a category subfolder of your Stash plugins directory:
   - **Linux/Mac:** `~/.stash/plugins/UI & Stats/New Scene Discovery/`
   - **Windows:** `%USERPROFILE%\.stash\plugins\UI & Stats\New Scene Discovery\`

   > The plugin must be **two levels deep** inside the plugins directory — `plugins/Category/Plugin/`. Placing it directly under `plugins/` will cause it not to appear in Stash.

3. In Stash, go to **Settings → Plugins** and click **Reload Plugins**
4. Enable **New Scene Discovery**
5. A **🔥 New Releases** button will appear in the Stash navigation bar

## Usage

Click **🔥 New Releases** in the nav bar — the page opens in a new tab showing a grid of recently released scenes from your performers that you don't already have in your library.

- **Search** performers in the feed using the search bar
- **Filter pills** let you narrow the feed to specific performers
- **Favorites toggle** (♥) filters to only scenes featuring performers you have marked as a favorite in Stash
- **Refresh** forces a fresh fetch from StashDB, bypassing the cache
- **Copy ID** (appears on hover) copies the StashDB scene ID to your clipboard for easy importing

Results are cached for 12 hours to avoid hammering the StashDB API on every page load.

## Configuration

Go to **Settings → Plugins → New Scene Discovery** to configure:

| Setting | Default | Description |
|---|---|---|
| New Releases (in Days) | `90` | How far back to look for new scenes |
| Max Scenes Per Performer | `0` | Cap scenes per performer to prevent one from dominating the feed (0 = unlimited) |
| Default to Favorites Only | `false` | If enabled, the favorites filter is on by default when you open the page |

> **Note:** Due to a bug in Stash, settings fields will appear blank even when defaults are set. You don't need to fill them in — the plugin uses the defaults shown above automatically if a field is left empty. Only enter a value if you want to override the default.

## How It Works

1. Fetches all performers from your Stash library that have a StashDB ID linked
2. Queries StashDB in batches for scenes released after the cutoff date featuring those performers
3. Filters out scenes you already own (matched by StashDB ID)
4. Displays the remaining scenes sorted by release date, newest first
