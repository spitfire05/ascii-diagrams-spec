# Flowchart

This document serves as a "language specification" for an ASCII flowchart diagram.

## Elements

### Shapes

V-Margin: 0
H-Margin: 1
V-Padding: 0
H-Padding: 1

#### Container-like

Container-like shapes can contain one or more other elements inside.

Service or rectangular block:

```plaintext
+---------+
| Service |
+---------+
```

Database or cylinder:

```plaintext
 .--------.
( Database )
 '--------'
```

Cloud service, SaaS, etc:

```plaintext
 ~~~~~~~~~
(( Cloud ))
 ~~~~~~~~~
```

#### Simple

Actor:

```plaintext
 O
/|\
/ \ 
```

### Links

Margin: -1 at intentional endpoint connections; elsewhere, respect the margins of unrelated elements.

In a complete diagram, link endpoints must touch their intended shapes' bounding boxes or link junctions directly. Contact with a visible shape stroke is not required. Links must not touch unrelated shapes or labels. Dangling endpoints are allowed only in standalone syntax examples, such as the link example below.

Links can consist of:

- vertical elements `|`
- horizontal elements `-`
- bends and connected junctions `+`
- optional end arrows: up `^`, down `v`, left `<`, and right `>`
- non-colliding cross pair `o o`

At a `+`, all incident link segments are connected. Perpendicular links may meet only at a connected `+` junction or cross using a non-colliding cross pair. A cross pair does not connect the two links.

For readability, each straight segment between endpoints, bends, or junctions must span at least 3 grid cells. Count arrowheads and bend/junction `+` cells as part of the segment, but do not count shape-boundary cells. Thus `-->` and `+--+` satisfy the minimum. A `+` shared by multiple segments counts toward each segment's length. Crossings do not split a straight segment; count all cells traversed through a crossing, including its markers and central cell.

At a shape connection or a dangling endpoint in a syntax example, the terminal link character must be an arrowhead or a vertical/horizontal element. A link may also join another link at a `+` junction. An `o` crossing marker cannot be a terminal character.

`--o|o--` denotes a horizontal link passing under a vertical link without connecting to it. The two `o` markers must enclose exactly one cell containing the perpendicular link: `o|o` horizontally, or three vertically aligned cells containing `o`, `-`, and `o`. Both links must continue on both sides of the crossing. Thus `--o||o--` is invalid. The vertical-under-horizontal orientation is allowed but discouraged as less readable.

The cross pair can also be used when crossing edge of a container shape to connect to one of its child elements. In that case, the cross pair can enclose more than one cell, for example to cross the cloud shape's `((`.

Example of an advanced link making use of all possible elements:
```plaintext
        ^     |
        |     |
        |     |
<-------+----o|o->
        |     |
        |     |
        +-----+
        |     |
        |     |
        v     v
```

### Labels

V-Margin: -1
H-Margin: 0

A label is text next to another element, usually giving additional context. External labels must be separated from link strokes by at least one space or one blank row, as appropriate. Text inside a shape follows shape's padding rules.

Example:

```plaintext
+-----+
| Foo |
+-----+
   |
   | Foobar
   v
+-----+
| Bar |
+-----+
```

## Margins & Padding

Every element type defines its margin size. For example, a margin 1 on shapes means that any two shapes need to have at least 2 characters of whitespace between them.

[Links](#Links) are a special case, where their end points should always directly connect to other elements. They however, should not "touch" unrelated shapes and respect their margins.

[Shapes](#shapes) also define padding, as they can have other elements inside them (like labels or other shapes), if they belong to the [Container-like](#container-like) type.

When calculating a minimum space between parent shape and a child element, parent's padding and child's margin should be added together.

Negative margins on elements can never result in elements overlapping. The minimum distance between any two elements is 0.

Bounding boxes determine clearance from unrelated elements and intentional link attachment positions, including for irregular shapes. A link endpoint must be directly adjacent to the intended shape's bounding box, even if the adjoining cell inside that box is whitespace, such as the space between an actor's feet.

## Special Examples

Nested elements in container shape:
```plaintext
+---------------------+
|  +-----+   +-----+  |
|  | Foo |---| Bar |  |
|  +-----+   +-----+  |
+---------------------+
```

Multiline version of database and cloud shapes:
```plaintext
 .---.
( aaa )
( bbb )
( ccc )
 '---'
```

```plaintext
 ~~~~~~~
(( aaa ))
(( bbb ))
(( ccc ))
 ~~~~~~~
```
