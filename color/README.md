# Color

## Index

* [Introduction](#introduction)
* [Color Space](#color-space)
  * [CIE](#cie)
  * [ACES](#aces)
* [Color Model](#color-model)
  * [RGB](#rgb)
  * [CMY](#cmy)
  * [HSL/HSV](#hslhsv)
  * [YUV](#yuv)
* [Blend Modes](#blend-modes)
* [References](#references)

## Introduction

[Colorimetry]() is the science that quantifies and describes physically the human color perception and [color theory](https://en.wikipedia.org/wiki/Color_theory), in visual arts, is a body of practical guidance to color mixing.

During the 20th century two important color systems were created. The [Munsell Color System](https://en.wikipedia.org/wiki/Munsell_color_system) and the [Natural Color System (NCS)](https://en.wikipedia.org/wiki/Natural_Color_System). Both were based on human perception and derived from experiments.

## Color Space

A [color space](https://en.wikipedia.org/wiki/Color_space) is the set of colors and luminance values which can be captured, stored or displayed in a medium.

### CIE

The [CIE 1931 color spaces](https://en.wikipedia.org/wiki/CIE_1931_color_space) are the first defined quantitative links between distributions of wavelengths in the electromagnetic visible spectrum, and physiologically perceived colors in human color vision. They were created by the [International Commission on Illumination (CIE)](https://en.wikipedia.org/wiki/International_Commission_on_Illumination) in 1931 from a series of experiments that were combined into the specification of the `CIE RGB` color space, from which the `CIE XYZ` color space was derived.

<p align="center"><img align="center" width="60%" height="60%" src="assets/CIE1931_chromaticity_diagram.svg"></p>
<p align="center">CIE Chromaticity Diagram</p>

* The diagram represents the colors visible to the average human eye.
* The edge is called spectral locus, the set of [spectral colors](https://en.wikipedia.org/wiki/Spectral_color), pure monochromatic light measured by wavelength in nanometers.
* Most saturated colors are at the edge.
* Least saturated colors are at the center.
* Colors along any line between 2 points can be made by mixing the colors at the end points.
* Line of purples are fully saturated colors that can only be made by mixing red and blue.

The diagram gives a common frame to define color spaces in `xyY` coordinates where `xy` is `chrominance` and `Y` is `luminance`.

Each color space has a [gamut](https://en.wikipedia.org/wiki/Gamut), a subset of colors that can be represented, and is defined by:
* Primary colors (R,G,B).
* [White point](https://en.wikipedia.org/wiki/White_point). Color spaces use [illuminants](https://en.wikipedia.org/wiki/Template:Color_temperature_white_points) to define reference whites, each illuminant has a [correlated color temperature (CCT)](https://en.wikipedia.org/wiki/Color_temperature#Correlated_color_temperature). The commonly used standard illuminant is [D65](https://en.wikipedia.org/wiki/Illuminant_D65) at 6504 K.
* [Transfer function](https://en.wikipedia.org/wiki/Transfer_function). [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction) is a non-linear operation used to encode and decode luminance or tristimulus values. It is used to take advantage of the non-linear manner in which humans perceive light and color.

<p align="center"><img align="center" width="80%" height="80%" src="assets/color_spaces.png"></p>
<p align="center">Color Spaces</p>

Color space conversion is done with `lineal values` and depends on the `primary colors` and `white points`. There are several lists of [matrices](http://www.brucelindbloom.com/index.html?Eqn_RGB_XYZ_Matrix.html) to convert RGB/XYZ and XYZ/RGB.

**RGB(709)/RGB(2020)**
<pre>
XYZ = RGB709_TO_XYZ_MAT * RGB(709)
RGB(2020) = XYZ_TO_RGB2020_MAT * XYZ
</pre>
Conversion assuming same white points.

**XYZ(D50)/XYZ(D65)**
<pre>
LMS(D50) = XYZ_TO_LMS_MAT * XYZ(D50)
LMS(D65) = D50_TO_D65_CAT * LMS(D50)
XYZ(D65) = LMS_TO_XYZ_MAT * LMS(D65)
</pre>
White points conversion matrices are called [Chromatic Adaptation Transform (CAT)](https://en.wikipedia.org/wiki/Chromatic_adaptation) and are equivalent to apply a [white balance](https://en.wikipedia.org/wiki/Color_balance).

**XYZ/xyY**
<pre>
x = X / (X + Y + Z)
y = Y / (X + Y + Z)
Y = Y
</pre>
For black, `X=Y=Z=0`, set `x` and `y` to the chromaticity coordinates of the reference white.

### ACES

[Academy Color Encoding System ACES](https://en.wikipedia.org/wiki/Academy_Color_Encoding_System) is a color image encoding system created by industry professionals of [Academy of Motion Picture Arts and Sciences](https://en.wikipedia.org/wiki/Academy_of_Motion_Picture_Arts_and_Sciences).

<p align="center"><img align="center" width="40%" height="40%" src="assets/aces_pipeline.png"></p>
<p align="center">ACES Pipeline</p>

* IDT: Input Device Transform.
* ACES Color Space.
* LMT: Look Modification Transform (optional).
* RRT: Reference Rendering Transform (tone mapping for a Reference Display Device).
* ODT: Output Device Transform.

ACES has several color spaces, defined by:
* Primary `AP0 = R(0.7347,0.2653) G(0,1) B(0.0001,-0.0770)`.
* Primary `AP1 = R(0.713,0.293) G(0.165,0.830) B(0.128,0.044)`.
* Reference illuminant `(0.32168,0.33767)`, close to CIE [D60](https://en.wikipedia.org/wiki/CIE_D60).

<p align="center"><img align="center" width="60%" height="60%" src="assets/aces_color_spaces.png"></p>
<p align="center">ACES Color Spaces</p>

ACES `working` color spaces are:
* ACEScc: Color grading (AP1 / log).
* ACEScct: Color grading (AP1 / log+toe).
* ACEScg: VFX and composition (AP1 / lineal).
* ACESproxy: Interchange (AP0).

## Color Model

A [color model](https://en.wikipedia.org/wiki/Color_model) is a method to represent colors, typically as tuples of three or four values or components. An image can be represented in memory (with a [stride](https://docs.microsoft.com/en-us/windows/win32/medfound/image-stride?redirectedfrom=MSDN)) component-wise or planar-wise.

* Packed formats are represented in memory:
<pre>
[X<sub>1</sub>Y<sub>1</sub>Z<sub>1</sub>...X<sub>n</sub>Y<sub>n</sub>Z<sub>n</sub>]
</pre>
* Planar formats are represented in memory:
<pre>
[X<sub>1</sub>...X<sub>n</sub>] [Y<sub>1</sub>...Y<sub>n</sub>] [Z<sub>1</sub>...Z<sub>n</sub>]
</pre>
* Semi-Planar formats are represented in memory:
<pre>
[X<sub>1</sub>...X<sub>n</sub>] [Y<sub>1</sub>Z<sub>1</sub>...Y<sub>n</sub>Z<sub>n</sub>]
</pre>
* Interleaved formats are represented in memory following a [sampling system](https://en.wikipedia.org/wiki/Chroma_subsampling#Sampling_systems_and_ratios), expressed as a three part ratio `J:a:b`. For example `4:2:2` has the `Y` and `Z` planes subsampled, they have less information than the `X` plane.
<pre>
[X<sub>1</sub>Y<sub>1</sub>X<sub>2</sub>Z<sub>1 </sub>X<sub>3</sub>Y<sub>2</sub>X<sub>4</sub>Z<sub>2</sub>...X<sub>n-1</sub>Y<sub>m</sub>X<sub>n</sub>Z<sub>m</sub>]
</pre>

### RGB

[RGB](https://en.wikipedia.org/wiki/RGB_color_model) is an [additive](https://en.wikipedia.org/wiki/Additive_color) color model with a separation of `red`, `green` and `blue` [additive primary colors](https://en.wikipedia.org/wiki/Primary_color).

<p align="center"><img align="center" width="20%" height="20%" src="assets/additive_color_mixing.png"></p>
<p align="center">Additive Color Mixing</p>

When the red, green and blue components have the same range of values the geometric representation has the shape of a cube otherwise it has the shape of a rectangular prism or cuboid.
<p align="center"><img align="center" width="40%" height="40%" src="assets/rgb_cube.png"></p>
<p align="center">RGB Color Range</p>

There are multitude [RGB pixel formats](https://en.wikipedia.org/wiki/List_of_monochrome_and_RGB_color_formats), the most common formats are:
* RGB888 or RGB24, uses 24 bits (8 bits per component).
* RGB565, uses 16 bits (5 bits R, 6 bits G and 5 bits B).

**RGB888/RGB555**
<pre>
short pixel = ((R >> 3) << 11) | ((G >> 2) << 5) | (B >> 3)
</pre>

### CMY

[CMY](https://en.wikipedia.org/wiki/CMY_color_model) is a [subtractive](https://en.wikipedia.org/wiki/Subtractive_color) color model with a separation of `cyan`, `magenta` and `yellow` [subtractive primary colors](https://en.wikipedia.org/wiki/Primary_color#Subtractive_mixing_of_ink_layers).

<p align="center"><img align="center" width="20%" height="20%" src="assets/subtractive_color_mixing.png"></p>
<p align="center">Subtractive Color Mixing</p>

### HSL/HSV

[HSL](https://en.wikipedia.org/wiki/HSL_and_HSV) is a color model with `hue`, `saturation` and `level` components.

<p align="center"><img align="center" width="30%" height="30%" src="assets/hsl_cylinder.png"></p>
<p align="center">HSL Color Range</p>

[HSV](https://en.wikipedia.org/wiki/HSL_and_HSV) is a color model with `hue`, `saturation` and `value` components (also known as HSB, `hue`, `saturation` and `brightness`).

<p align="center"><img align="center" width="30%" height="30%" src="assets/hsv_cylinder.png"></p>
<p align="center">HSV Color Range</p>

Both color ranges shapes are cylindrical.
* Hue, the angular dimension, starts at the red primary at 0°, passes through the green primary at 120° and the blue primary at 240°, and then back to red at 360°.
* The central vertical axis is the achromatic grayscale range, from top to bottom, white at lightness 1 to black at lightness 0.
* Primary and secondary colors are around the outside edge of the cylinder with saturation 1. These saturated colors have lightness 0.5 in HSL and value 1 in HSV.
* Mixing these saturated colors with black ([shades](https://en.wikipedia.org/wiki/Tints_and_shades)) leaves saturation unchanged.
* In HSL, mixing with white ([tints](https://en.wikipedia.org/wiki/Tints_and_shades)) leaves saturation unchanged.
* In HSL, mixing with both black and white ([tones](https://en.wikipedia.org/wiki/Tints_and_shades)) reduces saturation.
* In HSV, mixing with white ([tints](https://en.wikipedia.org/wiki/Tints_and_shades)) reduces saturation.

### YUV

[YUV](https://en.wikipedia.org/wiki/YUV) is a color model with `luma` and `chrominance` components. Sometimes `YUV` is also named `YCrCb`, where `Cr` is the red projection plane and `Cb` is the blue projection plane. It was invented when engineers wanted color television in a black-and-white infrastructure.

There are several [YUV pixel formats](https://www.fourcc.org/yuv.php), the [recommended formats](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering) for video rendering are:
* 4:4:4 (32 bpp)
  * [AYUV](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#ayuv)
* 4:2:2 (16 bpp)
  * [YUY2](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#yuy2)
  * [UYVY](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#uyvy)
* 4:2:0 (16 bpp)
  * [IMC1](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#imc1)
  * [IMC3](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#imc3)
* 4:2:0 (12 bpp)
  * [IMC2](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#imc2)
  * [IMC4](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#imc4)
  * [YV12](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#yv12)
  * [NV12](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering#nv12)

**RGB/YUV**
<pre>
Y =  (0.257 * R) + (0.504 * G) + (0.098 * B) + 16
U = -(0.148 * R) - (0.291 * G) + (0.439 * B) + 128
V =  (0.439 * R) - (0.368 * G) - (0.071 * B) + 128
</pre>

**YUV/RGB**
<pre>
R = 1.164(Y - 16)                  + 1.596(V - 128)
G = 1.164(Y - 16) - 0.391(U - 128) - 0.813(V - 128)
B = 1.164(Y - 16) + 2.018(U - 128)
</pre>

## Blend Modes

[Blend modes](https://en.wikipedia.org/wiki/Blend_modes) are used to determine how two color layers are blended with each other.

<p align="center"><img align="center" width="80%" height="80%" src="assets/blend_modes.png"></p>
<p align="center">Blend Modes</p>

**Normal**<br>
Mixes two layers by applying [alpha blending](https://en.wikipedia.org/wiki/Alpha_compositing).
<pre>
α<sub>0</sub> = α<sub>a</sub> + α<sub>b</sub>(1 - α<sub>a</sub>)
C<sub>0</sub> = (C<sub>a</sub>α<sub>a</sub> + C<sub>b</sub>α<sub>b</sub>(1 - α<sub>a</sub>)) / α<sub>0</sub>
</pre>

**Dissolve**<br>
Mixes two layer by taking random pixels from both layers using a [diffusion dither](https://en.wikipedia.org/wiki/Dither) pattern based on alpha.<br>
No anti-aliasing is used so the result looks grainy.

**Multiply**<br>
Mixes two layers by multiplying the values.<br>
Since color values are in the range `[0,1]`, the result will be less than each initial value.<br>
Multiplying a color by black produces black. Multiplying a color by white produces the same color.<br>
If a layer contains homogeneous value, **multiply** is equivalent to using **normal** with the value as opacity and a black bottom layer.
<pre>
C<sub>0</sub> = C<sub>a</sub>C<sub>b</sub>
</pre>

**Screen**<br>
Mixes two layers by inverting, multiplying and inverting again the values.<br>
**Screen** is the opposite of **multiply**.<br>
If a layer contains a homogeneous value, **screen** is equivalent to using **normal** with the value as opacity and a white top layer.
<pre>
C<sub>0</sub> = 1 - (1 - C<sub>a</sub>)(1 - C<sub>b</sub>)
</pre>

**Overlay**<br>
Combines **multiply** and **screen**.<br>
If the base layer is light the result is lighter. If the base layer is dark the result is darker.<br>
An overlay with the same picture looks like an S-curve.
<pre>
       2C<sub>a</sub>C<sub>b</sub>                  if a < 0.5
C<sub>0</sub> =
       1 - 2(1 - C<sub>a</sub>)(1 - C<sub>b</sub>)  otherwise
</pre>

## References

* [Lists of Colors](https://en.wikipedia.org/wiki/Lists_of_colors)
* [A Beginner's Guide to CIE Colorimetry](https://medium.com/hipster-color-science/a-beginners-guide-to-colorimetry-401f1830b65a)
* [The Essential Guide to Color Spaces](https://blog.frame.io/2020/02/03/color-spaces-101/)
* [Bruce Lindbloom Web Site](http://www.brucelindbloom.com/index.html)
* [Academy Color Encoding System](https://www.oscars.org/science-technology/sci-tech-projects/aces)
* [Pixel's Color](https://gitlab.freedesktop.org/pq/color-and-hdr/-/blob/main/doc/pixels_color.md)
