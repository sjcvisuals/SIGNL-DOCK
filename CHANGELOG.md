# Changelog

All notable user-visible changes for **SIGNL Dock** are listed here. For full commit history, use Git.

---

## Recent updates (May 2026)

### Firmware and “available versions”

- **Online firmware list** — Dock loads controller firmware metadata from a public **`manifest.json`** (hosted on the [SIGNL-DOCK](https://github.com/sjcvisuals/SIGNL-DOCK) repo). New versions can appear in the app **without reinstalling Dock**, as long as the manifest (and zip URLs) are updated.
- **Download-only versions at the top** — Versions offered only as an online download (shown with “**(download)**”) are listed **above** versions that exist only as files bundled with Dock, so the newest online builds are easy to spot.
- **Refresh control** — A small **refresh** icon next to “Select Version:” checks the server again for the latest manifest. Status text reports success or a clear failure if the network or server is unreachable.
- **More reliable fetching** — Longer timeout on manual refresh, cache-bypass query on refresh, no-cache HTTP headers where applicable, and safer UI threading so refresh does not hang the window.
- **Fallback** — If the manifest file cannot be loaded from any of the tried URLs, Dock can still try to build a firmware list from **GitHub Releases** on the firmware repo (when the API and assets are public and match expected zip naming).

### Dock self-update (installer)

- **Hosted manifest** — Dock checks **`dock-manifest.json`** on the same public manifests repo for a newer **MSI** and can show an in-app update prompt when your published version is newer than the running app.

### Build and installer (for maintainers / power users)

- **Publish output location** — Release publish and the installer script write under **`Documents\SIGNL dock\<Version>\`** (version comes from `Dock.csproj`).
- **Single file to ship** — After `Installer\build-installer.ps1`, distribute **`DockInstaller.msi`** from that folder; end users do not need the loose published files to install.
- **Installer build safety** — The script stops if WiX fails so an old MSI is not copied over a failed build.

---

## Earlier releases

Older changes were not tracked in this file. From here on, add a dated section when you ship a new **`<Version>`** in `Dock.csproj` and update manifests accordingly.
