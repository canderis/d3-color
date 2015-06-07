# d3-color

Color spaces! RGB, HSL, Lab and HCL (Lch).

Even though your browser understands a lot about colors, it doesn’t offer much help in manipulating colors through JavaScript. This module provides representations for various color spaces, including [RGB](http://en.wikipedia.org/wiki/RGB_color_model), [HSL](http://en.wikipedia.org/wiki/HSL_and_HSV), [LAB](http://en.wikipedia.org/wiki/Lab_color_space) and [HCL](https://en.wikipedia.org/wiki/CIELUV_color_space#Cylindrical_representation), allowing specification, interpolation, conversion and manipulation (such as making colors brighter or darker).

A d3.color base type is provided if you want to extend D3 with additional color spaces. This type enables automatic RGB interpolation by [d3.interpolate](Transitions#d3_interpolate) (detected via `instanceof d3.color`).

### API Reference

<a name="color" href="#color">#</a> <b>color</b>(<i>specifier</i>)

Parses the specified CSS Color Module Level 3 *specifier* string, returning an [RGB](#rgb) or [HSL](#hsl) color. If the specifier was not valid, an RGB color with NaN channel values is returned. Some examples:

* `"rgb(255,255,255)"`
* `"hsl(120,50%,20%)"`
* `"#ffeeaa"`
* `"#fea"`
* `"steelblue"`

The list of supported [named colors](http://www.w3.org/TR/SVG/types.html#ColorKeywords) is specified by CSS.

Note: this function may also be used with `instanceof` to test if an object is a color instance. The same is true of color subclasses, allowing you to test whether a color is in a particular color space.

<a name="color_rgb" href="#color_rgb">#</a> *color*.<b>rgb</b>()

Returns the [RGB equivalent](#rgb) of this color.

<a name="color_brighter" href="#color_brighter">#</a> *color*.<b>brighter</b>([<i>k</i>])

Returns a brighter copy of this color. If *k* is specified, it controls how much brighter the returned color should be. If *k* is not specified, it defaults to 1. The behavior of this method is dependent on the implementing color space.

<a name="color_darker" href="#color_darker">#</a> color.<b>darker</b>([<i>k</i>])

Returns a darker copy of this color. If *k* is specified, it controls how much brighter the returned color should be. If *k* is not specified, it defaults to 1. The behavior of this method is dependent on the implementing color space.

<a name="color_toString" href="#color_toString">#</a> *color*.<b>toString</b>()

Returns the RGB hexadecimal string representing this color, such as `"#f7eaba"`.

<a name="rgb" href="#rgb">#</a> <b>rgb</b>(<i>r</i>, <i>g</i>, <i>b</i>)<br>
<a href="#rgb">#</a> <b>rgb</b>(<i>specifier</i>)<br>
<a href="#rgb">#</a> <b>rgb</b>(<i>color</i>)<br>

Constructs a new RGB color. The channel values are exposed as `r`, `g` and `b` properties on the returned instance.

If *r*, *g* and *b* are specified, these represent the channel values of the returned color. Channel values will be rounded to the nearest integer value and clamped to the range [0,255].

If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the RGB color space. See [color](#color) for examples.

If a [*color*](#color) instance is specified, it is converted to the RGB color space using [color.rgb](#color_rgb). Note that unlike [color.rgb](#color_rgb) this method *always* returns a new instance, even if *color* is already an RGB color.

<a name="hsl" href="#hsl">#</a> <b>hsl</b>(<i>h</i>, <i>s</i>, <i>l</i>)<br>
<a href="#hsl">#</a> <b>hsl</b>(<i>specifier</i>)<br>
<a href="#hsl">#</a> <b>hsl</b>(<i>color</i>)<br>

Constructs a new HSL color. The channel values are exposed as `h`, `s` and `l` properties on the returned instance.

If *h*, *s* and *l* are specified, these represent the channel values of the returned color. The saturation and lightness channels will be clamped to the range [0,1].

If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the HSL color space. See [color](#color) for examples.

If a [*color*](#color) instance is specified, it is converted to the RGB color space using [color.rgb](#color_rgb) and then converted to HSL. (Colors already in the HSL color space skip the conversion to RGB.)

<a name="lab" href="#lab">#</a> <b>lab</b>(<i>l</i>, <i>a</i>, <i>b</i>)<br>
<a href="#lab">#</a> <b>lab</b>(<i>specifier</i>)<br>
<a href="#lab">#</a> <b>lab</b>(<i>color</i>)<br>

Constructs a new Lab color. The channel values are exposed as `l`, `a` and `b` properties on the returned instance.

If *l*, *a* and *b* are specified, these represent the channel values of the returned color.

If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the Lab color space. See [color](#color) for examples.

If a [*color*](#color) instance is specified, it is converted to the RGB color space using [color.rgb](#color_rgb) and then converted to Lab. (Colors already in the Lab color space skip the conversion to RGB, and colors in the HCL color space are converted directly to Lab.)

<a name="interpolateRgb" href="#interpolateRgb">#</a> <b>interpolateRgb</b>(<i>a</i>, <i>b</i>)

Returns an RGB color space interpolator between the two colors *a* and *b*. The colors *a* and *b* need not be in RGB; they will be converted to RGB using [rgb](#rgb). The return value of the interpolator is a hexadecimal RGB string.

<a name="interpolateHsl" href="#interpolateHsl">#</a> <b>interpolateHsl</b>(<i>a</i>, <i>b</i>)

Returns an HSL color space interpolator between the two colors *a* and *b*. The colors *a* and *b* need not be in HSL; they will be converted to HSL using [hsl](#hsl). If either color’s hue or saturation is NaN, the opposing color’s channel value is used. The shortest path between hues is used. The return value of the interpolator is a hexadecimal RGB string.

<a name="interpolateHslLong" href="#interpolateHslLong">#</a> <b>interpolateHslLong</b>(<i>a</i>, <i>b</i>)

Like [interpolateHsl](#interpolateHsl), but does not use the shortest path between hues.

<a name="d3_interpolateLab" href="#d3_interpolateLab">#</a> d3.<b>interpolateLab</b>(<i>a</i>, <i>b</i>)

Returns a Lab color space interpolator between the two colors *a* and *b*. The colors *a* and *b* need not be in Lab; they will be converted to Lab using [lab](#lab). The return value of the interpolator is a hexadecimal RGB string.

<a name="interpolateHcl" href="#interpolateHcl">#</a> <b>interpolateHcl</b>(<i>a</i>, <i>b</i>)

Returns an HCL color space interpolator between the two colors *a* and *b*. The colors *a* and *b* need not be in HCL; they will be converted to HCL using [hcl](#hcl). If either color’s hue or chroma is NaN, the opposing color’s channel value is used. The shortest path between hues is used. The return value of the interpolator is a hexadecimal RGB string.

<a name="interpolateHclLong" href="#interpolateHclLong">#</a> <b>interpolateHclLong</b>(<i>a</i>, <i>b</i>)

Like [interpolateHcl](#interpolateHcl), but does not use the shortest path between hues.

### Changes from D3 3.x:

* A new color method parses the specified string according to [CSS Color Module Level 3](http://www.w3.org/TR/css3-color/#colorunits) and returns the corresponding color in its colorspace. For HSL color values, this is the HSL colorspace; for other values, the RGB colorspace is used.

* In addition, the color method now correctly parses RGB colors with percentages (e.g., `rgb(30%,40%,50%)`). Decimal values where integers are required are no longer allowed (e.g., `rgb(100.5,0,0)` is not a valid color).

* The rgb.brighter method no longer special-cases behavior for black and very dark channels; it is now a simple channel multiplier, consistent with rgb.darker and implementations in the other colorspaces.

* The rgb.hsl method has been removed; use the appropriate constructor to convert any desired colorspace (e.g., `hsl(foo)`).

* All colorspaces, including RGB, now support the color.rgb method. This method returns a color instance representing the nearest-equivalent color in the RGB colorspace. For RGB colors, it returns `this`. Use the rgb constructor if you want a copy.

* When converting to HCL, hue and chroma are no longer undefined if the luminance is zero. Thus, the roundtrip from Lab to HCL and back again no longer loses information.

* Colors are now validated upon construction. For example, an RGB color’s `r`, `g` and `b` values are integers in the range [0,100]; an HSL color’s `s` and `l` are numbers in the range [0,1].
