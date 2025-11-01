# === Discrete Chebyshev/Gram polynomials

The discrete Chebyshev polynomial $t_n^N(x)$ is a polynomial of degree $n$ in $x$, for $n = 0, 1, 2, ..., N-1$, constructed such that two polynomials of ***unequal degree*** are ***orthogonal*** with respect to the weight function:

\[
\begin{equation}
w(x) = \sum_{r = 0}^{N - 1}\delta(x - r)
\end{equation}
\]

with $\delta(\cdot)$ being the ***Dirac delta function***:

\[
\begin{equation}
\int_{-\infty}^{\infty} t_n^N(x)t_m^N(x)w(x)dx = 0;\quad n\ne m
\end{equation}
\]

The integral on the left is actually a sum because of the delta function:

\[
\begin{equation}
\sum_{r=0}^{N-1} t_n^N(r)t_m^N(r) = 0; \quad n \ne m
\end{equation}
\]

The polynomials are complete in the sense that:

\[
\begin{equation}
\sum_{n=0}^{N-1} t_n^N(r)t_n^N(s) = 0; \quad r \ne s
\end{equation}
\]

Chebyshev chose the normalization so that:

\[
\begin{equation}
\sum_{r=0}^{N-1}t_n^N(r)t_n^N(r) = \frac{N}{2n+1}\prod_{k=1}^n(N^2 - k^2)
\end{equation}
\]

This fixes the polynomials completely along with the sign convention:

\[
\begin{equation}
t_n^N(N-1) > 0
\end{equation}
\]

Because of the delta function, even though $t_n^N(x)$ is a polynomial in $x$, only it's ***values at a discrete set of points*** $x = 0, 1, 2, ..., N-1$ are ***of any significance***.