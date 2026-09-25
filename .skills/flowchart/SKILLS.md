---
name: ASCII Diagrams - Flowchart
description: Create and edit ASCII-art diagrams
version: 0.1
author: michal.borejszo@pm.me
tags: [visualization, diagram, flowchart, markdown]
requires: []
---

# ASCII Diagrams Skill

This skill provides capabilities for creating and editing ASCII-art style flowcharts.

## Capabilities

- Create new flowcharts from user input
- Edit existing flowcharts to user requirements or to match the specification

## Usage

When working with ASCII flowcharts, load this skill and use the following rules:

- Follow spec defined in `../../flowchart.md`
- Keep the language spec self-contained; never refer to this or any other skill from the language spec.
- Diagrams should be placed in code blocks marked with `plaintext` syntax.
- Prefer symmetry whenever possible. Labels should be placed near middle of links or shapes they refer to. Links should connect to the middle of the shape if they are only ones, if there are more they should connect symmetrically.
- Fit shapes as closely as possible around their contents while respecting all margin and padding restrictions. For a shape containing only a single-line label, use exactly one space on each side: `| foo |` is OK, `| foo  |` is wrong. For compound or multiline shapes, minimize the overall bounding box; individual rows may contain extra whitespace when other contents determine the required width.
- Make the diagrams as concise as possible. Prefer links that are as short as possible while meeting the spec's minimum segment length.
- Among layouts that satisfy the spec and task constraints, prefer readability for the human end-user. Readability and symmetry preferences do not override mandatory requirements.

## Conformance and measurement

Syntax and numeric limits are requirements. Guidance explicitly described as preferred or discouraged is a recommendation; readability preferences do not override requirements.

Diagrams use a monospaced grid. Use spaces, never tabs, for whitespace. Measure width in displayed columns, including indentation and trailing spaces, but excluding the Markdown code fences. The applicable width limit is defined below unless the task explicitly specifies another limit.

## Spacing calculations

Calculate spacing independently on each axis using the corresponding horizontal or vertical margin and padding values from the language spec:

- Between sibling elements: `max(0, first element's margin + second element's margin)`.
- Between a parent shape's inner boundary and a child element: `max(0, parent's padding + child's margin)`.
- Horizontal spacing counts blank columns; vertical spacing counts blank rows. Zero spacing permits adjacency, not overlapping cells.
- Explicit link-attachment, crossing, and external-label spacing rules take precedence over these calculations. The negative endpoint margin applies only at intentional connections, not along the rest of a link.

## Limitations

- Diagrams must not exceed 120 monospaced columns in width unless the task explicitly specifies another limit. Measure width as defined in [Conformance and measurement](#conformance-and-measurement).
- Non-colliding cross pairs should be avoided, unless absolutely needed for readability or to meet the size constraints
- Do not shorten the labels or split the diagrams unless explicitly instructed to do so
- Layout changes must preserve all components, connections, and arrow directions unless a semantic change is explicitly requested.
