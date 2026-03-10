
---
## Definicija

$$\begin{flalign*} & \text{Odvod funkcije } f \text{ v točki } x \text{ je limita diferenčnega količnika:} &\\ & f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}. &\\[4pt] & \text{Drugi zapis (Leibnizev): } \frac{dy}{dx}\ \text{ali}\ \frac{df}{dx}. &\\[4pt] & \text{Geometrijski pomen: nagib tangente na graf funkcije v točki } x. &\\ & \text{Fizikalni pomen: trenutna hitrost spremembe (npr. hitrost, pospešek).} & \end{flalign*}$$

---

## 1. Vrste zapisov

$$\begin{flalign*} & f'(x), \quad f'(a), \quad \frac{dy}{dx}, \quad \frac{df}{dx}, \quad \dot{y}\ \text{(v fiziki — čas)}. &\\ & \text{Drugi odvod: } f''(x), \quad \frac{d^2y}{dx^2}. &\\ & \text{} n\text{-ti odvod: } f^{(n)}(x), \quad \frac{d^n y}{dx^n}. & \end{flalign*}$$

---

## 2. Odvedljivost in zveznost

$$\begin{flalign*} & \text{Funkcija } f \text{ je odvedljiva v točki } a\text{, če limita } \lim_{h \to 0} \frac{f(a+h)-f(a)}{h} \text{ obstaja in je končna.} &\\[4pt] & \textbf{Izrek: } \text{Če je } f \text{ odvedljiva v } a\text{, je tudi zvezna v } a. &\\ & \text{Obratno NE velja — zvezna funkcija ni nujno odvedljiva!} &\\[4pt] & \text{Primeri neodvedljivosti:} &\\ & \bullet\ f(x) = |x|\ \text{v točki } x = 0\ \text{(ostri kot — leva in desna limita se ne ujemata).} &\\ & \bullet\ \text{Funkcija s skokom (ni zvezna } \Rightarrow \text{ ni odvedljiva).} &\\ & \bullet\ \text{Funkcija z navpično tangenco.} & \end{flalign*}$$

---

## 3. Pravila za odvajanje

$$\begin{flalign*} & \text{1. Konstanta: } (c)' = 0. &\\ & \text{2. Vsota/razlika: } (f \pm g)' = f' \pm g'. &\\ & \text{3. Produkt s konstanto: } (c \cdot f)' = c \cdot f'. &\\ & \text{4. Produkt: } (f \cdot g)' = f' \cdot g + f \cdot g'. &\\ & \text{5. Količnik: } \left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2} \quad (g \neq 0). &\\ & \text{6. Verižno pravilo: } (f(g(x)))' = f'(g(x)) \cdot g'(x). &\\[4pt] & \text{7. Potenca (posplošitev): } \left(f(x)^n\right)' = n \cdot f(x)^{n-1} \cdot f'(x). &\\ & \text{8. Inverz: } \left(f^{-1}(x)\right)' = \frac{1}{f'(f^{-1}(x))}. & \end{flalign*}
$$
---

## 4. Tabela osnovnih odvodov

$$\begin{flalign*} & \textbf{Potenčne funkcije:} &\\ & (c)' = 0, &\\ & (x)' = 1, &\\ & (x^n)' = n x^{n-1} \quad (n \in \mathbb{R}), &\\ & \left(\frac{1}{x}\right)' = -\frac{1}{x^2}, &\\ & (\sqrt{x})' = \frac{1}{2\sqrt{x}}, &\\ & \left(\sqrt[n]{x}\right)' = \frac{1}{n \cdot \sqrt[n]{x^{n-1}}} = \frac{1}{n} x^{\frac{1}{n}-1}. &\\[6pt] & \textbf{Eksponentne in logaritemske:} &\\ & (e^x)' = e^x, &\\ & (a^x)' = a^x \ln a \quad (a > 0,\ a \neq 1), &\\ & (\ln x)' = \frac{1}{x} \quad (x > 0), &\\ & (\log_a x)' = \frac{1}{x \ln a} \quad (x > 0,\ a > 0,\ a \neq 1). &\\[6pt] & \textbf{Trigonometrične:} &\\ & (\sin x)' = \cos x, &\\ & (\cos x)' = -\sin x, &\\ & (\tan x)' = \frac{1}{\cos^2 x} = 1 + \tan^2 x, &\\ & (\cot x)' = -\frac{1}{\sin^2 x} = -(1 + \cot^2 x). &\\[6pt] & \textbf{Arcus funkcije (inverzne trig.):} &\\ & (\arcsin x)' = \frac{1}{\sqrt{1-x^2}} \quad (|x| < 1), &\\ & (\arccos x)' = -\frac{1}{\sqrt{1-x^2}} \quad (|x| < 1), &\\ & (\arctan x)' = \frac{1}{1+x^2}. & \end{flalign*}$$

---

## 5. Reševanje — algoritem

$$\begin{flalign*} & \text{1. Korak: prepoznaj tip funkcije (potenca, eksponentna, trigonometrična...).} &\\ & \text{2. Korak: izberi ustrezno pravilo (produkt, količnik, verižno pravilo...).} &\\ & \text{3. Korak: uporabi tabelirane odvode osnovnih funkcij.} &\\ & \text{4. Korak: poenostavi rezultat (če je mogoče).} & \end{flalign*}$$

---

## 6. Tehnike odvajanja — primeri

### 6.1 Odvod produkta

$$\begin{flalign*} & \text{Primer: } f(x) = x^2 \cdot \sin x. &\\ & u = x^2,\quad u' = 2x; \qquad v = \sin x,\quad v' = \cos x. &\\ & f'(x) = 2x \sin x + x^2 \cos x. & \end{flalign*}$$

### 6.2 Odvod količnika

$$\begin{flalign*} & \text{Primer: } f(x) = \frac{x^2 + 1}{x - 1}. &\\ & u = x^2+1,\quad u' = 2x; \qquad v = x-1,\quad v' = 1. &\\ & f'(x) = \frac{2x(x-1) - (x^2+1)}{(x-1)^2} = \frac{x^2 - 2x - 1}{(x-1)^2}. & \end{flalign*}$$

### 6.3 Verižno pravilo

$$\begin{flalign*} & \text{Primer: } f(x) = (3x+1)^5. &\\ & \text{Zunanja: } u^5 \to 5u^4; \qquad \text{Notranja: } g(x) = 3x+1,\quad g'(x) = 3. &\\ & f'(x) = 5(3x+1)^4 \cdot 3 = 15(3x+1)^4. & \end{flalign*}$$

### 6.4 Verižno pravilo — logaritem

$$\begin{flalign*} & \text{Primer: } f(x) = \ln(x^2+1). &\\ & (\ln u)' = \frac{u'}{u}; \qquad u = x^2+1,\quad u' = 2x. &\\ & f'(x) = \frac{2x}{x^2+1}. & \end{flalign*}$$

### 6.5 Verižno pravilo — eksponent

$$\begin{flalign*} & \text{Primer: } f(x) = e^{3x^2 - 1}. &\\ & (e^u)' = e^u \cdot u'; \qquad u = 3x^2 - 1,\quad u' = 6x. &\\ & f'(x) = e^{3x^2-1} \cdot 6x = 6x\,e^{3x^2-1}. & \end{flalign*}$$

### 6.6 Kombinirano — produkt + verižno pravilo

$$\begin{flalign*} & \text{Primer: } f(x) = x^3 \cdot e^{2x}. &\\ & u = x^3,\quad u' = 3x^2; \qquad v = e^{2x},\quad v' = 2e^{2x}. &\\ & f'(x) = 3x^2 e^{2x} + x^3 \cdot 2e^{2x} = e^{2x}(3x^2 + 2x^3) = x^2 e^{2x}(3+2x). & \end{flalign*}$$

### 6.7 Logaritemsko odvajanje

$$\begin{flalign*} & \text{Uporabno za } f(x) = [g(x)]^{h(x)}\ \text{(baza in eksponent sta obe funkciji } x\text{).} &\\ & \text{Primer: } f(x) = x^x \quad (x > 0). &\\ & \text{Vzamemo } \ln: \quad \ln f(x) = x \ln x. &\\ & \text{Odvajamo obe strani:} \quad \frac{f'(x)}{f(x)} = \ln x + x \cdot \frac{1}{x} = \ln x + 1. &\\ & f'(x) = f(x)(\ln x + 1) = x^x(\ln x + 1). & \end{flalign*}$$

---

## 7. Enačba tangente

$$\begin{flalign*} & \text{Tangenta na } f \text{ v točki } T(a,\, f(a))\text{:} &\\ & y = f'(a)(x - a) + f(a). &\\[4pt] & \text{Normala (pravokotna na tangento) v isti točki:} &\\ & y = -\frac{1}{f'(a)}(x - a) + f(a) \quad (f'(a) \neq 0). &\\[4pt] & \text{Primer: } f(x) = x^2 - 3x + 1,\quad a = 2. &\\ & f(2) = 4-6+1 = -1; \qquad f'(x) = 2x-3,\quad f'(2) = 1. &\\ & \text{Tangenta: } y = 1\cdot(x-2) + (-1) = x - 3. & \end{flalign*}$$

---

## 8. Monotonost in lokalni ekstremi

$$\begin{flalign*} & \text{Če je } f'(x) > 0\ \text{na intervalu } (a,b): \quad f \text{ je naraščajoča.} &\\ & \text{Če je } f'(x) < 0\ \text{na intervalu } (a,b): \quad f \text{ je padajoča.} &\\[4pt] & \textbf{Stacionarne točke: } f'(x) = 0. &\\ & \text{Lokalni maksimum: } f' \text{ se spremeni iz } + \text{ v } - \text{ v točki } x_0. &\\ & \text{Lokalni minimum: } f' \text{ se spremeni iz } - \text{ v } + \text{ v točki } x_0. &\\ & \text{Prevoj (ni ekstrema): predznak } f' \text{ se ne spremeni.} & \end{flalign*}$$

### Primer — iskanje ekstremov

$$\begin{flalign*} & f(x) = x^3 - 3x^2 - 9x + 2. &\\ & f'(x) = 3x^2 - 6x - 9 = 3(x^2 - 2x - 3) = 3(x-3)(x+1). &\\ & f'(x) = 0 \Rightarrow x_1 = -1,\quad x_2 = 3. &\\ & f'(-2) = 3(+)(+) > 0;\ f'(0) = 3(-)(+) < 0;\ f'(4) = 3(+)(+) > 0. &\\ & \Rightarrow x = -1\ \text{lokalni maks.},\quad x = 3\ \text{lokalni min.} & \end{flalign*}$$

---

## 9. Drugi odvod — konveksnost in konkavnost

$$\begin{flalign*} & f''(x) = (f'(x))'. &\\[4pt] & \text{Če je } f''(x) > 0\ \text{na } (a,b): \quad f \text{ je konveksna (konkavna navzgor, } \cup\text{).} &\\ & \text{Če je } f''(x) < 0\ \text{na } (a,b): \quad f \text{ je konkavna (konkavna navzdol, } \cap\text{).} &\\[4pt] & \textbf{Infleksijska točka: } f''(x) = 0\ \text{in predznak } f'' \text{ se v tej točki spremeni.} &\\[4pt] & \textbf{Test drugega odvoda za ekstreme (alternativa):} &\\ & \text{Če } f'(a) = 0\ \text{in } f''(a) > 0 \Rightarrow \text{lokalni minimum.} &\\ & \text{Če } f'(a) = 0\ \text{in } f''(a) < 0 \Rightarrow \text{lokalni maksimum.} &\\ & \text{Če } f'(a) = 0\ \text{in } f''(a) = 0 \Rightarrow \text{test ne pove ničesar — preveri s predznakom } f'. & \end{flalign*}$$

---

## 10. Globalni ekstremi na zaprtem intervalu

$$\begin{flalign*} & \text{Na zaprtem intervalu } [a, b] \text{ iščemo globalni (absolutni) maksimum in minimum.} &\\ & \text{Postopek:} &\\ & \text{1. Izračunaj } f'(x) = 0 \Rightarrow \text{stacionarne točke } x_1, x_2, \ldots \in [a,b]. &\\ & \text{2. Izračunaj vrednosti } f \text{ v stac. točkah in na robovih: } f(a),\ f(b). &\\ & \text{3. Največja vrednost = globalni maks.;\ najmanjša = globalni min.} &\\[4pt] & \text{Primer: } f(x) = x^3 - 3x \text{ na } [-2,\ 2]. &\\ & f'(x) = 3x^2 - 3 = 0 \Rightarrow x = \pm 1. &\\ & f(-2)=-2,\quad f(-1)=2,\quad f(1)=-2,\quad f(2)=2. &\\ & \text{Globalni maks. } = 2\ \text{(pri } x=-1\ \text{in } x=2\text{)},\quad \text{globalni min. } = -2. & \end{flalign*}$$

---

## 11. Optimizacijski problemi

$$\begin{flalign*} & \text{Cilj: poišči vrednost spremenljivke, ki optimizira (max/min) neko količino.} &\\[4pt] & \textbf{Postopek:} &\\ & \text{1. Definiraj spremenljivko in ciljno funkcijo } f(x). &\\ & \text{2. Zapiši morebitne omejitve in izlušči eno spremenljivko.} &\\ & \text{3. Izračunaj } f'(x) = 0 \Rightarrow \text{kritične točke.} &\\ & \text{4. Preveri, ali gre za maximum ali minimum (test } f''\ \text{ali predznaka } f'\text{).} &\\ & \text{5. Odgovori na vprašanje (vrni fizikalni/geometrijski pomen).} &\\[6pt] & \text{Primer: Pravokotnik z obsegom } 20\ \text{m — kdaj je ploščina največja?} &\\ & 2x + 2y = 20 \Rightarrow y = 10 - x. &\\ & P(x) = x(10-x) = 10x - x^2. &\\ & P'(x) = 10 - 2x = 0 \Rightarrow x = 5,\quad y = 5. &\\ & P''(x) = -2 < 0 \Rightarrow \text{maksimum. Ploščina: } P = 25\ \text{m}^2\ \text{(kvadrat!).} & \end{flalign*}$$

---

## 12. L'Hôpitalovo pravilo

$$\begin{flalign*} & \text{Uporabno za nedoločene oblike } \frac{0}{0}\ \text{ali}\ \frac{\pm\infty}{\pm\infty}. &\\[4pt] & \text{Če } \lim_{x \to a} f(x) = 0\ \text{in}\ \lim_{x \to a} g(x) = 0\text{, ter } g'(x) \neq 0 \text{ v okolici } a\text{:} &\\ & \lim_{x \to a} \frac{f(x)}{g(x)} = \lim_{x \to a} \frac{f'(x)}{g'(x)}. &\\[4pt] & \text{Pravilo lahko uporabimo večkrat zapored, dokler dobimo določeno obliko.} &\\[4pt] & \text{Primer: } \lim_{x \to 0} \frac{\sin x}{x} \quad \left(\frac{0}{0}\right). &\\ & = \lim_{x \to 0} \frac{\cos x}{1} = \cos 0 = 1. &\\[4pt] & \text{Primer: } \lim_{x \to \infty} \frac{x^2}{e^x} \quad \left(\frac{\infty}{\infty}\right). &\\ & = \lim_{x \to \infty} \frac{2x}{e^x} = \lim_{x \to \infty} \frac{2}{e^x} = 0. & \end{flalign*}$$


---

## 13. Potek funkcije — celoten postopek

$$\begin{flalign*} & \text{1. Definicijsko območje } D_f. &\\ & \text{2. Ničle: } f(x) = 0. &\\ & \text{3. Presečišče z } y\text{-osjo: } f(0). &\\ & \text{4. Sodost/lihist: } f(-x) = f(x)\ (\text{soda}),\quad f(-x)=-f(x)\ (\text{liha}). &\\ & \text{5. Asimptote:} &\\ & \quad \text{- Navpična: } x = a,\ \text{kjer } \lim_{x \to a} f(x) = \pm\infty. &\\ & \quad \text{- Vodoravna: } y = \lim_{x \to \pm\infty} f(x). &\\ & \quad \text{- Poševna: } y = kx + n,\quad k = \lim_{x \to \infty} \frac{f(x)}{x},\quad n = \lim_{x \to \infty}(f(x)-kx). &\\ & \text{6. Monotonost in ekstremi: } f'(x) = 0\ \text{ter predznačna analiza } f'. &\\ & \text{7. Konveksnost in infleksijske točke: } f''(x) = 0\ \text{ter predznačna analiza } f''. &\\ & \text{8. Skica grafa.} & \end{flalign*}$$

---

## 14. Fizikalne aplikacije

$$\begin{flalign*} & \text{Pot/položaj: } s(t). &\\ & \text{Hitrost: } v(t) = s'(t) = \frac{ds}{dt}. &\\ & \text{Pospešek: } a(t) = v'(t) = s''(t) = \frac{d^2s}{dt^2}. &\\[4pt] & \text{Telo miruje: } v(t) = 0. &\\ & \text{Telo se upočasnjuje: } v(t)\ \text{in}\ a(t)\ \text{imata nasprotna predznaka.} &\\ & \text{Telo se pospešuje: } v(t)\ \text{in}\ a(t)\ \text{imata enaka predznaka.} &\\[4pt] & \text{Primer: } s(t) = t^3 - 6t^2 + 9t + 1. &\\ & v(t) = 3t^2 - 12t + 9 = 3(t-1)(t-3). &\\ & v(t) = 0 \Rightarrow t = 1\ \text{s in}\ t = 3\ \text{s (telo se zaustavi).} &\\ & a(t) = 6t - 12;\quad a(1) = -6\ \text{(pojemanje)},\quad a(3) = 6\ \text{(pospeševanje).} & \end{flalign*}$$

---

## 15. Pogosta napaka — opomnik

$$\begin{flalign*} & \bullet\ (f \cdot g)' \neq f' \cdot g' \quad \text{— ne pozabi na pravilo produkta!} &\\ & \bullet\ \text{Pri verižnem pravilu ne pozabi na odvod notranje funkcije.} &\\ & \bullet\ (\ln x)' = \frac{1}{x},\ \text{ne}\ \ln 1 = 0\ \text{— to je vrednost, ne odvod.} &\\ & \bullet\ \text{Stacionarna točka } \neq \text{ekstrem — preveri predznak } f'. &\\ & \bullet\ f''(a) = 0\ \text{ne pomeni nujno infleksije — preveri predznak } f''. &\\ & \bullet\ \text{L'Hôpital velja le za obliki } \tfrac{0}{0}\ \text{ali}\ \tfrac{\infty}{\infty}. & \end{flalign*}$$