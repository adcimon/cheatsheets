# References

Made with [CodeCogs Equation Editor](https://www.codecogs.com/eqnedit.php).

Translation.
```
T(\overrightarrow{t}) = \begin{bmatrix}
1 & 0 & 0 & t_{x} \\
0 & 1 & 0 & t_{y} \\
0 & 0 & 1 & t_{z} \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
```

Rotation.
```
R_{x}(\theta ) = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & cos\theta  & -sin\theta  & 0 \\
0 & sin\theta  & cos\theta  & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}

R_{y}(\theta ) = \begin{bmatrix}
cos\theta  & 0 & sin\theta  & 0 \\
0 & 1 & 0 & 0 \\
-sin\theta  & 0 & cos\theta  & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}

R_{z}(\theta ) = \begin{bmatrix}
cos\theta  & -sin\theta  & 0 & 0 \\
sin\theta  & cos\theta  & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
```

Scaling.
```
S(\overrightarrow{s}) = \begin{bmatrix}
s_{x} & 0 & 0 & 0 \\
0 & s_{y} & 0 & 0 \\
0 & 0 & s_{z} & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
```

Shearing.
```
H = \begin{bmatrix}
1 & s_{x}^{y} & s_{x}^{z} & 0 \\
s_{y}^{x} & 1 & s_{y}^{z} & 0 \\
s_{z}^{x} & s_{z}^{y} & 1 & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
```