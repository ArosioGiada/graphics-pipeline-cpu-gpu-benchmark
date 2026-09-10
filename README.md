# Graphics Pipeline: CPU vs GPU Benchmark

Technical report analyzing CPU vs GPU performance when applying a multi-step image
transformation pipeline, built and executed using the Unity Graphics Pipeline Simulator.

## Overview

A 4-step image transformation pipeline (Colorify, Kernel/Emboss, Replace Colour, Brightness)
was designed to convert a 4K artwork into an antique bronze relief effect. The identical
pipeline was then executed on both CPU and GPU, across HD (1280×720) and 4K (3840×2160)
resolutions, to measure and compare execution time.

## What this demonstrates

- Understanding of the computer graphics pipeline and how CPU vs GPU architecture affects
  performance (sequential vs parallel processing)
- Quantitative benchmarking methodology (5 runs per configuration, averaged results)
- Data analysis and visualization (execution time tables and comparison graphs)
- Debugging a visual artifact (red fringing) by identifying and correcting pipeline step order
- Technical writing with APA-referenced sources

## Pipeline steps

1. **Colorify** (#FF7700) — recolors every pixel based on its original intensity
2. **Kernel — Emboss** — recalculates each pixel from its 3×3 neighborhood to create a relief/engraved effect
3. **Replace Colour** — replaces pixels within a tolerance range to simulate metallic highlights
4. **Brightness** (-5) — deepens shadows for a more realistic aged-metal look

## Key results

| Resolution | CPU Mean Total (ms) | GPU Mean Total (ms) |
|------------|---------------------|----------------------|
| HD         | 164.26              | 45.88                |
| 4K         | 891.44              | 150.46               |

The GPU consistently outperformed the CPU, with the gap widening at higher resolution —
most notably for the Kernel step, where the CPU/GPU performance gap grew from ~7.5x (HD)
to ~17x (4K), reflecting how well pixel-neighborhood operations parallelize on GPU hardware.
Simpler operations like Brightness benefited far less from GPU parallelization due to fixed
setup overhead.

## Files

- [`Interactive_Theory_Exploration.pdf`](./Interactive_Theory_Exploration.pdf) — full report with methodology, all pipeline step outputs, benchmark tables, graphs, and reflection

## Tools used

Unity Graphics Pipeline Simulator

> This was completed as part of ICG202 Introduction to Computer Graphics (Torrens University
Australia).
