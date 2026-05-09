
## Trikotnik
- Vsota notranjih kotov: $\alpha+\beta+\gamma=180°$
- Zunanjи kot = vsota dveh neprileglih notranjih kotov

### Ploščina
$$S = \frac{a \cdot h_a}{2}$$

#### Heronova formula (ko poznamo vse tri stranice)
$$s=\frac{a+b+c}{2} \quad \text{(polobseg)}$$
$$S = \sqrt{s(s-a)(s-b)(s-c)}$$

#### Ploščina s kotom
$$S = \frac{1}{2}ab\sin\gamma = \frac{1}{2}bc\sin\alpha = \frac{1}{2}ac\sin\beta$$

### Sinusni izrek
$$\frac{a}{\sin\alpha}=\frac{b}{\sin\beta}=\frac{c}{\sin\gamma}=2R$$
- $R$ = polmer očrtane krožnice
- Uporabimo ko poznamo: **kot in nasprotno stranico** + še en element

### Kosinusni izrek
$$a^2=b^2+c^2-2bc\cos\alpha$$
$$b^2=a^2+c^2-2ac\cos\beta$$
$$c^2=a^2+b^2-2ab\cos\gamma$$
- Uporabimo ko poznamo: **vse 3 stranice** ali **2 stranici in vključeni kot**

### Pravokotni trikotnik
$$a^2+b^2=c^2 \quad (c = \text{hipotenuza})$$
$$\sin\alpha=\frac{a}{c}, \quad \cos\alpha=\frac{b}{c}, \quad \tan\alpha=\frac{a}{b}$$

### Vpisana in očrtana krožnica
$$r = \frac{S}{s} \quad \text{(polmer vpisane)}, \qquad R = \frac{abc}{4S} \quad \text{(polmer očrtane)}$$

---

## Štirikotniki

### Kvadrat (stranica $a$)
$$S=a^2, \quad o=4a$$
$$\text{Diagonala: } d=a\sqrt{2}$$

### Pravokotnik (stranici $a, b$)
$$S=ab, \quad o=2(a+b)$$
$$\text{Diagonala: } d=\sqrt{a^2+b^2}$$

### Paralelogram (stranici $a, b$, višina $h$, kota $\alpha, \beta$)
$$S=ah=ab\sin\alpha, \quad o=2(a+b)$$
$$d_1^2+d_2^2=2(a^2+b^2) \quad \text{(razmerje diagonal)}$$

### Romb (stranica $a$, diagonali $d_1, d_2$)
$$S=\frac{d_1 d_2}{2}=a^2\sin\alpha, \quad o=4a$$
$$a=\frac{\sqrt{d_1^2+d_2^2}}{2}$$

### Trapez (vzporedni stranici $a, c$, višina $h$)
$$S=\frac{(a+c)h}{2}$$
$$\text{Srednja premica: } m=\frac{a+c}{2} \Rightarrow S=m \cdot h$$

---

## Krog (polmer $r$, premer $d=2r$)
$$S=r^2\pi, \quad o=2r\pi=d\pi$$

### Krožni izsek (centralni kot $\varphi$ v radianih)
$$S_{\text{izsek}}=\frac{r^2\varphi}{2}, \quad l_{\text{loka}}=r\varphi$$
$$\text{V stopinjah: } S_{\text{izsek}}=\frac{r^2\pi\varphi°}{360°}$$

$$\text{Dolžina izseka: } l_{\text{izsek}}=\frac{r\pi\varphi°}{180°}$$
### Krožni odsek
$$S_{\text{odsek}}=\frac{r^2}{2}(\varphi-\sin\varphi)$$

### Krožni kolobar (polmera $R$ in $r$, $R>r$)
$$S=\pi(R^2-r^2)=\pi(R+r)(R-r)$$

> [!tip] Pretvorba kotov
> $$\varphi_{\text{rad}}=\varphi°\cdot\frac{\pi}{180}, \qquad \varphi°=\varphi_{\text{rad}}\cdot\frac{180}{\pi}$$
> Pomembni koti:
> | Stopinje | $0°$ | $30°$ | $45°$ | $60°$ | $90°$ | $180°$ | $360°$ |
> |---|---|---|---|---|---|---|---|
> | Radiani | $0$ | $\frac{\pi}{6}$ | $\frac{\pi}{4}$ | $\frac{\pi}{3}$ | $\frac{\pi}{2}$ | $\pi$ | $2\pi$ |

---

## Pravilni večkotniki (stranica $a$, $n$ stranic)
$$S=\frac{na^2}{4}\cot\frac{\pi}{n}, \quad o=na$$
$$\text{Polmer vpisane krožnice: } r=\frac{a}{2}\cot\frac{\pi}{n}$$
$$\text{Polmer očrtane krožnice: } R=\frac{a}{2\sin(\pi/n)}$$

> [!note] Za maturo — tipične naloge
> - Ploščina in obseg sestavljenih likov
> - Sinusni/kosinusni izrek v trikotniku
> - Krožni izsek in odsek
> - Vpisana/očrtana krožnica v trikotniku
