# Tiling-AI-Workflow

A specification and tooling project for the TILLING system — a structured way to describe image compositions using grids, weights, depths, and visual elements.

What is TILLING?

TILLING is a prompt format designed to map visual elements onto a grid (e.g., 3x3, 4x4, 5x5). Rows are labeled with letters (A, B, C...) and columns with numbers (1, 2, 3...). Each cell (or group of cells) can contain a description, weight, depth, and even directional links.

Example:

TILLING 3x3
STYLE: digital painting, twilight atmosphere
[A1!3]: Stormy water
[A2,3:BG]: Iceberg
[B2!2:FG]: Warrior
[C1-C3:BG]: Temple

This describes:

Stormy water in A1, very important (!3)

An iceberg in the background across A2 and A3

A warrior in the foreground at B2, high importance (!2)

A temple across the entire C row, background layer

Features

Grid-based composition — define elements precisely in a WxH grid

Weights (!2, !3) — control visual importance

Depth (FG, MG, BG) — set foreground, midground, background

Links and directions — span multiple cells or indicate movement (e.g., A1→B2)

Style — global setting for mood, technique, or aesthetic

Repository Structure (draft)

README.md — project overview (this file)

SPEC.md — formal syntax specification

examples/ — sample .til prompts and mockups

schema/ — JSON schema describing parsed format

parser/ — Python implementation of a TILLING parser

visualizer/ — grid visualizer for prompts

cli/ — small CLI for validation and visualization

docs/ — additional notes, diagrams, conventions

Getting Started

Clone the repository

Install dependencies (pip install -r requirements.txt)

Try parsing an example:

python -m cli.tilling_cli validate examples/example_3x3.til

Visualize the layout:

python -m cli.tilling_cli visualize examples/example_3x3.til --out preview.png
Roadmap

Complete parser with robust error handling

Visualization with layered previews (FG/MG/BG)

Export options (JSON, layered PNG)

Web-based editor for interactive prompt creation

License

MIT License. Contributions welcome.
