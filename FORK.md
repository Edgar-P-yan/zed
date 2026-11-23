# Zed Personal

This fork tracks personal changes to Zed on `main`. Update this file whenever a
fork change is added, changed, or removed.

## Project title bar colors

- Right-click the project name in the title bar and choose **Change Project Color** to edit the color in the project's root settings.
- The setting is `project_title_bar_color` in the project's root `.zed/settings.json`. For example, `{"project_title_bar_color": "#3B82F6"}`.
- Zed blends the color with the current theme's title bar. In a multi-folder window, the tint follows the folder shown in the title bar. Clearing the setting restores the theme background.

## macOS build and profile

Run `script/build-zed-personal` from the checkout to build, locally sign, and
install the development app in your user Applications folder. It uses the
checkout's Rust toolchain, Xcode, CMake, and Python 3. Open the installed app
from Finder.

| Item | Location |
| --- | --- |
| Installed app bundle | `~/Applications/Zed Personal.app` |
| Personal app data | `~/Library/Application Support/Zed Personal` |
| Personal config | `~/Library/Application Support/Zed Personal/config` |
| User settings and keymap | `config/settings.json` and `config/keymap.json` inside the Personal data folder |
| Workspace and session database | `db/0-dev/db.sqlite` inside the Personal data folder |

The launcher passes the Personal data directory through `--user-data-dir` and
uses the existing macOS Keychain through `ZED_DEVELOPMENT_USE_KEYCHAIN=1`. macOS
can prompt for access to those entries.

## Import from regular Zed

Quit the Zed instances using both profiles, then run `script/import-zed-profile`.
It copies regular Zed's data from `~/Library/Application Support/Zed`, copies
`~/.config/zed` into the Personal profile's `config/` directory, and copies the
stable workspace database from `db/0-stable` into `db/0-dev`. An existing
Personal profile is moved to a timestamped backup before the new profile takes
its place. The script prints the backup path. The project folders themselves
stay at the paths stored in the workspace database.

Use `script/import-zed-profile --help` to see options for profile paths and
release channels. Keychain credentials and macOS preferences are managed by
macOS outside the copied profile.

## Synchronize with upstream

Fetch `upstream/main` and merge it into the fork's `main`. Use this file to
resolve conflicts and preserve or adapt the fork changes. Verify the title-bar
feature, the named build, and the profile import after synchronization. Update
this file for any resulting changes, then push `main` to `origin`.
