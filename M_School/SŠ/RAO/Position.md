- Kakšna je vrsta postavitve elementa
```css
position: static; /* je default in ničesar ne spremeni*/
position: relative;/* Je kot static samo da lahko dodajamo dodatne lasnosti premika ki so relativne na začetno mesto*/
position: absolute;/* njegova pozicija je odvisna od valuetov ampak so vrednosti glede na parent element*/
position: fixed;/* bo vedno na istem položaju na ekranu tudi če skrolamo*/
position: sticky;/* kot fixed kadar pride element do specificirane lokacije drugače je pa kot static*/

/* Global values */
position: inherit;
position: initial;
position: revert;
position: revert-layer;
position: unset;
```