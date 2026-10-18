# 🏎️ AI Racing League – Autonomous AI Driver (TORCS)

An autonomous driving client for the **TORCS** racing simulator, built on the competition's `snakeoil3_gym.py` and tested on the **Corkscrew** track, for the **IBM AI Racing League**.

> **Author:** Youssef Jakoum (solo participant)
> **University / School:** `<UNIVERSITY NAME>`

---

## 🎯 Problem

The original driving logic had no real speed control and no braking, so the car got stuck on the track and crashed into the walls. The goal was to make the car **complete the race without crashing**, while keeping the **lap time as low as possible**.

## 📂 Repository Files

| File | Description |
|------|-------------|
| `snakeoil3_gym.py` | Python client for TORCS with my modified driving logic (`drive_example` function) |
| `demonstration_vid.mp4` | Demonstration video (~2 min 16 s): the car driving the Corkscrew track |
| `ibmbob_env.mp4` | Short video (~45 s): TORCS setup, running the client, and my conversation with IBM Bob |
| `README.md` | Project documentation |

## 🔧 Enhancements

**First iteration (done with IBM Bob)**

- **Corner-aware speed control:** the target speed varies with the steering input, so the car slows down before tight corners instead of hitting the walls.
- **Proportional braking:** the original code had no braking at all. I added brake force proportional to how far the car is above its target speed, which removed the stuck-and-crash problem.
- **Steering stabilization:** the steering gain was reduced (from 15 to 10) to limit oscillation in the tight S-section, and the track-position centering was strengthened (from 0.10 to 0.35) to keep the car away from the walls.

**Final version (current `snakeoil3_gym.py`)**

- **Look-ahead corner detection:** the straight-ahead track sensor and the road angle are combined into a "corner severity" value, which sets the target speed *before* the corner (up to 250 on straights, down to 95 in corners).
- **Dangerous-corner override:** a lower minimum speed (65) is used on the section that caused a crash around 1:13 into the lap.
- **Capped centering correction:** the track-position correction is limited to avoid over-steering.
- **Reverse recovery:** if the car moves backward, it engages reverse and steers back onto the track.
- **Traction control and automatic gears:** throttle is cut when the rear wheels spin faster than the front wheels, and gears 1 to 6 are selected from the current speed.

## 🤖 How I Used IBM Bob

I used **IBM Bob** (free trial version) as a coding assistant during development, to:

1. **Compare** the original and modified versions of the driving code and identify exactly what changed, and its effect on speed and stability.
2. **Analyze** which parameters affect crashes on this specific track: steering gain, track-position centering, minimum corner speed and the braking ramp.
3. **Apply and tune** these changes, and **create backup versions** of the code between iterations.

The conversation with IBM Bob (task list, tuning steps and my questions when the lap time got worse) is shown in `ibmbob_env.mp4`.

## ⏱️ Results

| Metric | Value |
|--------|-------|
| Track | Corkscrew |
| Race completed | Yes, no crash in the demonstration video |
| Best lap time | `<1:48>` |

## 🙌 Acknowledgements

- IBM SkillsBuild and the IBM AI Racing League
- IBM Bob
- The TORCS project; `snakeoil3_gym.py` is based on the standard Python client for TORCS (SCR)
