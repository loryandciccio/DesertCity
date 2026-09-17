# DesertCity

**Cinematic Environment & Character Animation Project — Unreal Engine 5.5.4**

**Author:** Lorenzo Cozzolino  
**Course:** Computer Graphics — Roma Tre University

## Overview

DesertCity is a cinematic real-time graphics project built in Unreal Engine 5.5.4. The project presents a science-fiction desert city across three distinct moments of the day — **morning, sunset and night** — with dedicated lighting, atmosphere, camera work and character staging for each sequence.

The final version extends the base environment into an inhabited cinematic scene, combining environment lighting, post-processing, Sequencer-based camera direction, animated characters, spline-driven movement, animation retargeting and Movie Render Queue output.

## Final Cinematic Structure

The project contains three final 40-second sequences at 30 fps:

| Sequence | Purpose |
|---|---|
| `LS_Showcase_Mattina_ManualPaths` | Morning sequence with the highest level of pedestrian activity |
| `LS_Showcase_Tramonto_ManualPaths` | Sunset sequence with warmer lighting and reduced crowd density |
| `LS_Showcase_Notte_ManualPaths` | Night sequence with sparse population, artificial lighting and creature/combat staging |

Each sequence is organized through Unreal Sequencer using multiple Cine Camera Actors, camera cuts, character animation tracks and path tracks.

## Main Technical Work

### Environment and Lighting

- Three dedicated visual states: morning, sunset and night.
- Directional Light tuning for time-of-day changes and long desert shadows.
- `SkyAtmosphere`, `SkyLight`, `HDRIBackdrop` and `Exponential Height Fog` for environmental depth.
- Local volumetric fog used to shape specific streets and architectural areas.
- Rect Lights and localized colored lighting for the night sequence.
- Post Process Volume used to maintain a consistent cinematic look.

### Cinematic Direction

- Camera animation and shot composition created with Unreal Sequencer.
- Five-shot structure used to present streets, architecture and populated areas from different viewpoints.
- Separate camera and lighting direction for each time-of-day sequence.
- Final output prepared through Unreal Engine's Movie Render Queue.

### Character Population and Motion

- Multiple Paragon characters are used as inhabitants of the city, with varied placement, timing and movement.
- Walking animations were adapted to different character skeletons through Unreal Engine IK Rig and IK Retargeter workflows.
- Character movement is directed through Sequencer rather than runtime gameplay logic, keeping the cinematic deterministic and reproducible.
- Walk, stop, idle and action sections are combined directly in Sequencer to control pacing and staging.

## Spline-Based NPC Path System

A custom Blueprint path actor was created to make pedestrian trajectories easy to author directly in the level viewport.

The path workflow uses:

- A reusable Actor Blueprint containing a `Spline Component`.
- Sequencer Path tracks to move characters along manually directed trajectories.
- Normalized path progression from 0 to 1 for precise timing control.
- Intermediate spline points to follow streets, stairs and uneven terrain.
- An editor-callable `SnapToGround` utility that performs downward traces and aligns spline control points with the environment surface.

This approach provides direct cinematic control over where each character moves, when movement begins and ends, and which animation is active at each stage.

## Night Sequence

The night version changes the visual and narrative tone of the city. Population density is reduced, practical lighting becomes more prominent, and creature encounters introduce a short action beat. Character reactions and combat-oriented animation sections are staged in Sequencer together with the path-based movement system.

## Repository Structure

```text
DesertCity.uproject
Content/Cinematics/                  Final and development Level Sequences
Content/Scifi_desert_city/Level/     Environment levels
Content/Scifi_desert_city/Lorenzo/   Custom animations, materials, paths and retargeting assets
Config/                              Unreal Engine project configuration
```

## Requirements

- Unreal Engine **5.5.4**
- Git with **Git LFS** support
- Enabled Unreal plugins used by the project include HDRI Backdrop and Movie Render Pipeline.

The repository stores Unreal binary assets through Git LFS. Before cloning the project, make sure Git LFS is installed and initialized.

```bash
git lfs install
git clone https://github.com/loryandciccio/DesertCity.git
cd DesertCity
git lfs pull
```

Then open `DesertCity.uproject` with Unreal Engine 5.5.4.

For the final cinematic work, use the three `LS_Showcase_*_ManualPaths` sequences listed above. Other sequences included in the project are development or validation assets retained as part of the project history.

## Rendering

The cinematic sequences are prepared for rendering through Movie Render Queue. The final morning, sunset and night sequences are designed for **1920×1080 output at 30 fps**, with a duration of approximately **40 seconds each**.

## Third-Party Assets

| Asset | Author / Publisher | Usage |
|---|---|---|
| Science Fiction Desert City Kit | LAYA DESIGN | Base environment and architecture |
| Paragon character assets | Epic Games | Character meshes, materials and source animations |

Third-party assets remain the property of their respective authors and publishers and are used here as part of an academic Computer Graphics project.

## Author

**Lorenzo Cozzolino**  
Computer Graphics Project  
Roma Tre University
