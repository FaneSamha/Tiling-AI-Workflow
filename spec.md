# TILING Specification (SPEC.md)

This document defines the formal syntax and semantics of the **TILING** system for grid-based prompt design.

---

## 1. Grid Definition

A TILING prompt starts with a grid size declaration:

```
TILING <W>x<H>
```

* `<W>` → number of columns (1..N)
* `<H>` → number of rows (1..N)

Rows are labeled **A, B, C…** (top to bottom).
Columns are labeled **1, 2, 3…** (left to right).

### Example

```
TILING 3x4
```

Represents:

```
    1     2     3
A [A1]  [A2]  [A3]
B [B1]  [B2]  [B3]
C [C1]  [C2]  [C3]
D [D1]  [D2]  [D3]
```

---

## 2. Global Style

The `STYLE` line defines global aesthetic and mood for the scene.

```
STYLE: <description>
```

Example:

```
STYLE: digital painting, twilight mood
```

---

## 3. Cell Annotations

Each element is described by a coordinate or range, followed by optional modifiers, then a description.

### Syntax

```
[<coords>[!<weight>][:<depth>]]: <description>
```

* `<coords>` → cell(s) targeted (e.g., `A1`, `A1-A3`, `B2,C3`)
* `!<weight>` → optional weight/importance (default `!1`)
* `:<depth>` → optional depth indicator

  * `FG` = Foreground
  * `MG` = Midground (default)
  * `BG` = Background
* `<description>` → freeform text describing the visual element

### Examples

```
[A1!3:BG]: Red stormy clouds
[B2:FG]: Warrior with a sword
[C1-C3]: Temple ruins
```

---

## 4. Coordinate Ranges

* Continuous ranges: `A1-A3` → covers cells `A1`, `A2`, `A3`
* Multiple cells: `B1,B3` → applies to `B1` and `B3`
* Whole row: `C1-C4` → applies across row C
* Whole column: `A1-D1` → applies down column 1

---

## 5. Links & Motion

Arrows (`→`) define direction or relation between cells.

```
[B3→C3:MG]: Black dragon in motion
```

Interpretation: The dragon spans or moves from cell B3 toward C3 in midground.

---

## 6. Formal Grammar (BNF-style)

```
<tiling>       ::= "TILING" <int> "x" <int> "\n" <style> <elements>
<style>         ::= "STYLE:" <text> "\n"
<elements>      ::= <element>+

<element>       ::= "[" <coords> <weight>? <depth>? "]:" <text> "\n"
<coords>        ::= <coord> ("," <coord>)* | <coord_range>
<coord_range>   ::= <coord> "-" <coord> | <coord> "→" <coord>
<coord>         ::= <row><col>
<row>           ::= "A" | "B" | "C" | ...
<col>           ::= <digit>+

<weight>        ::= "!" <int>
<depth>         ::= ":FG" | ":MG" | ":BG"

<text>          ::= .+
```

---

## 7. Example Prompt

```
TILING 3x3
STYLE: digital painting, twilight atmosphere
[A1!3]: Stormy water
[A2,3:BG]: Iceberg
[B2!2:FG]: Warrior
[C1-C3:BG]: Temple
```

---

## 8. Reserved Keywords

* `TILING`
* `STYLE`
* `FG`, `MG`, `BG`
* `!<n>` (weight)
* Symbols: `[] : , - →`

---

## 9. Notes

* Default depth = `MG`
* Default weight = `!1`
* Whitespace is ignored around separators
* Descriptions are freeform and not parsed semantically

---

## 10. Future Extensions

* Support for perspective scaling (e.g., closer vs distant objects)
* Grouping shorthand (named sets of coordinates)
* Conditional elements (optional render layers)

---
