
- **Funkcija** $f: A \to B$ vsakemu elementu $x \in A$ priredi natanko en element $f(x) \in B$
- $A$: **definicijsko območje** $D_f$
- $B$: **zaloga vrednosti** $Z_f$

## Lastnosti funkcij

### Injektivnost (ena-ena)
$$f(x_1)=f(x_2) \Rightarrow x_1=x_2$$
Vsaka vrednost je dosežena **največ enkrat**.

### Surjektivnost (na)
$$\forall y \in B\ \exists x \in A: f(x)=y$$
Vsaka vrednost iz $B$ je dosežena **vsaj enkrat**.

### Bijektivnost
Funkcija je hkrati injektivna in surjektivna — obstaja inverzna funkcija.

## Inverzna funkcija
$$f^{-1}: B \to A, \quad f^{-1}(f(x))=x$$
- Graf $f^{-1}$ je zrcalna slika grafa $f$ čez premico $y=x$
- Postopek: zamenjaj $x$ in $y$, izrazi $y$

## Kompozitum
$$(g \circ f)(x)=g(f(x))$$
- Najprej $f$, potem $g$

## Soda in liha funkcija
$$\text{Soda: } f(-x)=f(x) \quad \text{(simetrija čez } y\text{-os)}$$
$$\text{Liha: } f(-x)=-f(x) \quad \text{(simetrija čez izhodišče)}$$

## Naraščanje in padanje
- **Naraščajoča** na $I$: $x_1<x_2 \Rightarrow f(x_1)<f(x_2)$
- **Padajoča** na $I$: $x_1<x_2 \Rightarrow f(x_1)>f(x_2)$

## Polinomi
$$p(x)=a_n x^n + a_{n-1}x^{n-1}+\ldots+a_1 x+a_0$$
- $n$: stopnja polinoma, $a_n \neq 0$: vodilni koeficient
- Polinom stopnje $n$ ima **največ $n$ realnih ničel**

### Ničle polinoma
- $x_0$ je ničla $\iff$ $p(x_0)=0$ $\iff$ $(x-x_0)$ je faktor polinoma
- **Hornerjeva shema**: učinkovito računanje vrednosti in deljenje polinoma

### Hornerjeva shema
$$p(x)=a_n x^n+\ldots+a_0 \text{ delimo z } (x-c):$$
$$\begin{array}{c|ccccc}
c & a_n & a_{n-1} & \cdots & a_1 & a_0 \\
  &     & ca_n    & \cdots &     & \\
\hline
  & a_n & b_{n-1} & \cdots & b_0 & r
\end{array}$$
- $r=p(c)$ je ostanek pri deljenju

### Kvadratna funkcija
$$f(x)=ax^2+bx+c, \quad a\neq 0$$
$$\text{Teme: } T=\left(-\frac{b}{2a},\ -\frac{D}{4a}\right), \quad D=b^2-4ac$$
$$x_{1,2}=\frac{-b\pm\sqrt{D}}{2a}$$
- $D>0$: dve realni ničli
- $D=0$: ena realna ničla (dvojna)
- $D<0$: ni realnih ničel

### Viètova izreka (za $ax^2+bx+c=0$)
$$x_1+x_2=-\frac{b}{a}, \qquad x_1\cdot x_2=\frac{c}{a}$$

## Racionalna funkcija
$$f(x)=\frac{p(x)}{q(x)}, \quad q(x)\neq 0$$
- $D_f=\{x\in\mathbb{R} \mid q(x)\neq 0\}$
- Navpična asimptota: ničle imenovalca (kjer števec $\neq 0$)

## Korenska funkcija
$$f(x)=\sqrt[n]{x}=x^{1/n}$$
- Za sode $n$: $D_f=[0,+\infty)$
- Za lihe $n$: $D_f=\mathbb{R}$

## Absolutna vrednost
$$|x|=\begin{cases}x & x\geq 0\\ -x & x<0\end{cases}$$
$$|x|=\sqrt{x^2}, \qquad |x|<a \iff -a<x<a$$

> [!note] Za maturo — tipične naloge
> - Določi $D_f$ in $Z_f$
> - Nariši in analiziraj graf
> - Ničle in ekstremi polinoma
> - Sestavi polinom iz danih lastnosti
> - Inverzna funkcija — postopek in graf
