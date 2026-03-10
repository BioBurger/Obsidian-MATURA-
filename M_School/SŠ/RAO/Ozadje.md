## background-color
```css
h1 {

  background-color: red;

}

  
div {

  background-color: #d38c8c;

}

  
p {

  background-color: rgb(245, 245, 156);

}

```
## Prosojnost:
```css
div {

  background-color: blue;

  /*opacity: 1;   privzeto je 1 */

}

  
div.drugi {

  opacity: 0.75;

}

  
div.tretji {

  opacity: 0.5;

}

  
div.cetrti {

  opacity: 0.25;

}
```
## background-image
```css
p {

   background-image: url("ozadje.jpg");

}
```
## background-repeat
```css
 body {

   background-image: url("primer.jpg");
   background-repeat: reapet;

 }
```
## background-position
```css
body {

   background-image: url("primer.jpg");

   background-repeat: no-repeat;

   background-position: right top;

}
```
## background-attachment
- Nam pove ali se bo background premikal ali ne
```css
     body {

       background-image: url("primer.jpg");

       background-repeat: no-repeat;

       background-position: right top;

       background-attachment: fixed;

     }
```
## background
- Da bi skrajšali kodo, je možno vse lastnosti ozadja določiti z eno samo lastnostjo – background.

- 1.background-color

- 2.background-image

- 3.background-repeat

- 4.background-attachment

- 5.background-position
```css
body {

  background-color: #ffff00;

  background-image: url("primer.jpg");

  background-repeat: no-repeat;

  background-position: right top;

}

  
/*lahko krajše zapišemo kot:  */
  
body {

  background: #ffff00 url("primer.png") no-repeat right top;

}
```
## background-size(Določa velikost slike ozadja)
## border-style
- Določamo obliko robov
- Mora biti drugače ne deluje nobena od naslednih style-ov

| Lastnost | Opis                   |
| -------- | ---------------------- |
| none     | ni roba                |
| hidden   | skrit rob              |
| dotted   | pike                   |
| dashed   | črte                   |
| solid    | polna črta             |
| double   | dvojni neprekinjen rob |
- Obstaja tudi
```css
p {

  border-top-style: dotted;

  border-right-style: solid;

  border-bottom-style: dotted;

  border-left-style: solid;

}
```
- **Drugače je pa**
1. border-style vsebuje 4 vrednosti, npr. border-style: dotted solid double dashed;
	zgornja obroba je pikčasta, desna obroba je polna, spodnja obroba je dvojna, leva obroba je črtasta

2. border-style vsebuje 3 vrednosti, npr. border-style: dotted solid double;
	zgornja obroba je pikčasta, desna in leva obroba sta polni, spodnja obroba je dvojna

3. border-style vsebuje 2 vrednosti, npr. border-style: dotted solid;
	zgornja in spodnja obroba sta pikčasti, desna in leva obroba sta polni

4. border-style vsebuje 1 vrednost, npr. border-style: dotted;
	vse 4 obrobe so pikčaste
### border-width
```css
 .thin { border-style: solid; border-width: thin }

 .medium { border-style: solid; border-width: medium  }

 .thick { border-style: solid; border-width: thick  }

 .width1 { border-style: solid; border-width: 1px  }

 .width3 { border-style: solid; border-width: 3px  }

 .width5 { border-style: solid; border-width: 5px  }

 .width10 { border-style: solid; border-width: 10px  }
```
### border-color
### border-radius
- **Lastnost border-radius se uporablja za dodajanje zaobljenih robov elementu.**
```css
.brez {

  border: 2px solid #0011ff

}

  
.round5 {

  border: 2px solid #0011ff; border-radius: 5px;

}

  
.round8 {

  border: 2px solid #0011ff; border-radius: 8px;

}

  
.round12 {

  border: 2px solid #0011ff; border-radius: 12px;

}

  
.round20 {

  border: 2px solid #0011ff; border-radius: 20px;

}
```
![[Pasted image 20251122190129.png]]
### outline
- Z lastnostjo outline določimo lastnosti zunanje obrobe, ki jo postavimo okrog HTML elementa zunaj robov.
```css
.obroba {

   border: 10px solid yellow;

   outline: 10px solid gray;

}
```
![[Pasted image 20251122190225.png]]
