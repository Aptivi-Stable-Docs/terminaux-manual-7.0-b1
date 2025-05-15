---
description: What do they represent?
icon: table-tree
---

# Terminal Structures

Terminaux provides some useful structures that help you make console applications seamlessly and without repetition, such as coordinates, margins, and padding. They are found in the `Terminaux.Base.Structures` namespace, and they use structs to represent values as they are informational.

## Coordinates

A structure that defines a coordinate relative to the console that starts with the upper left corner (0, 0) is called `Coordinate`. It contains two properties:

* `X`: Specifies the left position as specified by the X axis of the console
* `Y`: Specifies the top position as specified by the Y axis of the console

This allows you to store coordinate information in one variable without having to resort to tuples or multiple variables.

## Padding

A structure that defines padding information related to the element, such as the console, is called `Padding`. The default padding is (0, 0, 0, 0) which represents the left, the top, the right, and the bottom padding. It contains the following properties:

* `Left`: Left padding starting from 0
* `Top`: Top padding starting from 0
* `Right`: Right padding starting from 0
* `Bottom`: Bottom padding starting from 0

This allows you to store padding information in one variable without having to resort to tuples or multiple variables.

## Margin

A structure that defines the margin of an element is called `Margin`. It specifies the width and the height of the element, which makes this struct a measurement structure. It measures the margin values according to the padding values given. It contains the following properties:

* `Width`: Processed width with margin padding applied
* `Height`: Processed height with margin padding applied

This allows you to store margin information in one variable without having to resort to tuples or multiple variables.
