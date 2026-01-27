# AGENTS.md

## Overview
Reader is a Win32 (C++/MFC-style) desktop reader for TXT/EPUB/online sources. The core app is built from `Reader.sln` / `Reader/Reader.vcxproj` and targets Win32/x64 via Visual Studio 2019. This repo also ships docs and the default online book-source configuration.

## Quickstart
### Install prerequisites
- Windows + Visual Studio 2019 (C++ Desktop workload) with MSBuild/`devenv`.
- Optional: 7-Zip if you plan to run the packaging steps in `rebuild.bat`.

### Build / Run
- Open `Reader.sln` in Visual Studio and build the **Reader** project (Debug/Release, Win32/x64).
- Or use the batch script (requires a VS install path matching the script):
  - `rebuild.bat`

### Tests
- No automated test suite is present. Manual smoke tests are typically done by launching the built `Reader.exe` and opening sample TXT/EPUB files.

## Repo Map
- `Reader/` — C++ Win32 application sources, resources, and project file.
  - `Reader/Reader.cpp` / `Reader/Reader.h` — main application entry and window logic.
  - `Reader/*.rc` / `Reader/resource.h` — resources, menus, icons, strings.
  - `Reader/*Book*.{h,cpp}` — book formats and readers (TXT/EPUB/online, etc.).
  - `Reader/Online*` — online book fetching & UI.
- `bs.json` — default online book-source configuration.
- `doc/` — documentation (e.g., book-source rule docs).
- `rebuild.bat` — batch build + packaging automation.

## Common Commands
- Build via VS IDE: open `Reader.sln` and build.
- Batch build + package (Windows only):
  - `rebuild.bat`

## Conventions
- Formatting/Lint: no repository-wide formatter or linter is configured; follow existing style and line endings in touched files.
- Branching: follow the project’s default branch (`main`) unless a task specifies otherwise.
- Assets/resources: update both `.rc` files and `resource.h` if you add/rename resources.

## Troubleshooting
- **Build fails in `rebuild.bat`:** verify the VS install path in the script (`vsdevcmd` variable) and update it to your local Visual Studio location.
- **Missing output exe:** confirm the configuration/platform matches the script’s expectations (Win32 uses `Release/` or `Debug/` folders, x64 uses `x64/Release`).
- **Online sources not working:** `bs.json` sources change often; update from the repo’s latest `bs.json` or adjust rules per `doc/bs.md`.
