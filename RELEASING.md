# Releasing RoastConsole Pilot

This public repo distributes **signed** builds; it does not contain source.

## Flow
1. **Build + sign** the installer in the private source repo's CI (or locally).
   - macOS ships via the Mac App Store, not here.
   - Windows: produce `RoastConsolePilot-Setup-<version>.exe`, signed with
     Azure Trusted Signing (see the Windows signing plan).
2. **Create the release shell** here — either:
   - Actions → **Publish Release** → *Run workflow* (enter the version), or
   - push a tag: `git tag v1.0.8 && git push origin v1.0.8`.
3. **Attach the signed installer** to that release:
   ```bash
   gh release upload v1.0.8 RoastConsolePilot-Setup-1.0.8.exe --repo farspeak-labs/RoastConsole-Pilot
   ```
   To automate step 3 from the private CI, add a PAT with `contents:write` on
   this repo as a secret there (e.g. `DIST_REPO_TOKEN`) and call `gh release upload`.

## Notes
- Early Windows builds should stay **pre-release** until signed-publisher
  SmartScreen reputation establishes.
- Public-repo Actions minutes are free, so this workflow costs nothing.
