## **OSNOVNI POJMI**
- Napišemo ga s P(A)
- Zapiše se ga v **%, decimalni vrednosti ,ulomku**
- **Verjetnost** je področje matematike, ki se ukvarja s preučevanjem naključnih dogodkov.  
  
**Poskus** je aktivnost, ki jo izvedemo vedno na enak način in pri enakih pogojih.  
  
**Dogodek** je pojav, ki se pri danem poskusu lahko zgodi ali pa ne. Dogodke delimo na: gotove (G), nemogoče (N) in slučajne (A, B,…).

_Primeri_

V množici dogodkov danega poskusa imamo **tri relacije**.

|   |   |   |
|---|---|---|
|Relacija|Opis|Zapis|
|**biti združljiv** z dogodkom|Dogodek _A_ je združljiv z dogodkom _B_ natanko tedaj, ko se lahko zgodita hkrati.||
|**biti način** dogodka|Dogodek _A_ je način dogodka _B_, če se vsakokrat, ko se zgodi _A_, zagotovo zgodi tudi _B_.|_A_⊂_B_|
|**biti enak** dogodku|Dogodek _A_ je enak dogodku _B_ natanko tedaj, ko se vsakokrat zgodita hkrati.|_A_=_B_|

_Primeri_

Z dogodki danega poskusa tudi računamo. Računske operacije ustrezajo računanju z množicami.  
  

|   |   |   |   |
|---|---|---|---|
|Zapis|Operacija|Branje|Opis|
|_A_′|nasprotni dogodek|ne _A_|Nasprotni dogodek se zgodi, če se _A_ ne zgodi.|
|_A_∪_B_|vsota dogodkov|_A_ ali _B_|Dogodek _A_∪_B_ se zgodi, če se zgodi prvi ali drugi dogodek.|
|_A_∖_B, A-B_|razlika dogodkov|_A_ in ne _B_|Dogodek _A_∖_B_ se zgodi, če se zgodi prvi in ne drugi dogodek.|
|_A_∩_B_|produkt dogodkov|_A_ in _B_|Dogodek _A_∩_B_ se zgodi, če se zgodita prvi in drugi dogodek hkrati.|

_Primeri_

Dogodke, ki se zgodijo na en sam način, imenujemo **elementarni dogodki** ali izidi poskusa. Ti dogodki so med seboj nezdružljivi. Iz njih z operatorji tvorimo **sestavljene dogodke**.

Množico vseh izidov danega poskusa imenujemo **vzorčni prostor poskusa.** Vsak dogodek danega poskusa lahko prikažemo kot podmnožico vzorčnega prostora. Če sta podmnožici disjunktni, sta pripadajoča dogodka nezdružljiva. 

**Elementarni dogodki**

- Se zgodijo na en sam način.
- So med seboj paroma nezdružljivi.
- Vzorčni prostor je množica vseh elementarnih dogodkov danega poskusa.
- Če je število elementarnih dogodkov končno, ga označimo z _n_.   

**Sestavljeni dogodki**

- Se zgodijo na več načinov.
- Vsak sestavljeni dogodek lahko zapišemo kot vsoto elementarnih dogodkov.
- Gotovi dogodek je sestavljeni dogodek. Enak je vsoti vseh elementarnih dogodkov.
- Vsota različnih dogodkov je vedno sestavljeni dogodek.

_Primeri_

**Popoln sistem dogodkov** je taka množica dogodkov pri danem poskusu, da se ob vsaki ponovitvi poskusa zgodi natanko eden izmed njih. V to množico ne dajemo nemogočega in gotovega dogodka.
## **VERJETNOST DOGODKA**
Vzorčni prostor dogodkov poskusa je simetričen, če so vsi elementarni dogodki
enako verjetni.
Naj bo v poskusu popoln sistem elementarnih dogodkov simetričen in A dogodek iz
vzorčnega prostora tega poskusa. Verjetnost dogodka A je količnik med
številom m za dogodek A ugodnih elementarnih dogodkov in številom n vseh
elementarnih dogodkov poskusa:
$$\begin{aligned}
&\quad P(A)=\frac{m}{n}
\end{aligned}$$
Primeri

Aksiomi verjetnosti:
1. Verjetnost poljubnega dogodka A je nenegativno realno število: P(A) ≥ 0
2. Verjetnost gotovega dogodka G je enaka 1: P(G) = 1
3. Verjetnost vsote nezdružljivih dogodkov A in B iz istega poskusa je enaka vsoti
verjetnosti obeh dogodkov: A n B = N = P(AUB) = P(A) + P(B)

## **RAČUNANJE VERJETNOSTI
Lastnosti verjetnosti:

1. Verjetnost nemogočega dogodka je 0: P(N) = 0
2. Vsota verjetnosti dogodka A in verjetnosti nasprotnega dogodka A' je 1: P(A) +
P(A')=1
3. Če je dogodek A način dogodka B, A c B, potem velja: P(A) ≤ P(B)
4. Verjetnost poljubnega dogodka A ne more biti večja od 1: P(A) ≤ 1
5. Verjetnost razlike poljubnih dogodkov A in B je enaka: P(A - B) = P(A) -
P(AnB)
6. Verjetnost vsote združljivih dogodkov A in B je: P(A U B) = P(A) + P(B) -
P(AnB)


