# Time Tracker

A native macOS time tracker with a weekly calendar and quick capture in the menu bar.

## Distribution status

The first public release is being prepared. No downloadable version or Homebrew cask is available yet.

This repository will provide product documentation, release notes, distribution archives, and support through GitHub Issues. The source repository is private.

## Features

- Track work by topic, project, and one locally maintained Jira issue per time entry.
- Start, switch, and stop timers from the main window or menu bar.
- Review and edit time in a weekly calendar, including entries that cross midnight.
- Keep tracking records locally, with atomic saves and a backup of the previous valid snapshot.
- Export completed records as a neutral CSV.
- Preview, export, and transfer worklogs through the optional Tempo Cloud connection, with a local journal to prevent duplicate in-app transfers.

The current interface is German. Local tracking does not require a Jira connection, Homebrew, or API tokens. Maintaining an issue locally does not create it in Jira.

The neutral CSV is **not a verified Tempo import format**. Tempo Cloud requires the user's own Jira and Tempo credentials and assigns worklogs to that user's account. Live Tempo transfer and access permissions remain acceptance checks; development validation uses mocked HTTP and isolated demo data. Required Tempo work attributes are not supported and block transfer.

## Planned requirements

- macOS 14 (Sonoma) or later
- Apple Silicon (arm64)
- Homebrew only for installation through the Homebrew cask; direct ZIP installation will not require Homebrew

The planned distribution uses Developer ID signing and Apple notarization. These checks must pass before a download is published. Runtime checks on macOS 14–26 and another Mac remain separate acceptance checks.

The Homebrew package will be distributed through [felix-lorenz/homebrew-tap](https://github.com/felix-lorenz/homebrew-tap). Installation instructions will be added with the first verified release.

## Data and credentials

Tracking records and the Tempo import journal are stored in `~/Library/Application Support/Time Tracker/`. Jira and Tempo tokens are stored in the macOS login Keychain. Back up the tracking file and import journal together; the journal records transfers that must not be repeated.

Replacing the development build with a Developer ID signed build may require reauthorizing or re-entering the saved connection credentials. Installation and upgrades must preserve tracking records and the import journal.

## Support

Report bugs and request features through [GitHub Issues](https://github.com/felix-lorenz/timetracker-releases/issues). Include the app version, macOS version, steps to reproduce the problem, and relevant error messages. Remove personal work records, Jira details, email addresses, and all tokens from screenshots and logs before sharing them.

Time Tracker is an independent app and is not affiliated with or endorsed by Atlassian, Tempo, or Homebrew.
