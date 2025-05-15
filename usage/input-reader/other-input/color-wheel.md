---
description: Here's how you can let the users choose their own colors
icon: palette
---

# Color Wheel

<figure><img src="../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

The new color wheel, `ColorSelector`, is now available. You can use this brand new color selector, which is powered by the [textual UI](../../console-tools/textual-ui/) feature, to get information about your selected color visually. The color preview is split into two views: normal and color blinded. You can call the `OpenColorSelector()` function in your code to get the new color selector.

The color selector allows you to change the color in the following modes:

* In true color mode, you can change the hue, the lighting, and the saturation by pressing the appropriate key shortcuts to change the colors.
* In 256 and 16 colors mode, you can select a color using the right and the left arrow keys. It shows you color information, including the CMYK, HSL, and grayscale values.

The following controls are available:

| Key                                             | Action                                                                         |
| ----------------------------------------------- | ------------------------------------------------------------------------------ |
| `ENTER`                                         | Accept color selection                                                         |
| `ESC`                                           | DIscard changes                                                                |
| `H`                                             | Help page                                                                      |
| `LEFT` / `WHEEL UP on color box`                | Reduce hue (for true color)                                                    |
|                                                 | Previous color (for 256 and 16 colors)                                         |
| `CTRL + LEFT` / `WHEEL UP on lightness ramp`    | Reduce lightness (true color only)                                             |
| `RIGHT` / `WHEEL DOWN on color box`             | Increase hue (for true color)                                                  |
|                                                 | Next color (for 256 and 16 colors)                                             |
| `CTRL + RIGHT` / `WHEEL DOWN on lightness ramp` | Increase lightness (true color only)                                           |
| `DOWN` / `WHEEL UP on saturation ramp`          | Reduce saturation (true color only)                                            |
| `UP` / `WHEEL DOWN on saturation ramp`          | Increase saturation (true color only)                                          |
| `TAB`                                           | Change color mode (true color, 256 colors, and 16 colors)                      |
| `I`                                             | Shows the extended color information, including info about color deficiencies. |
| `O` / `WHEEL DOWN on opacity ramp`              | Increases the opacity                                                          |
| `P` / `WHEEL UP on opacity ramp`                | Decreases the opacity                                                          |
| `N`                                             | Next color blindness simulation                                                |
| `CTRL` + `N`                                    | Increase transformation frequency                                              |
| `M`                                             | Previous color blindness simulation                                            |
| `CTRL` + `M`                                    | Decrease transformation frequenc                                               |
| `W`                                             | Select web color                                                               |
| `L`                                             | Shows color list                                                               |

This function returns a `Color` instance containing necessary information. To know more about the structure of the `Color` class, visit the page below to learn more.

{% content-ref url="../../color-sequences/" %}
[color-sequences](../../color-sequences/)
{% endcontent-ref %}
