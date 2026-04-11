**
# Definicija
$$\begin{flalign*}
& \text{Električni naboj je fizikalna količina, ki opisuje lastnost delcev, da med seboj delujejo z električnimi silami.} &\\
& \text{Naboj je lahko pozitiven ali negativen (protoni, elektroni).} &
\end{flalign*}$$

# Osnovni pojmi
$$\begin{flalign*}
& \text{Oznaka: } Q \text{ ali } q. &\\
& \text{Enota: coulomb (C).} &\\
& \text{Osnovni naboj elektrona/protona: } e_0 \approx 1{,}602 \cdot 10^{-19}\,\text{C}. &\\
& \text{Skupni naboj telesa: } Q = N \cdot e_0,\ \ N \in \mathbb{Z}. &
\end{flalign*}$$

# Zakon o ohranitvi naboja
$$\begin{flalign*}
& \text{Skupni električni naboj v izoliranem sistemu je konstanten (naboj se ne ustvarja in ne izgine).} &
\end{flalign*}$$


# Jakost električnega polja

## Definicija
$$\begin{flalign*}
& \text{Jakost električnega polja } \vec{E} \text{ v točki je sila na enoto pozitivnega preizkusnega naboja:} &\\
& \vec{E} = \frac{\vec{F}}{q}. &
\end{flalign*}$$ 

## Enota in pomen
$$\begin{flalign*}
& [\vec{E}] = \text{V/m} = \text{N/C}. &\\
& \text{Vektor: smer } \vec{E} \text{ je smer sile na pozitivni naboj.} &
\end{flalign*}$$

## Polje točkastega naboja
$$\begin{flalign*}
& \text{Za točkasti naboj } Q \text{ v razdalji } r: &\\
& E = k \frac{|Q|}{r^2}, \qquad k = \frac{1}{4\pi \varepsilon_0}. &
\end{flalign*}$$

## Homogeno polje med ploščama
$$\begin{flalign*}
& \text{V homogenem polju med vzporednima ploščama razdalje } d \text{ velja:} &\\
& E = \frac{U}{d}. &
\end{flalign*}$$


# Električni potencial in napetost

## Električni potencial
$$\begin{flalign*}
& \text{Električni potencial } \varphi \text{ v točki je potencialna energija na enoto naboja:} &\\
& \varphi = \frac{W}{q}. &\\
& [\varphi] = \text{V}. &
\end{flalign*}$$

## Napetost
$$\begin{flalign*}
& \text{Napetost med točkama A in B:} &\\
& U_{AB} = \varphi_A - \varphi_B = \frac{W_{AB}}{q}. &\\
& [U] = \text{V}. &
\end{flalign*}$$

## Povezava s poljem
$$\begin{flalign*}
& \text{Homogeno polje (razdalja } d\text{): } E = \frac{U}{d} \quad \Leftrightarrow \quad U = E \cdot d. &
\end{flalign*}$$


# Kondenzator

\subsection*{Definicija}
$$\begin{flalign*}
& \text{Kondenzator je element, ki shranjuje naboj in energijo v električnem polju.} &\\
& \text{Oznaka: } C,\quad [C] = \text{F (farad)}. &
\end{flalign*}$$

## Kapacitivnost
$$\begin{flalign*}
& C = \frac{Q}{U}. &\\[4pt]
& \text{Ravnoplanski kondenzator: } C = \varepsilon \frac{S}{d}, &\\
& \text{kjer je } S \text{ ploščina plošče, } d \text{ razdalja, } \varepsilon \text{ dielektrična konstanta.} &
\end{flalign*}$$

## Energija v kondenzatorju
$$\begin{flalign*}
& W = \frac{1}{2} C U^2. &
\end{flalign*}$$

## Vzporedna vezava kondenzatorjev
$$\begin{flalign*}
& \text{Napetost: } U_1 = U_2 = \dots = U_n = U. &\\
& \text{Naboj: } Q = Q_1 + \dots + Q_n. &\\
& \Rightarrow C_\text{eq} = C_1 + C_2 + \dots + C_n. &
\end{flalign*}$$

## Zaporedna vezava kondenzatorjev
$$\begin{flalign*}
& \text{Naboj: } Q_1 = Q_2 = \dots = Q_n = Q. &\\
& \text{Napetost: } U = U_1 + U_2 + \dots + U_n. &\\
& \Rightarrow \frac{1}{C_\text{eq}} = \frac{1}{C_1} + \frac{1}{C_2} + \dots + \frac{1}{C_n}. &
\end{flalign*}$$


# Električni tok in uporniki

## Električni tok
$$\begin{flalign*}
& I = \frac{\Delta Q}{\Delta t}, \qquad [I] = \text{A}. &\\
& \text{Smer toka: od + proti - polu (dogovorjena smer).} &
\end{flalign*}$$

## Ohmov zakon
$$\begin{flalign*}
& U = R I, \qquad [R] = \Omega. &
\end{flalign*}$$

## Zaporedna vezava upornikov
$$\begin{flalign*}
& \text{Tok: } I_1 = I_2 = \dots = I_n = I. &\\
& \text{Napetost: } U = U_1 + U_2 + \dots + U_n. &\\
& R_\text{eq} = R_1 + R_2 + \dots + R_n. &
\end{flalign*}$$

## Vzporedna vezava upornikov
$$\begin{flalign*}
& \text{Napetost: } U_1 = U_2 = \dots = U_n = U. &\\
& \text{Tok: } I = I_1 + I_2 + \dots + I_n. &\\
& \frac{1}{R_\text{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}. &
\end{flalign*}$$


# Kirchhoffova zakona

## 1. Kirchhoffov zakon (tokovni, vozliščno pravilo)
$$\begin{flalign*}
& \text{Vsota tokov, ki pritekajo v vozlišče, je enaka vsoti tokov, ki iz njega odtekajo.} &\\
& \sum I_\text{v} = \sum I_\text{iz} \quad \Leftrightarrow \quad \sum I = 0. &
\end{flalign*}$$

## 2. Kirchhoffov zakon (napetostni, zankno pravilo)
$$\begin{flalign*}
& \text{V poljubni zanki je algebrska vsota napetosti enaka nič:} &\\
& \sum U = 0. &\\
& \text{Napetostne dvige štejemo s pozitivnim predznakom, padce z negativnim.} &
\end{flalign*}$$


# Joulova toplota

## Definicija
$$\begin{flalign*}
& \text{Joulova toplota je toplota, ki nastane pri prehodu električnega toka skozi upor.} &\\
& \text{Del električne energije se pretvori v toploto.} &
\end{flalign*}$$

## Enačbe
$$\begin{flalign*}
& Q = I^2 R t, &\\
& Q = U I t, &\\
& Q = \frac{U^2}{R} t. &
\end{flalign*}$$

## Enota toplote
$$\begin{flalign*}
& [Q] = \text{J (joule)}. &
\end{flalign*}$$


# Gibanje delca v električnem polju}
## Sila na nabiti delec
$$\begin{flalign*}
& \vec{F} = q \vec{E}. &\\
& \text{Če je } q > 0,\ \text{smer sile = smer polja; če } q < 0,\ \text{smer je nasprotna.} &
\end{flalign*}$$

## Pospešek delca
$$\begin{flalign*}
& \vec{F} = m \vec{a} \Rightarrow \vec{a} = \frac{\vec{F}}{m} = \frac{q}{m} \vec{E}. &
\end{flalign*}$$

Gibanje v homogenem polju}
$$\begin{flalign*}
& \text{1. Začetna hitrost v smeri polja: enakomerno pospešeno gibanje.} &\\
& v = v_0 + a t,\qquad s = v_0 t + \frac{1}{2} a t^2. &\\[4pt]
& \text{2. Začetna hitrost pravokotno na polje:} &\\
& \text{v smeri polja: enakomerno pospešeno, pravokotno: enakomerno.} &\\
& \Rightarrow \text{tirnica je parabola (analogija z gibanjem v težnosti).} &
\end{flalign*}$$
