- Stožnice so presečišča ravnine s stožcem: **krog, elipsa, hiperbola, parabola**

## Krog
$$\text{Enačba s središčem }(p,q)\text{ in polmerom }r:$$
$$(x-p)^2+(y-q)^2=r^2$$

## Elipsa
$$\frac{x^2}{a^2}+\frac{y^2}{b^2}=1, \quad a>b>0$$

- **Središče**: $(0,0)$
- **Polosi**: $a$ (glavna, po $x$), $b$ (stranska, po $y$)
- **Gorišči**: $F_{1,2}=(\pm c, 0)$, kjer $c=\sqrt{a^2-b^2}$
- **Definicija**: $|PF_1|+|PF_2|=2a$ za vsako točko $P$ na elipsi
- **Ekscentričnost**: $e=\dfrac{c}{a} \in (0,1)$

### Elipsa s središčem $(p,q)$
$$\frac{(x-p)^2}{a^2}+\frac{(y-q)^2}{b^2}=1$$

### Če je $b>a$: gorišča na osi $y$
$$F_{1,2}=(0, \pm c), \quad c=\sqrt{b^2-a^2}$$

## Hiperbola
$$\frac{x^2}{a^2}-\frac{y^2}{b^2}=1$$

- **Gorišči**: $F_{1,2}=(\pm c, 0)$, kjer $c=\sqrt{a^2+b^2}$
- **Definicija**: $\bigl||PF_1|-|PF_2|\bigr|=2a$ za vsako točko $P$ na hiperboli
- **Asimptoti**: $y=\pm\dfrac{b}{a}x$
- **Ekscentričnost**: $e=\dfrac{c}{a}>1$

### Hiperbola s središčem $(p,q)$
$$\frac{(x-p)^2}{a^2}-\frac{(y-q)^2}{b^2}=1$$

### Enačna hiperbola
$$xy=k \quad (k\neq 0)$$
- Asimptoti sta koordinatni osi

## Parabola
$$y=ax^2+bx+c \quad \text{ali v temenska oblika:}$$
$$y=a(x-p)^2+q$$

- **Teme**: $(p,q)$
- **Gorišče**: $F=\left(p,\ q+\dfrac{1}{4a}\right)$
- **Direktrisa**: $y=q-\dfrac{1}{4a}$
- **Definicija**: $|PF|=d(P,\text{direktrisa})$ za vsako točko $P$ na paraboli
- $a>0$: parabola se odpira navzgor; $a<0$: navzdol

### Parabola z vodoravno osjo
$$x=a(y-q)^2+p$$

## Tangente na stožnice

### Tangenta na krog $(x-p)^2+(y-q)^2=r^2$ v točki $T(x_0,y_0)$
$$(x_0-p)(x-p)+(y_0-q)(y-q)=r^2$$

### Tangenta na elipso $\dfrac{x^2}{a^2}+\dfrac{y^2}{b^2}=1$ v točki $T(x_0,y_0)$
$$\frac{x_0 x}{a^2}+\frac{y_0 y}{b^2}=1$$

### Tangenta na hiperbolo $\dfrac{x^2}{a^2}-\dfrac{y^2}{b^2}=1$ v točki $T(x_0,y_0)$
$$\frac{x_0 x}{a^2}-\frac{y_0 y}{b^2}=1$$

> [!tip] Prepoznavanje stožnic iz splošne enačbe
> Splošna enačba: $Ax^2+Bxy+Cy^2+Dx+Ey+F=0$
> - $A=C$, $B=0$: **krog**
> - $A\neq C$, isti predznak, $B=0$: **elipsa**
> - Različna predznaka, $B=0$: **hiperbola**
> - $A=0$ ali $C=0$ (ne oba): **parabola**

> [!note] Za maturo — tipične naloge
> - Določi gorišča, polosi, asimptote iz enačbe
> - Zapiši enačbo stožnice iz podanih lastnosti
> - Najdi presečišča stožnice s premico
> - Enačba tangente v dani točki
