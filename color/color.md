# Color

## Index

* [Color Space](#color-space)
* [Color Model](#color-model)
* [References](#references)

## Color Space

A [color space](https://en.wikipedia.org/wiki/Color_space) is the set of colors and luminance values which can be captured, stored or displayed in a medium.

The [CIE 1931 color spaces](https://en.wikipedia.org/wiki/CIE_1931_color_space) are the first defined quantitative links between distributions of wavelengths in the electromagnetic visible spectrum, and physiologically perceived colors in human color vision. They were created by the [International Commission on Illumination (CIE)](https://en.wikipedia.org/wiki/International_Commission_on_Illumination) in 1931 from a series of experiments that were combined into the specification of the CIE RGB color space, from which the CIE XYZ color space was derived.

<p align="center"><img align="center" src="CIE1931_chromaticity_diagram.svg"></p>
<p align="center">CIE Chromaticity Diagram</p>

## Color Model

A [color model](https://en.wikipedia.org/wiki/Color_model) is a method to represent colors, typically as tuples of three or four values or components. An image can be represented in memory component-wise or planar-wise.

* Packed formats are represented in memory `[X0Y0Z0...X(n-1)Y(n-1)Z(n-1)]`.
* Planar formats are represented in memory `[X0...X(n-1)] [Y0...Y(n-1)] [Z0...Z(n-1)]`.
* Semi-Planar formats are represented in memory `[X0...X(n-1)] [Y0Z0...Y(n-1)Z(n-1)]`.
* Interleaved formats are represented in memory following a [sampling system](https://en.wikipedia.org/wiki/Chroma_subsampling#Sampling_systems_and_ratios), for example 4:2:2 `[X0Y0X1Z0 X2Y1X3Z1...X(n-2)Y((n-1)/2)X(n-1)Z((n-1)/2)]`.

### RGB

[RGB](https://en.wikipedia.org/wiki/RGB_color_model) is an [additive](https://en.wikipedia.org/wiki/Additive_color) color model with a separation of red, green and blue [additive primary colors](https://en.wikipedia.org/wiki/Primary_color).

### CMY

[CMY](https://en.wikipedia.org/wiki/CMY_color_model) is a [subtractive](https://en.wikipedia.org/wiki/Subtractive_color) color model with a separation of cyan, magenta and yellow [subtractive primary colors](https://en.wikipedia.org/wiki/Primary_color#Subtractive_mixing_of_ink_layers).

### YUV

[YUV](https://en.wikipedia.org/wiki/YUV) is a color model with a separation of luma `Y` and chrominance `U,V` components. It was invented when engineers wanted color television in a black-and-white infrastructure. Sometimes `YUV` is named `YCrCb`, where `Cr` is the red projection plane and `Cb` is the blue projection plane.

## References

* [The Essential Guide to Color Spaces](https://blog.frame.io/2020/02/03/color-spaces-101/)
* [YUV Pixel Formats](https://www.fourcc.org/yuv.php)
* [Recommended 8-Bit YUV Formats for Video Rendering](https://docs.microsoft.com/en-us/windows/win32/medfound/recommended-8-bit-yuv-formats-for-video-rendering)
