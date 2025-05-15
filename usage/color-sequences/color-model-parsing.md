---
description: Getting a color from a text-based color representation.
icon: badge-check
---

# Color Model Parsing

In addition to Terminaux supporting RGB color model, you can also use the CMYK and other color models when creating the color instances, provided that their specifiers that you must use are:

* RGB's specifier is `rrr;ggg;bbb`, `#RRGGBB`, `#RGB`, `0-16777215`, `0-255`, or `0-15`
* CMYK's specifier is `cmyk:ccc;mmm;yyy;kkk`
* CMY's specifier is `cmy:ccc;mmm;yyy`
* HSL's specifier is `hsl:hhh;sss;lll`
* HSV's specifier is `hsv:hhh;sss;vvv`
* HWB's specifier is `hwb:hhh;www;bbb`
* RYB's specifier is `ryb:rrr;yyy;bbb`
* YIQ's specifier is `yiq:yyy;iii;qqq`
* YUV's specifier is `ryb:yyy;uuu;vvv`
* XYZ's specifier is `xyz:xxx;yyy;zzz`
* YXY's specifier is `yxy:yyy;xxx;yyy`
* HunterLab's specifier is `hunterlab:lll;aaa;bbb`
* CIE-L\*ab's specifier is `cielab:lll;aaa;bbb` or `cielab:lll;aaa;bbb;o;i`
* CIE-L\*uv's specifier is `cieluv:lll;uuu;vvv` or `cieluv:lll;uuu;vvv;o;i`
* CIE-L\*ch's specifier is `cielch:lll;ccc;hhh` or `cielch:lll;ccc;hhh;o;i`

{% hint style="info" %}
The `hhh` notation in the CIE-L\*ch specifier is an angle at degrees, not radians.

The `o` and `i` notations represent the observer (2 or 10 degrees) and the illuminant number starting from zero. These two notations will be used to get the 3D reference values (`X`, `Y`, and `Z`) used for calculation. This is returned by the `GetIlluminantReferences()` function in `IlluminanceTools`.
{% endhint %}

To get a color instance from just the specifiers mentioned above, you first have to pick a source specifier. For example, if you want an RGB color instance from HSV's specifier, you must have a string that holds the HSV color specifier as mentioned above. Then, you can call the `ParsingTools`'s `ParseSpecifier()` function, passing it that specifier, to get an RGB instance that you can convert to HSV using the available conversion tools that you can consult in the below page.

{% content-ref url="color-model-conversions.md" %}
[color-model-conversions.md](color-model-conversions.md)
{% endcontent-ref %}

{% hint style="info" %}
You have two options if you don't want to rely on exceptions:

* For boolean-based checks, you can rely on the output of the `IsSpecifierValidRgbHash()`, `IsSpecifierConsoleColors()`, and `IsSpecifierValid()` on `ParsingTools`.
* If you want to also check the values, you can consult the `...AndValueValid()` sibling functions.

You can also use the color-model-specific `IsSpecifierValid()` function, such as `RedYellowBlue`.
{% endhint %}
