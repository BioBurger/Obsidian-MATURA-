Kompleksna števila razširijo realna z imaginarno enoto $i$, kjer $i^2=-1$
	

## Osnovna oblika
$$z = a + bi, \quad a,b \in \mathbb{R}$$
- $a = \text{Re}(z)$: realni del
- $b = \text{Im}(z)$: imaginarni del
- **Konjugirano kompleksno število**: $\bar{z}=a-bi$

## Računanje

### Seštevanje / odštevanje
$$(a+bi)\pm(c+di)=(a\pm c)+(b\pm d)i$$

### Množenje
$$(a+bi)(c+di)=ac+adi+bci+bdi^2=(ac-bd)+(ad+bc)i$$

### Deljenje — množenje s konjugatom
$$\frac{a+bi}{c+di}=\frac{(a+bi)(c-di)}{(c+di)(c-di)}=\frac{(ac+bd)+(bc-ad)i}{c^2+d^2}$$

## Absolutna vrednost (modul)
$$|z|=\sqrt{a^2+b^2}$$
$$z\cdot\bar{z}=a^2+b^2=|z|^2$$

## Potence imaginarne enote
$$i^1=i,\quad i^2=-1,\quad i^3=-i,\quad i^4=1,\quad i^5=i,\ldots$$

> [!tip] Hitri izračun $i^n$
> Izračunaj ostanek $n \mod 4$:
> - ostanek 0 → $1$
> - ostanek 1 → $i$
> - ostanek 2 → $-1$
> - ostanek 3 → $-i$

## Gaussova ravnina
- Vsako kompleksno število $z=a+bi$ predstavimo kot točko $(a,b)$
- **Realna os**: $x$-os, **imaginarna os**: $y$-os
- Modul $|z|$ = razdalja od izhodišča

## Trigonometrična (polarna) oblika
$$z=r(\cos\varphi+i\sin\varphi)=r\,\text{cis}\,\varphi$$
- $r=|z|=\sqrt{a^2+b^2}$
- $\varphi=\arg(z)=\arctan\dfrac{b}{a}$ (upoštevamo kvadrant!)

### Pretvorba iz algebrske v polarno
$$a=r\cos\varphi, \quad b=r\sin\varphi$$

## Množenje in deljenje v polarni obliki
$$z_1\cdot z_2=r_1 r_2\,\text{cis}(\varphi_1+\varphi_2)$$
$$\frac{z_1}{z_2}=\frac{r_1}{r_2}\,\text{cis}(\varphi_1-\varphi_2)$$

## De Moivreov izrek
$$z^n=r^n(\cos(n\varphi)+i\sin(n\varphi))$$
$$\begin{aligned}
&\quad \text{Primer: } z=1+i,\ z^4=?\\
&\quad r=\sqrt{2},\ \varphi=\frac{\pi}{4}\\
&\quad z^4=(\sqrt{2})^4\left(\cos\pi+i\sin\pi\right)=4\cdot(-1)=-4
\end{aligned}$$

## Koreni kompleksnega števila
$$\sqrt[n]{z}=\sqrt[n]{r}\,\text{cis}\!\left(\frac{\varphi+2k\pi}{n}\right), \quad k=0,1,\ldots,n-1$$
- $n$-ti koren ima natanko $n$ rešitev

> [!note] Za maturo — tipične naloge
> - Računanje z algebrsko obliko (+, −, ·, /)
> - Pretvorba med algebrsko in polarno obliko
> - De Moivreov izrek — potenciranje
> - Iskanje $n$-tih korenov
