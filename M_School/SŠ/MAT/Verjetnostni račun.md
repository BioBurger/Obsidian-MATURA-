## Osnovni pojmi
- Verjetnost se zapiše s $P(A)$ — v **%**, decimalni vrednosti ali ulomku
- **Verjetnost** je področje matematike, ki se ukvarja s preučevanjem naključnih dogodkov.

**Poskus** je aktivnost, ki jo izvedemo vedno na enak način in pri enakih pogojih.

**Dogodek** je pojav, ki se pri danem poskusu lahko zgodi ali pa ne. Delimo jih na:
- **Gotovi (G)** — se zagotovo zgodi
- **Nemogoči (N)** — se ne more zgoditi
- **Slučajni (A, B, …)** — se lahko zgodi ali ne

### Relacije med dogodki

| Relacija | Opis | Zapis |
|---|---|---|
| **biti združljiv** z dogodkom | Dogodek $A$ je združljiv z $B$, ko se lahko zgodita hkrati. | |
| **biti način** dogodka | Dogodek $A$ je način dogodka $B$, če iz $A$ sledi $B$. | $A\subset B$ |
| **biti enak** dogodku | $A$ in $B$ sta enaka, ko se vsakokrat zgodita hkrati. | $A=B$ |

### Računske operacije z dogodki

| Zapis | Operacija | Branje | Opis |
|---|---|---|---|
| $A'$ | nasprotni dogodek | ne $A$ | Zgodi se, če se $A$ ne zgodi. |
| $A\cup B$ | vsota dogodkov | $A$ ali $B$ | Zgodi se, če se zgodi vsaj eden. |
| $A\setminus B$ | razlika dogodkov | $A$ in ne $B$ | Zgodi se $A$, ne pa $B$. |
| $A\cap B$ | produkt dogodkov | $A$ in $B$ | Zgodita se oba hkrati. |

### Elementarni in sestavljeni dogodki
- **Elementarni dogodki**: zgodijo se na en sam način; so med seboj nezdružljivi.
- **Sestavljeni dogodki**: zgodijo se na več načinov; zapišemo jih kot vsoto elementarnih.
- **Vzorčni prostor**: množica vseh elementarnih dogodkov danega poskusa.
- **Popoln sistem dogodkov**: množica dogodkov, kjer se ob vsaki ponovitvi zgodi natanko eden.

## Verjetnost dogodka
Vzorčni prostor je **simetričen**, če so vsi elementarni dogodki enako verjetni.
$$P(A)=\frac{m}{n}$$
kjer je $m$ število ugodnih izidov in $n$ skupno število vseh izidov.

### Aksiomi verjetnosti
1. $P(A) \geq 0$
2. $P(G) = 1$
3. Če $A\cap B = \emptyset$: $P(A\cup B) = P(A) + P(B)$

## Računanje verjetnosti
### Lastnosti
1. $P(N) = 0$
2. $P(A) + P(A') = 1$
3. Če $A\subset B$: $P(A) \leq P(B)$
4. $P(A) \leq 1$
5. $P(A - B) = P(A) - P(A\cap B)$
6. $P(A\cup B) = P(A) + P(B) - P(A\cap B)$

## Pogojna verjetnost
$$P(A|B)=\frac{P(A\cap B)}{P(B)}, \quad P(B)>0$$
- Verjetnost dogodka $A$, če je $B$ že nastopil.

## Neodvisni dogodki
Dogodka $A$ in $B$ sta **neodvisna**, če:
$$P(A\cap B)=P(A)\cdot P(B)$$
