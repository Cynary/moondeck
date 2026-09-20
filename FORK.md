# Cynary's MoonDeck build

1.12.2-cynary.1 is based on upstream main aebfbd6, with the existing optional
stop-host-game-on-local-exit feature retained. This feature requires the compatible
Buddy stopSteamApp command; the user's Windows host already has that build.
The settings key remains stopHostGameOnExit (schema 43), preserving existing users.
Upstream PR #179 is still open; do not assume its differently named closeHostAppOnExit
setting or API is interchangeable with this fork.

Upstream's process-cleanup race handling replaces our earlier equivalent utils.py
change. Keep the upstream runner lifecycle and secondary-cursor fixes. The frontend
beingKilled guard remains necessary here to prevent our TerminateApp hook from
intercepting internal cleanup, including suspend cleanup.

Decky's ordinary MoonDeck store update replaces this custom build. Freeze updates
for MoonDeck in Decky Settings → Plugins. This is Decky's supported per-plugin
setting (frozenPlugins), not a fabricated high version number. It excludes MoonDeck
from store update checks and clears pending update notices while leaving other
plugins alone. Manual unfreeze/reinstallation can replace the fork.

Maintain the fork by rebasing onto upstream main, dropping equivalent changes,
then running build/lint, focused exit/settings tests and live host launch/exit tests.
Do not merge upstream's future exit API without coordinating Buddy compatibility
and settings migration. Work in a new branch; preserve old deployed releases.

Rebase, conflict resolution and validation performed with Codex.

1.12.2-cynary.2 adds Runner → General → “Pause splash rendering when
unfocused”. It defaults to off and takes effect on the next launch. Enable it
if the background splash causes extra Gamescope refreshes during VRR streaming.
Settings migrate to schema 44 without changing the host-exit preference.
Upstream review: https://github.com/FrogTheFrog/moondeck/pull/183.
