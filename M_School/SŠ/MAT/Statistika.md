
## Osnovni pojmi
- **Statistična enota**: posamezni objekt opazovanja
- **Statistična spremenljivka**: lastnost, ki jo merimo
- **Populacija**: celotna množica enot
- **Vzorec**: izbrani del populacije

## Mere srednje vrednosti

### Aritmetična sredina
$$\bar{x}=\frac{x_1+x_2+\ldots+x_n}{n}=\frac{1}{n}\sum_{i=1}^n x_i$$

### Utežena aritmetična sredina
$$\bar{x}=\frac{\sum_{i=1}^k f_i x_i}{\sum_{i=1}^k f_i}$$
kjer je $f_i$ frekvenca vrednosti $x_i$.

### Mediana
- Vrednost na sredini urejenega zaporedja
- $n$ lih: $\tilde{x}=x_{\frac{n+1}{2}}$
- $n$ sod: $\tilde{x}=\frac{x_{\frac{n}{2}}+x_{\frac{n}{2}+1}}{2}$

### Modus
- Najpogosteje pojavljena vrednost

## Mere razpršenosti

### Varianca
$$\sigma^2=\frac{1}{n}\sum_{i=1}^n (x_i-\bar{x})^2=\frac{1}{n}\sum_{i=1}^n x_i^2-\bar{x}^2$$

### Standardni odklon
$$\sigma=\sqrt{\sigma^2}$$

### Razmik (rang)
$$R=x_{\max}-x_{\min}$$

## Relativna frekvenca
$$f_i^{\text{rel}}=\frac{f_i}{n}, \qquad \sum f_i^{\text{rel}}=1$$

## Prikaz podatkov

### Frekvenčna tabela

| Vrednost $x_i$ | Frekvenca $f_i$ | Rel. frekvenca $f_i^{\text{rel}}$ | Kum. frekvenca |
|---|---|---|---|
| ... | ... | ... | ... |

### Grafični prikazi
- **Stolpčni diagram**: diskretni podatki
- **Histogram**: zvezni podatki v razredih
- **Krožni diagram**: deleži celote
- **Škatlasti diagram (box plot)**: $Q_1$, mediana, $Q_3$, min, max

## Kvartili
$$Q_1 \text{: mediana spodnje polovice}$$
$$Q_2 = \tilde{x} \text{: mediana}$$
$$Q_3 \text{: mediana zgornje polovice}$$
$$\text{Interkvartilni razmik: } IQR=Q_3-Q_1$$

## Korelacija
- Meri **linearno povezanost** dveh spremenljivk
- **Pearsonov korelacijski koeficient** $r \in [-1, 1]$:
  - $r \approx 1$: močna pozitivna korelacija
  - $r \approx -1$: močna negativna korelacija
  - $r \approx 0$: ni linearne korelacije

## Linearna regresija
$$y = kx + n$$
$$k=\frac{\sum(x_i-\bar{x})(y_i-\bar{y})}{\sum(x_i-\bar{x})^2}, \qquad n=\bar{y}-k\bar{x}$$

> [!note] Za maturo — tipične naloge
> - Izračun $\bar{x}$, $\tilde{x}$, modusa
> - Izračun variance in standardnega odklona
> - Branje in sestavljanje frekvenčnih tabel
> - Interpretacija škatlastega diagrama
> - Linearna regresija — izračun in interpretacija
