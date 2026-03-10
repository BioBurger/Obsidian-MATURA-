- Geometrijsko zaporedje je zaporedje števil, kjer je količnik dveh zaporednih členov vedno konstanten in različen od nič.

$$\begin{aligned}
\text{Količnik: } q=\frac{a_{n+1}}{a_{n}}\\
\text{Splošni člen: } a_{n}=a_{1}\cdot q^{n-1}\\
\text{Geometrijska sredina: } a,b>0 \rightarrow \sqrt{a\cdot b}
\end{aligned}$$

## Končna geometrijska vrsta
$$S_{n}=a_{1}+a_{1}\cdot q+a_{1}\cdot q^2+\dots+a_{1}\cdot q^{n-1}$$
$$S_{n}=\frac{a_{1}(q^n-1)}{q-1}, \quad q\neq1$$

## Neskončna geometrijska vrsta
$$\text{Konvergira, če } |q|<1:$$
$$S=\frac{a_{1}}{1-q}$$

> [!tip] Primerjava z aritmetičnim zaporedjem
> | | Aritmetično | Geometrijsko |
> |---|---|---|
> | Lastnost | Stalna razlika $d$ | Stalni količnik $q$ |
> | Splošni člen | $a_1+(n-1)d$ | $a_1 \cdot q^{n-1}$ |
> | Vsota | $\frac{n}{2}(2a_1+(n-1)d)$ | $\frac{a_1(q^n-1)}{q-1}$ |
