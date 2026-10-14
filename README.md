# 🏎️ AI Racing League – Autonomous AI Driver

An autonomous AI driver for **TORCS** (The Open Race Car Simulator), written in **Python** for the **IBM AI Racing League**. The car drives the **Corkscrew** track on its own, using only the simulator's sensor data.

> **Team:** `<TEAM NAME>`
> **University:** `<UNIVERSITY NAME>`
> **Members:** `<NAME 1>`, `<NAME 2>`, ...

---

## 📂 Repository Files

| File | Description |
|------|-------------|
| `demonstration_video.mp4` | Demonstration video (~2 min 16 s): our AI driver racing on the Corkscrew track, followed by a screen recording scrolling through our IBM work |
| `snakeoil3_gym.py` | Python client that connects to TORCS, plus our driver logic in the `drive_example` function |
| `README.md` | Project documentation |

## 🧠 Our Approach

Our driver is a **rule-based controller**: at every simulation step it reads the car's sensors and decides steering, throttle, brake and gear. The main design goal was **finishing the race safely without hitting the walls**; lap time came second.

The logic is built from five parts:

1. **Reverse recovery** – if the car is moving backward, it engages reverse gear and steers to get back on track.
2. **Steering** – the car aligns with the road using the track angle, with a small capped correction towards the center of the track to avoid over-steering.
3. **Look-ahead corner detection** – the front track sensor (distance to the road edge straight ahead) and the road angle are combined into a "corner severity" value. The car then sets a **target speed before the corner**: up to 250 on straights and down to 95 in corners.
4. **Throttle and brake** – the car brakes progressively when it is faster than the target speed, and accelerates smoothly otherwise.
5. **Traction control and automatic gears** – throttle is reduced if the rear wheels spin faster than the front ones, and gears (1 to 6) are chosen from the current speed.

**Tuning:** we found the section of the lap where the car crashed (around 1:13 into the lap) and added a lower corner speed (65) for that part of the track. The minimum corner speed elsewhere was raised from 85 to 95 to improve lap time.

**Use of IBM Granite:** `<describe how you used Granite: brainstorming, code ideas, debugging...>`

## 🎥 Demonstration

`demonstration_video.mp4` shows the car completing the Corkscrew track with our controller, and also includes a screen recording (scrolling through the content) of the work we completed with IBM (`<IBM SkillsBuild courses / IBM Granite credential>`). `<Add a sentence about what to look for in the video, e.g. the corner at 1:13>`

## ⏱️ Results

| Metric | Value |
|--------|-------|
| Track | Corkscrew |
| Best lap time | `<MM:SS.ms>` |

## 🎓 IBM SkillsBuild

Our team completed the IBM SkillsBuild learning path, including the **IBM Granite** course. It helped us `<what you learned / how it helped>`.

## 🙌 Acknowledgements

- IBM SkillsBuild and the IBM AI Racing League
- The TORCS project
- `snakeoil3_gym.py` is based on the standard Python client for TORCS (SCR)
