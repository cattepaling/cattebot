# Changes since the last Beat Saber launch

The installed live build is **CatteBot 0.9.7-1**.

- Double-directional resets now use three stages: reverse the finished swing to neutral, move the hand while holding neutral, then wind up for the next note.
- Live saber-root movement now enforces the configured speed and acceleration limits. The previous 160 m/s diagnostic ceiling was replaced by the 16 m/s movement limit.

# What to test

1. Play a map that reliably creates same-colour double-directional resets and press **F9** to enable CatteBot.
2. Watch the transition between opposite-direction notes. Check whether the saber reverses to neutral, transfers, and winds up—or still makes a full 360-degree loop.
3. Watch for teleports, unnatural speed or acceleration, new misses, and loss of normal saber control.
4. After the song, provide the newest CatteBot report and Beat Saber log, plus a short description of what you saw.
