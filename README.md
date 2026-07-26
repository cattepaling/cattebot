# Changes since the last Beat Saber launch

The installed live build is **CatteBot 0.9.7-23**.

- CatteBot records the exact saber-root and saber-tip pose applied each frame after movement limits.
- The trace labels the current motion phase and records speed, acceleration, and limiter activity. The session report includes the trace path, row count, and write-error count.
- The matched plugin and Core DLLs now include normalized beatmap timelines, explainable section measurements, versioned pre-map plan validation, and deterministic motion boundaries.
- Two-bone arm geometry now measures shoulder, elbow, forearm, hand, reach, and elbow-angle feasibility.
- Wrist-orientation and angular speed/acceleration constraints are included, and the live report now measures applied-pose reach clamps, elbow angles, and forearm-to-blade angle warnings without changing the applied saber pose.
- Continuous cubic motion phrases can carry velocity through neighboring targets, start and finish at rest, use adjustable tension, and rotate by the shortest path.
- Offline phrase diagnostics now report path length, sample spacing, peak speed, peak acceleration, and configured-limit violations, with CSV and SVG output.
- The installed Core now recognizes explainable Loloppe, Paul, and Wide-Paul occurrences from timing, hand, cut direction, and spatial geometry.
- The installed Core now also recognizes regular same-hand metronome runs while excluding irregular timing, very-fast vibro-like alternation, and large spatial jumps.
- Recognized Loloppe, Paul, Wide-Paul, and metronome occurrences now map to explicit shared-cut, continuous-sweep, wide-sweep, or alternating-pendulum motion intents.
- The installed Core now recognizes regular same-hand directionless-note paths and separates strongly turning technical sliders while excluding arrow notes, native slider objects, repeated-position dots, irregular timing, and large jumps.
- Dot paths and technical sliders now map to explicit continuous-waypoint or curved-technical-sweep motion intents.
- The installed Core now recognizes exact two-note opposite-colour simultaneous pairs and broad simultaneous dot walls while excluding same-colour pairs, offset notes, dense arrow chords, compact dot clusters, arrow walls, and native slider groups.
- Mixed-colour pairs and dot walls now map to coordinated dual-cut or coordinated wall-sweep motion intents.
- Normalized events now support stable linked-object identity. Complete native slider head/tail groups can be recognized as arcs, and complete burst heads plus ordered link elements can be recognized as chains; unlinked, partial, duplicated, mixed, reversed, same-beat arc, and range-clipped groups are rejected.
- Linked arcs and chains now map to guided follow-through or ordered continuous-chain motion intents.
- The installed Core now recognizes sustained regular alternating streams, separates compact very-fast directional vibro, recognizes rapid large-step same-hand jumps, and marks fixed-window dense scoring-head sections without counting burst-chain elements as extra notes.
- Streams, vibro, jumps, and dense sections now map to alternating-flow, compact-oscillation, rapid-transfer, or dense-phrase motion intents.
- The installed Core now recognizes same-hand body-centerline crossover transitions and exact simultaneous crossed-hand targets, plus bounded one-direction wrist rolls and explicit high-turn wrist-reset requirements.
- Palm-up is installed only as a heuristic candidate pending replay-pose calibration; crossover, palm-up, wrist-roll, and wrist-reset labels map to cross-body, calibrated grip-roll, progressive-roll, or bounded-unwind motion intents.
- Loloppe, Paul, Wide-Paul, and metronome intents can now construct offline blade-contact trajectories with pre-swing, timed-contact, and follow-through waypoints. Loloppe members share one contact center; all results are marked calibration-required and not live-ready.
- Dot-path and technical-slider intents now construct offline contact trajectories whose direction comes from measured spatial tangents. They preserve every timed contact, reject arrows and zero-motion tangents, and remain calibration-required and not live-ready.
- Directional mixed-colour pairs now produce synchronized offline left/right contact trajectories. Both sabers share one averaged contact time while retaining independent positions, directions, pre-swings, and follow-throughs; dot members use the separate context-candidate boundary below. The result remains calibration-required and not live-ready.
- Directionless mixed-colour pairs now produce bounded offline per-saber direction candidates from the nearest same-hand notes: centered, incoming, and outgoing evidence is retained, near-parallel directions are merged, and every left/right combination remains available. Missing, distant, or zero-motion context is rejected; all candidates require replay/context selection and calibration and remain not live-ready.
- Same-hand dot walls now produce explicit low-to-high and high-to-low offline sweep candidates along their measured dominant axis. Neither direction is selected: both require replay-based direction selection and saber calibration and remain not live-ready.
- Mixed-hand dot walls now produce all four offline combinations of independently low-to-high or high-to-low left/right saber sweeps. A one-contact hand keeps both global-axis direction candidates; all four combinations require replay-based selection and calibration and remain not live-ready.
- Complete directional native arcs and burst-slider chains now produce offline linked blade paths. An arc has one scoring head contact plus non-scoring tail guidance; a chain keeps every head/link contact, preserves strict times, and uses a recorded bounded spread only for ties. Directionless heads and zero-path tangents are rejected; results require calibration and remain not live-ready.
- Recognized streams and vibro now produce coordinated offline left/right contact trajectories that preserve every source time and saber owner. Arrows retain their directions; stream dots use only same-hand spatial tangents, and vibro rejects dots. Both paths require calibration and remain not live-ready.
- Recognized rapid same-hand jumps now produce offline single-saber contact trajectories that preserve every source target and time. Arrows retain their directions and dots use same-hand tangents; cross-hand, native, simultaneous, missing, and zero-tangent inputs are rejected. Results require calibration and remain not live-ready.
- Recognized dense sections now produce offline independent per-saber scoring-head trajectories that preserve every ordinary-note, slider-head, and burst-slider-head target and source time. Opposite-hand simultaneous contacts remain independent; same-saber simultaneous heads, directionless heads, non-head native elements, missing events, and inconsistent hand metadata are rejected. Results require calibration and remain not live-ready.
- The phrase policy, pattern recognition, and new motion constraints are installed foundations; they do not yet replace the current live pass-first saber planner.

# What to test

1. Start Beat Saber and confirm the newest log says **CatteBot 0.9.7.23** is initializing.
2. Play any map, press **F9** to enable CatteBot, and finish or leave the song normally.
3. Open the newest CatteBot report and check that **Trace enabled** is True, **Applied-pose rows** is greater than zero, and **Trace write errors** is 0.
4. Check that the reported CatteBot_trajectory_trace_*.csv file exists.
5. In **ANATOMICAL FEASIBILITY TELEMETRY**, check that **Applied-pose samples** is greater than zero and **Telemetry errors** is 0. Keep the reach-clamp, elbow-angle, and forearm/blade-warning values for review.
6. Double-directional resets should visibly reverse toward neutral instead of continuing through a full 360-degree turn.
7. Closely stacked notes should be hit without the saber abandoning the shared swing too early.
8. Bomb avoidance should react only when the saber tip would intersect a bomb at the same time. Bombs beside the blade should not cause avoidable note misses.
9. Saber movement should not teleport, snap, or make obviously impossible speed or acceleration changes.
10. Note whether any miss happens immediately after a reset, during a stack, or because the saber moved away from a note to avoid a bomb.
11. Pattern recognition and motion-intent selection, including dot paths, technical sliders, mixed-colour pairs, dot walls, linked arcs, chains, streams, vibro, jumps, dense sections, crossovers, palm-up candidates, wrist rolls, and wrist resets, are not connected to live swing generation yet. The new offline Loloppe, Paul, Wide-Paul, metronome, dot-path, technical-slider, directional and directionless mixed-colour-pair, same-hand and mixed-hand dot-wall candidate, native arc and chain, stream and vibro, jump, and dense-section trajectories are also not connected. Report any new behavior change as a regression.
12. Before the next feature, provide the newest CatteBot report, trajectory trace CSV, and Beat Saber log, plus the visual observations above.
