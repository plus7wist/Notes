// Latex 笔记

## 符号表

|$\mathfrak{Code}$|$\mathfrak{Display}$|
|:--:|:--:|
|`a_i`|$a_i$|
|`p^n`|$p^n$|
|`\sqrt{x}`|$\sqrt{x}$|
|`\sqrt[n]{x}`|$\sqrt[n]{x}$|
|`\overline{x}`|$\overline{x}$|
|`\underline{x}`|$\underline{x}$|
|`\overbrace{x}`|$\overbrace{x}$|
|`\underbrace{x}`|$\underbrace{x}$|
|`vec{x}`|$\vec{x}$|
|`\frac{1}{2}`|$\frac{1}{2}$|
|`\int`|$\int$|
|`\oint`|$\oint$|
|`\sum`|$\sum$|
|`\prod`|$\prod$|
|`\alpha`|$\alpha$|
|`\beta`|$\beta$|
|`\gamma`|$\gamma$|
|`\phi`|$\phi$|
|`\varphi`|$\varphi$|
|`\le`|$\le$|
|`\ge`|$\ge$|
|`\ne`|$\ne$|
|`\ll`|$\ll$|
|`\gg`|$\gg$|
|`\equiv`|$\equiv$|
|`\sim`|$\sim$|
|`\approx`|$\approx$|
|`\in`|$\in$|
|`\notin`|$\notin$|
|`\pm`|$\pm$|
|`\mp`|$\mp$|
|`\times`|$\times$|
|`\div`|$\div$|
|`\dots`|$\dots$|
|`\angle`|$\angle$|
|`\forall`|$\forall$|
|`\exists`|$\exists$|
|`\triangle`|$\triangle$|
|`\odot`|$\odot$|
|`\leqslant`|$\leqslant$|
|`\geqslant`|$\geqslant$|
|`\mathcal{abcABC}`|$\mathcal{abcABC}$|
|`\mathbb{abcABC}`|$\mathbb{abcABC}$|
|`\mathfrak{abcABC}`|$\mathfrak{abcABC}$|
|`\mathbf{abcABC}`|$\mathbf{abcABC}$|
|`\mathrm{abcABC}`|$\mathrm{abcABC}$|
|`abcABC`|$abcABC$|
|`a bc \quad def`|$a bc \quad def$|
|`a bc \ def`|$a bc \ def$|
|`a bc \qquad def`|$abc \qquad def$|
|`a\mod b\\c\!\mod d`|$a\mod b\\c\!\mod d$|
|`\text{a b}`|$\text{a b}$|

## 垂直对齐

```
\mathbf{M} =
    \left(
        \begin{array}{ccc}
            x_{11} & x_{12} & \ldots \\
            x_{21} & x_{22} & \ldots \\
            \vdots & \vdots & \ddots
        \end{array}
    \right)
```

$$
\mathbf{M} =
    \left(
        \begin{array}{ccc}
            x_{11} & x_{12} & \ldots \\
            x_{21} & x_{22} & \ldots \\
            \vdots & \vdots & \ddots
        \end{array}
    \right)
$$

```
f(x) =
    \left\{
        \begin{array}{ll}
            a & case 1\\
            b & case 2\\
            c & otherwise
        \end{array}
    \right.
```

$$
f(x) =
    \left\{
        \begin{array}{ll}
            a & case 1\\
            b & case 2\\
            c & otherwise
        \end{array}
    \right.
$$

```
\left(
    \begin{array}{c|c}
        1 & 2 \\
        \hline
        3 & 4
    \end{array}
\right)
```

$$
\left(
    \begin{array}{c|c}
        1 & 2 \\
        \hline
        3 & 4
    \end{array}
\right)
$$



```
\begin{eqnarray*}
    f(x) & = & \cos x \\
    f’(x) & = & -\sin x \\
    \int_{0}^{x} f(y)dy & = & \sin x
\end{eqnarray*}
```

$$
\begin{eqnarray*}
    f(x) & = & \cos x \\
    f’(x) & = & -\sin x \\
    \int_{0}^{x} f(y)dy & = & \sin x
\end{eqnarray*}
$$

```
\begin{eqnarray}
    f(x) & = & \cos x \\
    f’(x) & = & -\sin x \\
    \int_{0}^{x} f(y)dy & = & \sin x
\end{eqnarray}
```

$$
\begin{eqnarray}
    f(x) & = & \cos x \\
    f’(x) & = & -\sin x \\
    \int_{0}^{x} f(y)dy & = & \sin x
\end{eqnarray}
$$
