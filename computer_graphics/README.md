# Computer Graphics

## Letterbox

Image data: (wi, hi) and define ri = wi / hi<br>
Screen resolution: (ws, hs) and define rs = ws / hs
```
rs > ri ? (wi * hs/hi, hs) : (ws, hi * ws/wi)
```

Example.
```
|------------------|
    10
|---------|

--------------------     ---   ---
|         |        |      | 7   |
|         |        |      |     | 10
|----------        |     ---    |
|                  |            |
--------------------           ---

ws = 20
hs = 10
wi = 10
hi = 7

20/10 > 10/7 ==> (wi * hs/hi, hs) = (10 * 10/7, 10) = (100/7, 10) ~ (14.3, 10)
```

Center the image.
```
top = (hs - hnew)/2
left = (ws - wnew)/2
```
