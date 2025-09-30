# TILLING Framework

**TILLING** is a structured prompt framework for guiding AI-generated images using a grid-based system. It allows creators to define elements in a scene with precise positions, weights, depth layers, and relationships. This repository provides the specification, examples, parsing tools, and visualization utilities to adopt TILLING in creative workflows.

---

## Table of Contents

* [Overview](#overview)
* [Core Concepts](#core-concepts)

  * [Grid System](#grid-system)
  * [Coordinates](#coordinates)
  * [Depth Layers](#depth-layers)
  * [Weights](#weights)
  * [Ranges and Links](#ranges-and-links)
* [Example Prompts](#example-prompts)
* [Repository Structure](#repository-structure)
* [Getting Started](#getting-started)
* [Roadmap](#roadmap)
* [License](#license)

---

## Overview

TILLING introduces a **visual grammar** for describing image layouts. Instead of freeform text prompts, it divides the canvas into a **grid (WxH)** where each cell (or group of cells) holds a description. This approach:

* Enforces **structured composition**
* Allows **precise placement** of objects
* Separates **foreground, midground, and background** layers
* Supports **importance weighting** and **motion vectors**

TILLING makes image generation more predictable, modular, and reproducible.

---

## Core Concepts

### Grid System

A TILLING grid is defined by `TILLING WxH`, where `W` = number of columns and `H` = number of rows.

Example: `TILLING 3x4` → 3 columns, 4 rows.

```
    1     2     3
A [A1]  [A2]  [A3]
B [B1]  [B2]  [B3]
C [C1]  [C2]  [C3]
D [D1]  [D2]  [D3]
```

### Coordinates

* Rows are labeled with **letters** (`A, B, C...`) from **top to bottom**.
* Columns are labeled with **numbers** (`1, 2, 3...`) from **left to right**.

Examples:

* `A1` → top-left cell
* `B2` → second row, second column
* `C1-C3` → entire row segment
* `B1-B3` → entire row B
* `A2→B2` → element spanning or moving from A2 to B2

### Depth Layers

* `FG` → Foreground (closest, most detailed)
* `MG` → Midground (middle)
* `BG` → Background (distant, less detail)

Default: `MG` if not specified.

### Weights

Importance is defined with `!n` where `n` is an integer ≥1.

* `!1` = default
* `!3` = very important, dominant visual

### Ranges and Links

* **Ranges**: `A1-A4` covers multiple adjacent cells.
* **Directional Links**: `B3→C3` describes orientation or motion from one cell to another.

---

## Example Prompts

### Example 1: 3x3 Grid

```
TILLING 3x3
STYLE: digital painting, twilight atmosphere
[A1!3]: Stormy water
[A2,3:BG]: Iceberg
[B2!2:FG]: Warrior
[C1-C3:BG]: Temple
```

**Interpretation**:

* A1: Stormy water (very important)
* A2, A3: Iceberg in background
* B2: Warrior in foreground, high importance
* Entire row C: Temple in background

### Example 2: 3x4 Grid

```
TILLING 3x4
STYLE: manga style, sunny holidays mood
[A1-A3:BG]: Blue sky
[A2:BG]: Airplane with “I love TILLING” written
[B2-B3:MG]: Ocean with small waves
[B2:MG]: Surfer with black board
[C1-C4:MG]: Detailed sandy beach
[C1-C4:FG]: People resting and playing
[C3]: Beach volleyball game
[D1-D3:FG]: Top of a wall, framing the scene
```

**Interpretation**:

* Top: Sky with airplane
* Middle: Ocean + surfer
* Lower mid: Beach with people (volleyball at C3)
* Bottom: Wall in the foreground

---

## Repository Structure

* `README.md` → project overview
* `SPEC.md` → complete syntax specification
* `examples/` → sample `.til` prompts and visual mockups
* `schema/` → JSON schema describing parsed format
* `parser/` → Python implementation of the TILLING parser
* `visualizer/` → mockup generator for grids
* `cli/` → command-line tools for validation and visualization
* `docs/` → diagrams, usage guides, design notes

---

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/tilling-spec.git
   cd tilling-spec
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Parse a sample prompt:

   ```bash
   python -m cli.tilling_cli validate examples/example_3x3.til
   ```

4. Visualize the layout:

   ```bash
   python -m cli.tilling_cli visualize examples/example_3x3.til --out preview.png
   ```

---

## Roadmap

* ✅ Initial parser and JSON schema
* 🔲 Full visualizer with depth-aware mockups
* 🔲 Export to layered PSD/PNG
* 🔲 Web-based editor with drag-and-drop grid building
* 🔲 Integration with AI image generation pipelines

---

## License

This project is licensed under the MIT License.

---
