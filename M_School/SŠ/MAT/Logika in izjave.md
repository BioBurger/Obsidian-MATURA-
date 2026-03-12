
- **Izjava** je trditev, ki je bodisi resnična (R) bodisi napačna (N)

## Logični vezniki

| Veznik | Simbol | Branje | Resnična ko |
|---|---|---|---|
| Negacija | $\neg A$ | ne $A$ | $A$ je napačna |
| Konjunkcija | $A \wedge B$ | $A$ in $B$ | oba resnična |
| Disjunkcija | $A \vee B$ | $A$ ali $B$ | vsaj eden resničen |
| Implikacija | $A \Rightarrow B$ | če $A$, potem $B$ | ni mogoče R→N |
| Ekvivalenca | $A \Leftrightarrow B$ | $A$ natanko tedaj ko $B$ | oba enaka |

## Resničnostna tabela

| $A$ | $B$ | $\neg A$ | $A\wedge B$ | $A\vee B$ | $A\Rightarrow B$ | $A\Leftrightarrow B$ |
|---|---|---|---|---|---|---|
| R | R | N | R | R | R | R |
| R | N | N | N | R | N | N |
| N | R | R | N | R | R | N |
| N | N | R | N | N | R | R |

> [!tip] Implikacija
> $A \Rightarrow B$ je napačna **samo** kadar je $A$ resnična in $B$ napačna.

## Tavtologija in protislovje
- **Tavtologija**: izjava, ki je vedno resnična (npr. $A \vee \neg A$)
- **Protislovje**: izjava, ki je vedno napačna (npr. $A \wedge \neg A$)

## Kontraponiranje
$$A \Rightarrow B \iff \neg B \Rightarrow \neg A$$
- Implikacija in njena **kontraponirana** oblika sta enakovredni

## De Morganova zakona
$$\neg(A \wedge B) \iff \neg A \vee \neg B$$
$$\neg(A \vee B) \iff \neg A \wedge \neg B$$

## Kvantifikatorji
$$\forall x: P(x) \quad \text{— za vse } x \text{ velja } P(x)$$
$$\exists x: P(x) \quad \text{— obstaja } x\text{, za katerega velja } P(x)$$

### Negacija kvantifikatorjev
$$\neg(\forall x: P(x)) \iff \exists x: \neg P(x)$$
$$\neg(\exists x: P(x)) \iff \forall x: \neg P(x)$$

> [!note] Za maturo — tipične naloge
> - Določi resničnost sestavljene izjave
> - Zapiši negacijo izjave z kvantifikatorji
> - Preveri ali je izjava tavtologija
> - Kontraponiranje implikacije
