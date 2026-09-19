# 1.12.2-cynary.1 validation — 2026-09-19

Rebased the three custom commits onto upstream aebfbd6 (1.12.2).
Upstream PR #179 remains open; the former custom PR #176 is closed, unmerged.
Kept upstream utils.py cleanup handling, which already handles disappeared
processes. Retained the frontend internal-cleanup guard required by our exit hook.
No Windows Buddy executable or API change was made.

Codex performed the rebase, build, automated checks, deployment and live test.

Passed: frozen-lockfile install, Rollup build, frontend ESLint, diff whitespace,
settings default/migration/persistence tests, frontend exit routing/failure/race
checks, backend host-exit confirmation, and live process-cleanup tests.

Package contains new frontend/backend sources and pinned SSL submodule. Python
requirements did not change; retained the previously working K17 external packages.
All 647 installed files matched the built package SHA256 manifest.

K17 Decky UI state showed 1.12.2-cynary.1, MoonDeck frozen and no pending updates.
Freeze persisted across Decky restart; explicit checkPluginUpdates also returned
no update. Other plugins were not frozen. Existing settings/host pairing and eight
non-Steam shortcuts were retained.

Native Steam test: launched Overcooked! 2 through MoonDeck frontend. Passed launch
stability wait. Invoking Steam's local TerminateApp API at 15:47:15 sent the host
stop request. Windows reported the game Stopped around 15:47:18; Moonlight closed
gracefully and host Steam remained running. The expected TERMINATED runner result
on explicit local exit is not classified as a failure.

This is a launch/exit smoke test, not new gameplay, physical-controller, TV VRR,
suspend/resume or launcher-specific regression coverage. Windows launcher support
remains provided by the user's existing private Buddy build. No upstream comment
or PR was submitted. The image release was not modified.

Previous K17 plugin and settings: ~/k17-option1/moondeck-before-1.12.2/.
