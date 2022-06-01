# Computer Graphics

[Computer graphics](https://en.wikipedia.org/wiki/Computer_graphics_(computer_science)) is a sub-field of computer science which studies methods for digitally synthesizing and manipulating visual content.

## Index

* [Transformation Matrices](#transformation-matrices)
  * [Translation Matrix](#translation-matrix)
  * [Rotation Matrix](#rotation-matrix)
  * [Scaling Matrix](#scaling-matrix)
  * [Shearing Matrix](#shearing-matrix)
* [Algorithms](#algorithms)
  * [Letterbox](#letterbox)
* [References](#references)

## Transformation Matrices

[Transformation matrices](https://en.wikipedia.org/wiki/Transformation_matrix) are a type of matrices that represent [linear transformations](https://en.wikipedia.org/wiki/Linear_map). [Affine transformations](https://en.wikipedia.org/wiki/Affine_transformation) are transformations that preserve lines and parallelism but not necessarily distances and angles.

### Translation Matrix

Translation is a transformation that moves objects to a position.

<p align="center"><img align="center" width="40%" height="40%" src="assets/translation_matrix.svg"></p>

### Rotation Matrix

[Rotation](https://en.wikipedia.org/wiki/Rotation_matrix) is a transformation that moves objects relative to an axis by an angle θ.

<p align="center"><img align="center" width="40%" height="40%" src="assets/rotationx_matrix.svg"></p>
<p align="center"><img align="center" width="40%" height="40%" src="assets/rotationy_matrix.svg"></p>
<p align="center"><img align="center" width="40%" height="40%" src="assets/rotationz_matrix.svg"></p>

### Scaling Matrix

[Scaling](https://en.wikipedia.org/wiki/Scaling_(geometry)) is a transformation that enlarges (increases) or shrinks (diminishes) objects by a scale factor.

<p align="center"><img align="center" width="40%" height="40%" src="assets/scaling_matrix.svg"></p>

### Shearing Matrix

[Shearing](https://en.wikipedia.org/wiki/Shear_mapping) is a transformation that skews the coordinate space, stretching it nonuniformly. Areas and volumes are preserved but angles are not.

<p align="center"><img align="center" width="40%" height="40%" src="assets/shearing_matrix.svg"></p>

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

## References

* [Matrices in Computer Graphics](https://vitaminac.github.io/Matrices-in-Computer-Graphics/)
* [Why are 2D vector graphics so much harder than 3D?](https://blog.mecheye.net/2019/05/why-is-2d-graphics-is-harder-than-3d-graphics/)
