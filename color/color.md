# Color

## Index

* [Color Space](#color-space)
* [Color Model](#color-model)
  * [RGB](#rgb)
  * [CMY](#cmy)
  * [HSL/HSV](#hslhsv)
  * [YUV](#yuv)
* [Conversions](#conversions)
* [References](#references)

## Color Space

A [color space](https://en.wikipedia.org/wiki/Color_space) is the set of colors and luminance values which can be captured, stored or displayed in a medium.

The [CIE 1931 color spaces](https://en.wikipedia.org/wiki/CIE_1931_color_space) are the first defined quantitative links between distributions of wavelengths in the electromagnetic visible spectrum, and physiologically perceived colors in human color vision. They were created by the [International Commission on Illumination (CIE)](https://en.wikipedia.org/wiki/International_Commission_on_Illumination) in 1931 from a series of experiments that were combined into the specification of the CIE RGB color space, from which the CIE XYZ color space was derived.

<p align="center"><img align="center" width="50%" height="50%" src="CIE1931_chromaticity_diagram.svg"></p>
<p align="center">CIE Chromaticity Diagram</p>

## Color Model

A [color model](https://en.wikipedia.org/wiki/Color_model) is a method to represent colors, typically as tuples of three or four values or components. An image can be represented in memory component-wise or planar-wise.

* Packed formats are represented in memory [X<sub>1</sub>Y<sub>1</sub>Z<sub>1</sub>...X<sub>n</sub>Y<sub>n</sub>Z<sub>n</sub>].
* Planar formats are represented in memory [X<sub>1</sub>...X<sub>n</sub>] [Y<sub>1</sub>...Y<sub>n</sub>] [Z<sub>1</sub>...Z<sub>n</sub>].
* Semi-Planar formats are represented in memory [X<sub>1</sub>...X<sub>n</sub>] [Y<sub>1</sub>Z<sub>1</sub>...Y<sub>n</sub>Z<sub>n</sub>].
* Interleaved formats are represented in memory following a [sampling system](https://en.wikipedia.org/wiki/Chroma_subsampling#Sampling_systems_and_ratios), sampling is expressed as a three part ratio `J:a:b`. For example 4:2:2 has the `Y` and `Z` planes subsampled, they have less information than the `X` plane, [X<sub>1</sub>Y<sub>1</sub>X<sub>2</sub>Z<sub>1 </sub>X<sub>3</sub>Y<sub>2</sub>X<sub>4</sub>Z<sub>2</sub>...X<sub>n-1</sub>Y<sub>m</sub>X<sub>n</sub>Z<sub>m</sub>].

### RGB

[RGB](https://en.wikipedia.org/wiki/RGB_color_model) is an [additive](https://en.wikipedia.org/wiki/Additive_color) color model with a separation of `red`, `green` and `blue` [additive primary colors](https://en.wikipedia.org/wiki/Primary_color).

<p align="center"><img align="center" width="20%" height="20%" src="additive_color_mixing.png"></p>
<p align="center">Additive Color Mixing</p>

When the red, green and blue components have the same range of values the geometric representation has the shape of a cube otherwise it has the shape of a rectangular prism or cuboid.
<p align="center"><img align="center" width="30%" height="30%" src="rgb_cube.png"></p>
<p align="center">RGB Color Range</p>

There are several RGB pixel formats, the most common formats are:
* RGB888, uses 24 bits, 8 bits per component.
* RGB565, uses 16 bits, 5 bits for R, 6 bits for G and 5 bits for B.

### CMY

[CMY](https://en.wikipedia.org/wiki/CMY_color_model) is a [subtractive](https://en.wikipedia.org/wiki/Subtractive_color) color model with a separation of `cyan`, `magenta` and `yellow` [subtractive primary colors](https://en.wikipedia.org/wiki/Primary_color#Subtractive_mixing_of_ink_layers).

<p align="center"><img align="center" width="20%" height="20%" src="subtractive_color_mixing.png"></p>
<p align="center">Subtractive Color Mixing</p>

### HSL/HSV

[HSL](https://en.wikipedia.org/wiki/HSL_and_HSV) is a color model with `hue`, `saturation` and `level` components.

<p align="center"><img align="center" width="30%" height="30%" src="hsl_cylinder.png"></p>
<p align="center">HSL Color Range</p>

[HSV](https://en.wikipedia.org/wiki/HSL_and_HSV) is a color model with `hue`, `saturation` and `value` components (also known as HSB, `hue`, `saturation` and `brightness`).

<p align="center"><img align="center" width="30%" height="30%" src="hsv_cylinder.png"></p>
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

There are several [YUV pixel formats](https://www.fourcc.org/yuv.php), the recommended formats for video rendering are:
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

## Conversions

RGB888 to RGB555.
```
short pixel = ((R >> 3) << 11) | ((G >> 2) << 5) | (B >> 3)
```

RGB to YUV.
```
Y  =      (0.257 * R) + (0.504 * G) + (0.098 * B) + 16
Cr = V =  (0.439 * R) - (0.368 * G) - (0.071 * B) + 128
Cb = U = -(0.148 * R) - (0.291 * G) + (0.439 * B) + 128
```

YUV to RGB.
```
B = 1.164(Y - 16)                  + 2.018(U - 128)
G = 1.164(Y - 16) - 0.813(V - 128) - 0.391(U - 128)
R = 1.164(Y - 16) + 1.596(V - 128)
```

## References

* [The Essential Guide to Color Spaces](https://blog.frame.io/2020/02/03/color-spaces-101/)
* [Recommended 8-Bit YUV Formats for Video Rendering](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering)
* [Image Stride](https://docs.microsoft.com/en-us/windows/win32/medfound/image-stride?redirectedfrom=MSDN)
