# CatteBot

CatteBot is an experimental live Beat Saber AI focused on continuous, anatomically plausible saber motion that is difficult to distinguish from skilled human play.

Target environment: PCVR Beat Saber 1.39.1 with BSIPA 4.3.6.

## TL;DR — what to test now

The current installed test build is **CatteBot 0.9.7-1**.

1. Start Beat Saber 1.39.1 and play a map that reliably creates same-colour double-directional (DD) resets.
2. Press **F9** to enable CatteBot.
3. Watch the saber between the two opposite-direction notes. The candidate fix should visibly:
   - reverse the completed swing back to neutral;
   - move the hand while the saber stays neutral;
   - wind up for the next note.
4. Check whether it still performs a full 360-degree loop. That is the most important result to report.
5. Also note any missed stacked notes, bomb contacts, unnatural speed spikes, or loss of normal saber control.
6. After the song, provide the newest CatteBot report and Beat Saber log with a short description of what you saw.

Issue #1 is **not complete** until this behavior is confirmed in-game. The newer per-frame trajectory trace exists in source but is awaiting the next guarded deployment, so it is not part of the current 0.9.7-1 test.

## Current development status

The current development line is **CatteBot 0.9.7.x**. The manually installed gameplay candidate is **0.9.7-1** (Windows assembly/file version **0.9.7.1**). Newer source-only trajectory diagnostics are awaiting the next guarded deployment.

Current baseline features include:

- F9-controlled saber takeover and F11 emergency restoration;
- genuine Beat Saber saber collisions and native scoring;
- normalized note, bomb, wall, slider, and chain timelines;
- pass-first scoring arcs, adaptive timing, flow chains, parity, and same-colour grouped swings;
- time-aligned saber-tip-only bomb checks;
- context-aware idle-saber evacuation;
- directional contact calibration and native score telemetry;
- configured saber-position speed and acceleration enforcement;
- dependency-free Core motion, reset, safety, kinematic, and telemetry routines;
- offline CSV/SVG trajectory inspection;
- per-frame actual applied-pose trajectory capture in the current source.

Every existing capability is provisional and will continue to be improved.

## GitHub issue #1: resets/DD

The first candidate fix attempt for [issue #1](https://github.com/cattepaling/cattebot/issues/1) replaces the previous one-waypoint DD bridge with three distinct stages:

1. reverse the completed swing to neutral at the old grip pivot;
2. transfer the hand while holding the saber neutral;
3. wind up at the next grip pivot.

The deterministic signed-sweep regression proves that this candidate does not continue forward around the swing circle. It is still awaiting an in-game visual test and is **not considered completed**.

## Validation status

- Full Release solution build: passing with no errors.
- Deterministic Core regression suite: **42/42 passing**.
- Runtime-trace CSV round trip and offline SVG rendering: passing on a synthetic fixture.
- New 0.9.7.x in-game gameplay validation: pending.

Automated tests do not prove Unity collision behavior, visual human realism, or arbitrary-map reliability. Those require fresh Beat Saber runs and inspection of the generated logs, reports, score telemetry, and actual-pose trajectory traces.

## Safety and integrity

CatteBot must:

- use real saber collisions and native scoring;
- never manipulate score, combo, note state, health, leaderboard state, or physical headset tracking;
- restore normal saber control when disabled, on gameplay end, or on emergency stop;
- preserve user configuration and calibration;
- never replace installed DLLs or live configuration while Beat Saber is running.

## Development workflow

Before each roadmap feature, the issue tracker is scanned for new or updated actionable reports. One fix attempt is made per issue, then that issue waits for new tracker or in-game evidence before another attempt.

The repository issues page and the full roadmap are both completion gates. CatteBot is not complete while any roadmap feature remains unfinished, any visible issue remains unreviewed, or an attempted issue still lacks authoritative verification.

## Building

When source is present, the Release solution is built and tested with:

```powershell
dotnet build .\CatteBot.sln -c Release
dotnet test .\CatteBot.sln -c Release
```

Work-mode deployment is manual; no installer is required. Both `CatteBot.dll` and `CatteBot.Core.dll` must be deployed together, and only while Beat Saber is not running.
