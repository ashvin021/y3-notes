> Prewitt-x (moving average $\ast$ finite difference): $$\begin{bmatrix} 1 & 0 & -1 \\ 1 & 0 & -1 \\ 1 & 0 & -1\end{bmatrix} = \begin{bmatrix}0 & 1 & 0 \\ 0 & 1 & 0 \\ 0 & 1 & 0\end{bmatrix} \ast \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & -1 \\ 0 & 0 & 0\end{bmatrix}$$

- This can be applied along the horizontal or vertical axis, to obtain the central difference (gradient) along each axis.
- This is a separable filter.
- Prewitt-y is the transpose of Prewitt-x.