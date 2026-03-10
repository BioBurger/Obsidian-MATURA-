

- Vektor je matematični objekt z **velikostjo** (dolžino) in **smerjo**
- Označimo ga z $\vec{a}$, zapišemo s koordinatami: $\vec{a}=(x,y)$ v ravnini ali $\vec{a}=(x,y,z)$ v prostoru

## Osnovni pojmi
- **Ničelni vektor**: $\vec{0}=(0,0)$ oz. $\vec{0}=(0,0,0)$ — nima smeri
- **Enotski vektor**: $|\vec{a}|=1$
- **Nasprotni vektor**: $-\vec{a}$ — enaka dolžina, nasprotna smer
- **Kolinearni vektorji**: ležijo na vzporednih premicah (vzporedni ali antiparalelni)
- **Koplanarni vektorji**: ležijo v isti ravnini

## Dolžina vektorja
$$|\vec{a}|=\sqrt{x^2+y^2} \quad \text{(ravnina)}$$
$$|\vec{a}|=\sqrt{x^2+y^2+z^2} \quad \text{(prostor)}$$

## Računske operacije

### Seštevanje in odštevanje
$$\vec{a}+\vec{b}=(x_1+x_2,\ y_1+y_2,\ z_1+z_2)$$
$$\vec{a}-\vec{b}=(x_1-x_2,\ y_1-y_2,\ z_1-z_2)$$

### Množenje s skalarjem
$$\lambda\vec{a}=(\lambda x,\ \lambda y,\ \lambda z)$$
- $\lambda>0$: ista smer
- $\lambda<0$: nasprotna smer
- $\lambda=0$: ničelni vektor

### Enotski vektor (normiranje)
$$\vec{e}_{a}=\frac{\vec{a}}{|\vec{a}|}$$

## Linearna kombinacija in neodvisnost
$$\vec{c}=\alpha\vec{a}+\beta\vec{b}$$
Vektorja $\vec{a}$ in $\vec{b}$ sta **linearno neodvisna**, če enačba
$$\alpha\vec{a}+\beta\vec{b}=\vec{0}$$
velja le za $\alpha=\beta=0$. Linearno neodvisna vektorja v ravnini tvorita **bazo** — vsak vektor v ravnini lahko zapišemo kot njuno linearno kombinacijo.

## Skalarni produkt

### Koordinatna oblika
$$\vec{a}\cdot\vec{b}=x_1 x_2+y_1 y_2+z_1 z_2$$

### Geometrijska oblika
$$\vec{a}\cdot\vec{b}=|\vec{a}|\cdot|\vec{b}|\cdot\cos\varphi$$

### Kot med vektorjema
$$\cos\varphi=\frac{\vec{a}\cdot\vec{b}}{|\vec{a}|\cdot|\vec{b}|}$$

### Lastnosti
- $\vec{a}\cdot\vec{b}=\vec{b}\cdot\vec{a}$ (komutativnost)
- $\vec{a}\cdot(\vec{b}+\vec{c})=\vec{a}\cdot\vec{b}+\vec{a}\cdot\vec{c}$ (distributivnost)
- $\vec{a}\cdot\vec{a}=|\vec{a}|^2$

### Pravokotnost in vzporednost
$$\vec{a}\perp\vec{b} \iff \vec{a}\cdot\vec{b}=0$$
$$\vec{a}\parallel\vec{b} \iff \vec{a}=\lambda\vec{b} \quad \text{za nek } \lambda\in\mathbb{R}$$

## Pravokotna projekcija

### Projekcija vektorja $\vec{a}$ na $\vec{b}$
$$\text{proj}_{\vec{b}}\vec{a}=\frac{\vec{a}\cdot\vec{b}}{|\vec{b}|^2}\cdot\vec{b}$$

### Dolžina projekcije
$$\left|\text{proj}_{\vec{b}}\vec{a}\right|=\frac{\vec{a}\cdot\vec{b}}{|\vec{b}|}=|\vec{a}|\cos\varphi$$

## Projekcija točke na premico

### Metoda 1 — vektorska (premica skozi $B$ in $C$, projiciramo točko $T$)
$$t=\frac{\vec{BT}\cdot\vec{BC}}{|\vec{BC}|^2}, \qquad T'=B+t\cdot\vec{BC}$$

### Metoda 2 — s premicami (priporočena na maturi)
1. Izračunaj enačbo premice $BC$ s smernim koeficientom $k$
2. Pravokotnica skozi $T$ ima smerni koeficient $k_\perp=-\dfrac{1}{k}$
3. Presečišče obeh premic je projekcija $T'$

## Zrcaljenje točke čez premico
Najprej izračunaj projekcijo $T'$, nato:
$$T''=2T'-T$$
Zrcalna slika leži na nasprotni strani premice, na enaki razdalji.

## Vektorski produkt (samo v prostoru)
$$\vec{a}\times\vec{b}=\begin{vmatrix}\vec{i}&\vec{j}&\vec{k}\\x_1&y_1&z_1\\x_2&y_2&z_2\end{vmatrix}=(y_1z_2-z_1y_2,\ z_1x_2-x_1z_2,\ x_1y_2-y_1x_2)$$

- Rezultat je vektor, **pravokoten na oba**
$$|\vec{a}\times\vec{b}|=|\vec{a}||\vec{b}|\sin\varphi$$
$$\vec{a}\parallel\vec{b} \iff \vec{a}\times\vec{b}=\vec{0}$$

### Ploščini
$$S_{\text{paralelograma}}=|\vec{a}\times\vec{b}|, \qquad S_{\text{trikotnika}}=\frac{1}{2}|\vec{a}\times\vec{b}|$$

## Uporaba v trikotniku

### Kosinusni izrek
$$c^2=a^2+b^2-2ab\cos\gamma$$

### Ploščina trikotnika
$$S=\frac{1}{2}|\vec{a}||\vec{b}|\sin\varphi$$

### Pravokotni trikotnik — očrtani krog
Hipotenuza je premer očrtanega kroga:
$$r=\frac{c}{2} \implies S_\bigcirc=\pi r^2=\frac{\pi c^2}{4}$$

### Dokaz pravokotnosti trikotnika $ABC$ s pravim kotom pri $A$
$$\vec{AB}\cdot\vec{AC}=0$$

> [!note] Za maturo — pogoste naloge
> - Izračun kota med vektorjema z $\cos\varphi$
> - Določanje kolinearnosti in pravokotnosti
> - Razstavljanje vektorja na komponente (projekcija)
> - Linearna kombinacija — določi $\alpha, \beta$
> - Projekcija točke na premico
> - Dokazovanje pravokotnosti trikotnika s skalarnim produktom
> - Ploščina trikotnika z vektorskim ali skalarnim produktom
> - Očrtani krog pravokotnega trikotnika
