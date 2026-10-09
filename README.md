# CI-Tests

Smoke tests for the Slicer → unlayered3d.com publish pipeline that don't need a real OrcaSlicer build.

`Dummy publish` (Actions → Run workflow) makes small fake installers for Windows, macOS and Linux and
publishes them with `scripts/publish-software.mjs` — the same script the Slicer workflows use (copied
from the site repo's `scripts/`). It then re-runs the publish to check that a re-run does nothing.

Inputs:
- **site** – the site to publish to. Point it at a local dev server (through a tunnel) or a test
  deployment. **Do not point the stable channel at https://unlayered3d.com:** a stable publish replaces
  the live /software download and the update every installed Slicer is offered.
- **channel** – which secret to use: `SOFTWARE_PUBLISH_TOKEN_TEST_STABLE` or `SOFTWARE_PUBLISH_TOKEN_TEST_DEV`.
  The token decides the channel on the site; nothing else does.
- **size_mb** – fake installer size. Anything over 8 MB uses a multipart upload, as real installers do.
