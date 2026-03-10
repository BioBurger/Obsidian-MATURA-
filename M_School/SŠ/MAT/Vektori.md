- Vektor je matematični objekt z **velikostjo** (dolžino) in **smerjo**
- Označimo ga z $\vec{a}$ ali **a**, zapišemo s koordinatami: $\vec{a}=(x, y)$ v ravnini ali $\vec{a}=(x, y, z)$ v prostoru

## Osnovni pojmi
- **Ničelni vektor**: $\vec{0}=(0,0,0)$ — nima smeri
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
- Če $\lambda>0$: ista smer; če $\lambda<0$: nasprotna smer

### Enotski vektor (normiranje)
$$\vec{e}_{a}=\frac{\vec{a}}{|\vec{a}|}$$

## Linearna kombinacija in neodvisnost
$$\vec{c}=\alpha\vec{a}+\beta\vec{b}$$
- Vektorja $\vec{a}$ in $\vec{b}$ sta **linearno neodvisna**, če $\alpha\vec{a}+\beta\vec{b}=\vec{0}$ velja le za $\alpha=\beta=0$
- Linearno neodvisna vektorja v ravnini tvorita **bazo**

## Skalarni produkt
$$\vec{a}\cdot\vec{b}=x_1 x_2+y_1 y_2+z_1 z_2$$

### Geometrijska oblika
$$\vec{a}\cdot\vec{b}=|\vec{a}|\cdot|\vec{b}|\cdot\cos\varphi$$

### Kot med vektorjema
$$\cos\varphi=\frac{\vec{a}\cdot\vec{b}}{|\vec{a}|\cdot|\vec{b}|}$$

### Lastnosti
- $\vec{a}\cdot\vec{b}=\vec{b}\cdot\vec{a}$ (komutativnost)
- $\vec{a}\cdot(\vec{b}+\vec{c})=\vec{a}\cdot\vec{b}+\vec{a}\cdot\vec{c}$ (distributivnost)
- $\vec{a}\cdot\vec{a}=|\vec{a}|^2$

> [!tip] Pravokotnost in vzporednost
> - $\vec{a}\perp\vec{b} \iff \vec{a}\cdot\vec{b}=0$
> - $\vec{a}\parallel\vec{b} \iff \vec{a}=\lambda\vec{b}$ za nek $\lambda\in\mathbb{R}$

## Pravokotna projekcija
$$\text{proj}_{\vec{b}}\vec{a}=\frac{\vec{a}\cdot\vec{b}}{|\vec{b}|^2}\cdot\vec{b}$$
$$\text{Dolžina projekcije: }\frac{\vec{a}\cdot\vec{b}}{|\vec{b}|}=|\vec{a}|\cos\varphi$$

## Uporaba v trikotniku

### Kosinusni izrek (z vektorji)
$$c^2=a^2+b^2-2ab\cos\gamma$$

### Ploščina trikotnika
$$S=\frac{1}{2}|\vec{a}||\vec{b}|\sin\varphi$$

> [!note] Za maturo
> Pogoste naloge:
> - Izračun kota med vektorjema z $\cos\varphi$
> - Določanje kolinearnosti/pravokotnosti
> - Razstavljanje vektorja na komponente (projekcija)
> - Linearna kombinacija — določi $\alpha, \beta$
