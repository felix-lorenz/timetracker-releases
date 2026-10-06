# Time Tracker

A native macOS time tracker with a weekly calendar and quick capture in the menu bar.

## Distribution

Download the latest version from [GitHub Releases](https://github.com/felix-lorenz/timetracker-releases/releases/latest), or install it through [felix-lorenz/homebrew-tap](https://github.com/felix-lorenz/homebrew-tap).

This repository provides product documentation, release notes, distribution archives, and support through GitHub Issues. The source repository is private.

## Features

- Start tracking immediately, with optional booking text, project, and a locally maintained Jira issue.
- Start, switch, and stop timers from the main window or menu bar.
- Review and edit time in a weekly calendar with daily totals, including entries that cross midnight, and edit a running entry's details and start time without stopping it.
- Reuse topic templates while keeping each existing entry's booking text, project, and Jira issue unchanged by template edits.
- Preselect the latest booking's project and Jira issue for new capture, and restore historical assignments when choosing a topic suggestion.
- Start a new topic immediately from the menu bar and edit its details while the timer runs; canceling the editor leaves the timer running.
- Use consistent project-color brightness and saturation, an opaque menu-bar capsule with subtle daily progress, and compact timers; remove recent-topic shortcuts without deleting historical records.
- Keep tracking records locally, with atomic saves and a backup of the previous valid snapshot.
- Export completed records as a neutral CSV.
- Preview, export, and transfer worklogs through the optional Tempo Cloud connection, with a local journal to prevent duplicate in-app transfers.

The current interface is German. Local tracking does not require a Jira connection, Homebrew, or API tokens. Maintaining an issue locally does not create it in Jira.

The neutral CSV is **not a verified Tempo import format**. Tempo Cloud requires the user's own Jira and Tempo credentials and assigns worklogs to that user's account. Every transferred worklog requires exactly one locally maintained Jira issue. Live Tempo transfer and access permissions remain acceptance checks; development validation uses mocked HTTP and isolated demo data.

Tempo combines completed bookings with the same exact booking text, Jira issue, required attributes, and day in the author's Jira profile time zone. Captured durations are summed before each worklog is rounded to the nearest 15 minutes, with halfway values rounded up and a minimum of 15 minutes. Worklogs transfer their date and duration without the captured start time. Local records remain unchanged.

Required Tempo work attributes appear as immutable per-ticket preview columns. This version automatically reads a required Tempo Account from the Jira issue and resolves its account key through Tempo. This requires Accounts read access in addition to Worklogs Manage access. Missing or unavailable defaults, including other required attribute types, block the affected bookings while valid groups remain importable. Tempo validates Account applicability during transmission; acceptance in the intended installation remains a live check.

## Screenshots

![Weekly calendar](assets/screenshots/weekly-calendar.png)

Time Tracker 0.3.0 — weekly calendar in an isolated demo view.

![Menu bar popover](assets/screenshots/menu-bar-popover.png)

Time Tracker 0.3.0 — menu bar popover in an isolated demo view.

## Requirements

- macOS 27 (Golden Gate) or later
- Apple Silicon (arm64)
- Homebrew only for installation through the Homebrew cask; direct ZIP installation does not require Homebrew

Distribution builds use Developer ID Application signing, Hardened Runtime, and Apple notarization. Runtime checks on another Mac remain a separate acceptance check.

## Installation and updates

### Direct download

1. Download the ZIP asset from the [latest release](https://github.com/felix-lorenz/timetracker-releases/releases/latest).
2. Extract the archive and move `Time Tracker.app` to `/Applications`.
3. Open Time Tracker from Applications.

To update, quit Time Tracker before replacing the app with the latest download. Quitting preserves an active timer; stop it first if you want tracking to end.

### Homebrew

Install [Homebrew](https://brew.sh), then run:

```sh
brew tap felix-lorenz/tap
brew install --cask felix-lorenz/tap/timetracker
```

To update, quit Time Tracker and run:

```sh
brew update
brew upgrade --cask felix-lorenz/tap/timetracker
```

Quitting does not stop an active timer. Installation and updates preserve local tracking records and the Tempo import journal.

## Data and credentials

Tracking records and the Tempo import journal are stored in `~/Library/Application Support/Time Tracker/`. Jira and Tempo tokens are stored in the macOS login Keychain. Back up the tracking file and import journal together; the journal records transfers that must not be repeated.

Version 0.2.0 upgrades older tracking data in memory to store each entry's own booking text and project. Loading alone leaves the file unchanged; the first successful change saves the upgraded format and backs up the original file. Older app versions cannot read the upgraded tracking file.

Replacing the development build with a Developer ID signed build may require reauthorizing or re-entering the saved connection credentials. Installation and upgrades must preserve tracking records and the import journal.

## Support

Report bugs and request features through [GitHub Issues](https://github.com/felix-lorenz/timetracker-releases/issues). Include the app version, macOS version, steps to reproduce the problem, and relevant error messages. Remove personal work records, Jira details, email addresses, and all tokens from screenshots and logs before sharing them.

Time Tracker is an independent app and is not affiliated with or endorsed by Atlassian, Tempo, or Homebrew.
