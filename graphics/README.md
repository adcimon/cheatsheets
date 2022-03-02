# Computer Graphics

[Computer graphics](https://en.wikipedia.org/wiki/Computer_graphics_(computer_science)) is a sub-field of computer science which studies methods for digitally synthesizing and manipulating visual content.

## Index

* [Transformation Matrices](#transformation-matrices)
  * [Translation Matrix](#translation-matrix)
  * [Rotation Matrix](#rotation-matrix)
  * [Scaling Matrix](#scaling-matrix)
* [Algorithms](#algorithms)
  * [Letterbox](#letterbox)

## Transformation Matrices

### Translation Matrix

<p align="center"><img align="center" width="25%" height="25%" src="translation_matrix.svg"></p>

### Rotation Matrix

<p align="center"><img align="center" width="25%" height="25%" src="rotationx_matrix.svg"></p>
<p align="center"><img align="center" width="25%" height="25%" src="rotationy_matrix.svg"></p>
<p align="center"><img align="center" width="25%" height="25%" src="rotationz_matrix.svg"></p>

### Scaling Matrix

<p align="center"><img align="center" width="25%" height="25%" src="scaling_matrix.svg"></p>

### Shearing Matrix

<p align="center"><img align="center" width="25%" height="25%" src="shearing_matrix.svg"></p>

## Algorithms

### Letterbox

Given the image:
* Resolution: `(wi, hi)`
* Aspect Ratio:  `ri = wi / hi`

Given the canvas:
* Resolution: `(wc, hc)`
* Aspect Ratio: `rc = wc / hc`

The new resolution is:
```
rc > ri ? (wi * hc/hi, hc) : (wc, hi * wc/wi)
```

To center the image:
```
top = (hc - hnew) / 2
left = (wc - wnew) / 2
```

Example.
```
         20
|------------------|
    10
|---------|

--------------------     ---   ---
|         |        |      | 7   |
|         |        |      |     | 10
|----------        |     ---    |
|                  |            |
--------------------           ---

wc = 20
hc = 10
wi = 10
hi = 7

20/10 > 10/7 ==> (wi * hc/hi, hc) = (10 * 10/7, 10) = (100/7, 10) ~ (14.3, 10)
```
