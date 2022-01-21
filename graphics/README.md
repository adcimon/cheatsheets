# Computer Graphics

## Letterbox

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

To center the image.
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
