<!-- Core project info -->
[![Download](https://img.shields.io/badge/Download-latest-blue)](https://github.com/PHNexus/AppManager/releases/latest)
[![Release](https://img.shields.io/github/v/release/PHNexus/AppManager?semver)](https://github.com/PHNexus/AppManager/releases/latest)
[![License](https://img.shields.io/github/license/PHNexus/AppManager)](https://github.com/PHNexus/AppManager/blob/main/LICENSE)
[![AnyLinux](https://img.shields.io/badge/AnyLinux-compatible-green?logo=linux&logoColor=white)](https://pkgforge-dev.github.io/Anylinux-AppImages/)
![GTK 4](https://img.shields.io/badge/GTK-4-blue?logo=gtk)
![Vala](https://img.shields.io/badge/Vala-compiler-blue?logo=vala)
[![Copy of kem-a/AppManager](https://img.shields.io/badge/copy%20of-kem--a%2FAppManager-blue?logo=github)](https://github.com/kem-a/AppManager)

# <img width="48" height="48" alt="AppManager" src="https://github.com/user-attachments/assets/879952cc-d0b3-48c8-aa35-1132c7423fe0" /> AppManager

> **Note:** This is a fork of [kem-a/AppManager](https://github.com/kem-a/AppManager). All credit goes to [@kem-a](https://github.com/kem-a). I do not own the original project.

**AppManager** is a GTK/Libadwaita desktop utility written in **Vala** that makes installing and uninstalling AppImages on Linux painless. It supports both SquashFS and DwarFS AppImage formats, features a seamless background **auto-update** process, and leverages **zsync** delta updates for efficient bandwidth usage. Double-click any `.AppImage` to open a macOS-style drag-and-drop window — drag to install and AppManager will move the app, wire up desktop entries, and copy icons.

> **This AppImage bundles everything and should work on any Linux distro, including old and musl-based ones.**
>
> AppManager doesn't require FUSE to run, thanks to [uruntime](https://github.com/VHSgunzo/uruntime).

## Preview

<img width="1600" height="1237" alt="Screenshot" src="https://github.com/user-attachments/assets/acc7d1b8-6e07-4540-af6c-cf3167345252" />

## Features

- **Drag-and-drop installer** — macOS-style Applications install flow.
- **Smart install modes** — portable (move the AppImage) or extracted (unpack to `~/Applications/.installed/AppRun`), with manual override.
- **True isolated portable mode** — optionally creates `.home` and `.config` folders next to the AppImage for fully self-contained installs.
- **Side-by-side installs** — multiple copies/versions of the same app get numbered suffixes (`Bitwarden`, `Bitwarden 2`), each with their own desktop entries.
- **Desktop integration** — extracts the bundled `.desktop`, rewrites `Exec` and `Icon`, and stores it in `~/.local/share/applications`.
- **Simple uninstall** — right-click in the app drawer and choose *Move to Trash*, or delete from `~/Applications`.
- **One-click installs from the web** — registers the `x-scheme-handler/appimg` handler, so `appimg://install?url=…&sha256=…` links (e.g. from [AppHub](https://xlc-dev.github.io/apphub/)) download the AppImage over HTTPS, verify SHA-256, and hand it to the normal install flow.
- **Install registry + preferences** — main window lists installed apps, default mode, and cleanup behaviors, stored via GSettings.
- **Background app updates** — optional auto-update checks (daily/weekly/monthly) with notifications.
- **GitHub authentication** — optional personal access token to raise the API rate limit (60 → 5,000 req/h). Token stored in the system keyring when available, otherwise in an AES-256-GCM blob bound to the machine.

## Installation

### Download the AppImage

1. Go to [Releases](https://github.com/PHNexus/AppManager/releases)
2. Download `AppManager-3.8.0-anylinux-x86_64.AppImage`
3. Make it executable:
   ```bash
   chmod +x ~/Downloads/AppManager-3.8.0-anylinux-x86_64.AppImage
   ```
4. Install it (it installs itself):
   ```bash
   ~/Downloads/AppManager-3.8.0-anylinux-x86_64.AppImage install ~/Downloads/AppManager-3.8.0-anylinux-x86_64.AppImage
   ```

Done. The app will appear in your application menu (wofi, rofi, GNOME Activities, etc.).

## Usage

1. Launch **AppManager** from your application menu
2. Click **Import AppImages from folder**
3. Select the folder where your AppImages are stored
4. Done — the app will list and manage them for you

### CLI helpers

- Install an AppImage: `app-manager install /path/to/app.AppImage`
- Install side by side: `app-manager install --keep-both /path/to/app.AppImage`
- Uninstall by path or checksum: `app-manager uninstall /path/or/checksum`
- Update a single installed AppImage: `app-manager update /path/or/checksum`
- Update all installed AppImages: `app-manager --update-all`
- List available updates (no install): `app-manager --update-check`
- Check if installed: `app-manager --is-installed /path/to/app.AppImage`
- Run a background update check: `app-manager --background-update`
- Show version or help: `app-manager --version` / `app-manager --help`
- Open a web install link: `app-manager 'appimg://install?url=https://host/App.AppImage&sha256=<hex>'`

## Requirements

- Linux x86_64
- FUSE (for running AppImages)
  - **Arch**: `sudo pacman -S fuse2`
  - **Debian/Ubuntu**: `sudo apt install libfuse2`
  - **Fedora**: `sudo dnf install fuse`

## License

MIT — see [LICENSE](LICENSE). Original license belongs to [@kem-a](https://github.com/kem-a).
