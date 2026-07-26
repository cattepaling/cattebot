# Changes since the last Beat Saber launch

The installed live build is **CatteBot 0.9.7-2**.

- CatteBot now records the exact saber-root and saber-tip pose applied each frame after movement limits.
- The trace labels the current motion phase and records speed, acceleration, and limiter activity. The session report includes the trace path, row count, and write-error count.

# What to test

1. Play any map, press **F9** to enable CatteBot, and finish or leave the song normally.
2. Open the newest CatteBot report and check that **Trace enabled** is True, **Applied-pose rows** is greater than zero, and **Trace write errors** is 0.
3. Check that the reported CatteBot_trajectory_trace_*.csv file exists.
4. Provide the newest CatteBot report, trajectory trace CSV, and Beat Saber log. Also note any unexpected gameplay change, because this update is intended to add diagnostics without changing saber behavior.
