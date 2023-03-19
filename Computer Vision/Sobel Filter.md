>Sobel-x (weighted average $\ast$ finite difference): $$\begin{bmatrix}1 & 0 & -1 \\ 2 & 0 & -2 \\ 1 & 0 & -1\end{bmatrix} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 2 & 0 \\ 0 & 1 & 0\end{bmatrix} \ast \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & -1 \\ 0 & 0 & 0\end{bmatrix}$$
- This can be applied along the horizontal and vertical axes, just like the Prewitt filter.
- This is also a separable filter.
- Sobel-y is the transpose of Sobel-x.