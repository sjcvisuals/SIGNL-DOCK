# SIGNL Dock

Windows desktop application for configuring and flashing **SIGNL** controllers, managing layouts, Wi‑Fi profiles, and related tools.

## Requirements

- **Windows 10/11** (x64)
- **[.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)** (to build from source)

## Build and run (development)

```powershell
cd path\to\Dock
dotnet build
dotnet run
```

Or open `Dock.csproj` in Visual Studio and run with **Debug**.

## Windows installer (MSI)

From the repo root:

```powershell
.\Installer\build-installer.ps1
```

This script:

1. Publishes the app to **`%USERPROFILE%\Documents\SIGNL dock\<Version>\`** (see `<Version>` in `Dock.csproj`).
2. Builds the WiX MSI and copies **`DockInstaller.msi`** into that same folder.

**Distribution:** ship only **`DockInstaller.msi`**. The loose files in that folder are build staging; the MSI embeds the payload.

Visual Studio **Publish** (profile `Dock`) uses the same **`SignlDockPublishDir`** pattern from `Dock.csproj`.

## Online updates (manifests)

Dock reads small JSON files over HTTPS (no sign-in required):

| Purpose | Typical location (public repo) |
|--------|--------------------------------|
| **Controller firmware** (`manifest.json`) | [SIGNL-DOCK `manifest.json`](https://raw.githubusercontent.com/sjcvisuals/SIGNL-DOCK/refs/heads/main/manifest.json) |
| **Dock MSI** (`dock-manifest.json`) | [SIGNL-DOCK `dock-manifest.json`](https://raw.githubusercontent.com/sjcvisuals/SIGNL-DOCK/refs/heads/main/dock-manifest.json) |

Repo: **[github.com/sjcvisuals/SIGNL-DOCK](https://github.com/sjcvisuals/SIGNL-DOCK)** — hosts manifests (and optional firmware zip assets). URLs are defined in `MainWindow.xaml.cs` (`SignlManifestsGithubOwner` / `SignlManifestsGithubRepo`).

Firmware entries in the manifest can point at zip URLs on the same repo or elsewhere; each zip must unpack the three expected `*.ino.bin` / bootloader / partitions files for the selected folder name (for example `SIGNL_2.8.0`).

## Repository layout (high level)

| Path | Role |
|------|------|
| `Dock.csproj` | App version, publish directory, WPF app |
| `MainWindow.xaml(.cs)` | Main UI, firmware checks, Dock self-update |
| `Installer/` | WiX project (`DockInstaller.wixproj`), `Package.wxs`, `build-installer.ps1` |
| `Dependencies/` | Bundled Python + esptool for flashing |
| `Firmware/` | Optional bundled controller firmware `.bin` files |

## Changelog

See **[CHANGELOG.md](CHANGELOG.md)** for user-facing release notes.
