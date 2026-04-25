# OpenCode Agent Instructions

## Repository Overview
- This is a [Scoop](https://scoop.sh) bucket containing Windows application manifests (`.json` files) in the `bucket/` directory.
- The `autoupdate` and `checkver` fields in manifests are used by GitHub Actions (`excavator`) to automatically update application versions.

## Commands & Workflow
All commands are PowerShell scripts located in `bin/` and require Scoop to be installed on the system (they use `$env:SCOOP_HOME`). Run them from the repository root:

- **Format Manifests:** `.\bin\formatjson.ps1 <app>` or `.\bin\formatjson.ps1 *` (Always run this after editing any JSON manifest to maintain styling conventions).
- **Run Tests:** `.\bin\test.ps1` (Validates manifests against the Scoop schema using Pester).
- **Check/Update Versions:** `.\bin\checkver.ps1 <app>` or `.\bin\checkver.ps1 * -Update` to check for and apply updates.
- **Update Hashes:** `.\bin\checkhashes.ps1 <app>` to automatically download the installer and update the manifest's hash.

## Quirks & Rules
- Use PowerShell (`powershell` or `pwsh`) to run the scripts.
- Avoid manually editing version strings or hashes if the `checkver` and `autoupdate` blocks are properly configured. Rely on `checkver.ps1` and `checkhashes.ps1` instead.
- Manifests must strictly adhere to Scoop's JSON schema and formatting. Always test changes with `test.ps1` before committing.
