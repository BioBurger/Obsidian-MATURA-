- Integral je "obratna operacija" od odvajanja — iščemo funkcijo, katere odvod je znana funkcija.

## Nedoločeni integral

### Definicija
$$\int f(x)\,dx = F(x) + C$$
kjer je $F'(x)=f(x)$ in $C\in\mathbb{R}$ integralna konstanta.

## Tabela osnovnih integralov

| Funkcija $f(x)$ | Integral $\int f(x)\,dx$ |
|---|---|
| $x^n\ (n\neq-1)$ | $\dfrac{x^{n+1}}{n+1}+C$ |
| $\dfrac{1}{x}$ | $\ln|x|+C$ |
| $e^x$ | $e^x+C$ |
| $a^x$ | $\dfrac{a^x}{\ln a}+C$ |
| $\sin x$ | $-\cos x+C$ |
| $\cos x$ | $\sin x+C$ |
| $\dfrac{1}{\cos^2 x}$ | $\tan x+C$ |
| $\dfrac{1}{\sin^2 x}$ | $-\cot x+C$ |
| $\dfrac{1}{\sqrt{1-x^2}}$ | $\arcsin x+C$ |
| $\dfrac{1}{1+x^2}$ | $\arctan x+C$ |

## Pravila integriranja

### Linearnost
$$\int (af(x)+bg(x))\,dx = a\int f(x)\,dx + b\int g(x)\,dx$$

### Integracija kompozituma (substitucija v osnovi)
$$\int f(ax+b)\,dx = \frac{1}{a}F(ax+b)+C$$
$$\begin{aligned}
&\quad \text{Primer: }\int \sin(3x)\,dx = -\frac{1}{3}\cos(3x)+C
\end{aligned}$$

## Metoda substitucije
$$\int f(g(x))\cdot g'(x)\,dx = \int f(t)\,dt, \quad t=g(x)$$
$$\begin{aligned}
&\quad \text{Primer: }\int 2x\cdot e^{x^2}\,dx\\
&\quad t=x^2 \Rightarrow dt=2x\,dx\\
&\quad \int e^t\,dt = e^t+C = e^{x^2}+C
\end{aligned}$$

## Integracija per partes
$$\int u\,dv = uv - \int v\,du$$
$$\int u(x)\cdot v'(x)\,dx = u(x)\cdot v(x) - \int u'(x)\cdot v(x)\,dx$$

> [!tip] Kdaj izbrati $u$ in $dv$?
> Pravilo **ILATE** — $u$ izberemo po vrstnem redu:
> **I**nverz trig. → **L**ogaritem → **A**lgebrična (polinomi) → **T**rigonometrična → **E**ksponentna
> $$\begin{aligned}
> &\quad \text{Primer: }\int x\cdot e^x\,dx\\
> &\quad u=x,\ dv=e^x\,dx \Rightarrow du=dx,\ v=e^x\\
> &\quad = xe^x - \int e^x\,dx = xe^x - e^x + C = e^x(x-1)+C
> \end{aligned}$$

## Integracija racionalnih funkcij
$$\frac{P(x)}{Q(x)}: \text{ če } \deg P \geq \deg Q \Rightarrow \text{najprej deljenje polinomov}$$

### Razstavljanje na parcialne ulomke
$$\frac{1}{(x-a)(x-b)}=\frac{A}{x-a}+\frac{B}{x-b}$$
$$\begin{aligned}
&\quad \text{Primer: }\int\frac{1}{x^2-1}\,dx = \int\frac{1}{(x-1)(x+1)}\,dx\\
&\quad = \int\left(\frac{1/2}{x-1}-\frac{1/2}{x+1}\right)dx\\
&\quad = \frac{1}{2}\ln|x-1|-\frac{1}{2}\ln|x+1|+C
\end{aligned}$$

## Določeni integral

### Definicija (Newton-Leibnizova formula)
$$\int_a^b f(x)\,dx = F(b)-F(a) = \bigl[F(x)\bigr]_a^b$$

### Lastnosti
$$\int_a^b f(x)\,dx = -\int_b^a f(x)\,dx$$
$$\int_a^b f(x)\,dx = \int_a^c f(x)\,dx + \int_c^b f(x)\,dx$$
$$\int_a^a f(x)\,dx = 0$$

## Geometrijske uporabe

### Ploščina med grafom in osjo $x$
$$S=\int_a^b |f(x)|\,dx$$
- Kjer je $f(x)<0$, vzamemo absolutno vrednost (ploščina je vedno pozitivna!)

### Ploščina med dvema grafoma
$$S=\int_a^b |f(x)-g(x)|\,dx$$

### Prostornina vrtenine okoli osi $x$
$$V=\pi\int_a^b \bigl[f(x)\bigr]^2\,dx$$

> [!note] Za maturo — tipične naloge
> - Izračun nedoločenega integrala (substitucija, per partes)
> - Določeni integral z Newton-Leibnizom
> - Ploščina lika omejenega z grafoma dveh funkcij
> - Prostornina vrtenine
