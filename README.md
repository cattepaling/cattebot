# Changes since the last Beat Saber launch

The installed live build is **CatteBot 0.9.7-6**.

- CatteBot records the exact saber-root and saber-tip pose applied each frame after movement limits.
- The trace labels the current motion phase and records speed, acceleration, and limiter activity. The session report includes the trace path, row count, and write-error count.
- The matched plugin and Core DLLs now include normalized beatmap timelines, explainable section measurements, versioned pre-map plan validation, and deterministic motion boundaries.
- Two-bone arm geometry now measures shoulder, elbow, forearm, hand, reach, and elbow-angle feasibility.
- Wrist-orientation and angular speed/acceleration constraints are included, and the live report now measures applied-pose reach clamps, elbow angles, and forearm-to-blade angle warnings without changing the applied saber pose.
- Continuous cubic motion phrases can carry velocity through neighboring targets, start and finish at rest, use adjustable tension, and rotate by the shortest path.
- Offline phrase diagnostics now report path length, sample spacing, peak speed, peak acceleration, and configured-limit violations, with CSV and SVG output.
- The phrase policy and new motion constraints are installed foundations; they do not yet replace the current live pass-first saber planner.

# What to test

1. Start Beat Saber and confirm the newest log says **CatteBot 0.9.7.6** is initializing.
2. Play any map, press **F9** to enable CatteBot, and finish or leave the song normally.
3. Open the newest CatteBot report and check that **Trace enabled** is True, **Applied-pose rows** is greater than zero, and **Trace write errors** is 0.
4. Check that the reported CatteBot_trajectory_trace_*.csv file exists.
5. In **ANATOMICAL FEASIBILITY TELEMETRY**, check that **Applied-pose samples** is greater than zero and **Telemetry errors** is 0. Keep the reach-clamp, elbow-angle, and forearm/blade-warning values for review.
6. Double-directional resets should visibly reverse toward neutral instead of continuing through a full 360-degree turn.
7. Closely stacked notes should be hit without the saber abandoning the shared swing too early.
8. Bomb avoidance should react only when the saber tip would intersect a bomb at the same time. Bombs beside the blade should not cause avoidable note misses.
9. Saber movement should not teleport, snap, or make obviously impossible speed or acceleration changes.
10. Note whether any miss happens immediately after a reset, during a stack, or because the saber moved away from a note to avoid a bomb.
11. Before the next feature, provide the newest CatteBot report, trajectory trace CSV, and Beat Saber log, plus the visual observations above.
