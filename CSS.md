# CSS/Sass Code Style Guidelines

## Formatierung

```css
.foo, .foo.bar,
.baz {
    display: block;
    background-color: green;
    color: red;
}

.qux {
	width: 100%;
}
```

### Allgemein
* Alle Selektoren und Eigenschaften sind klein zu schreiben (**keine camelCase-Selektoren**)
* In selektoren sind alphanumerische Zeichen (a-z sowie 0-9) sowie Bindestriche zulässig (**keine snake_case-Selektoren**)

### Regeln
* Genau eine Leerzeile nach jeder Regel

### Selektoren
* Ein Selektor je Zeile (Normalfall)
* Verwandte Selektoren in eine Zeile, getrennt durch ein Komma `,` und genau ein folgendes Leerzeichen
* Genau ein Leerzeichen zwischen letztem Selektor und öffnender Klammer `{` (kein Zeilenumbruch)
* Schließende Klammer `}` in eigene Zeile
* Selektoren sollten stets **so unspezifisch wie möglich sein**
    * Die Adressierung von Elementen sollte in dieser Prioritätenreihenfolge realisiert werden:
        1. Elementnamen (z.B. `div`)
        2. Klassennamen (z.B. `.blog`)
        3. Elementattribute (z.B. `[type=text]`)
        4. Pseudo-Selektoren & -Elemente (z.B. `:focus` oder `::before`)
        5. IDs (z.B. `#article-list`)

### Deklarationen (Eigenschaft-Wert-Paare)
* **Eine Zeile je Deklaration, eine Deklaration je Zeile**
* Doppelpunkt `:` unmittelbar nach dem Eigenschaftsnamen
* Genau ein Leerzeichen zwischen Doppelpunkt `:` und Wert
* Einrückung zur Selektorflucht um genau ein `TAB`
* Genau ein Semikolon `;` am Ende Zeile
* Verwandte Eigenschaften (z.B. `width`, `height` oder `top`, `left`, `bottom`, `right`) sind zu gruppieren und zueinander zu sortieren

### Sonderfälle

Zum Zweck der **schnelleren Erfassbarkeit** dürfen bestimmte Angaben **durch Leerzeichen** ausgerichtet werden.

```css
.foo {
	-webkit-border-radius: 3px;
	   -moz-border-radius: 3px;
	        border-radius: 3px;
}

.bar {
    position: absolute;
    top:    0;
    right:  0;
    bottom: 0;
    left:   0;
    margin-right: -10px;
    margin-left:  -10px;
    padding-right: 10px;
    padding-left:  10px;
}

.icon-home     { background-position:   0     0  ; }
.icon-person   { background-position: -16px   0  ; }
.icon-files    { background-position:   0   -16px; }
.icon-settings { background-position: -16px -16px; }
```

* Rechtsausrichtung von Eigenschaftsnamen mit *vendor prefix*
* Rechtsausrichtung der Werte verwandter Eigenschaften
* Einzeilige, in sich ausgerichtete Notation ähnlicher Regelvarianten
	* **Nur genau eine Wertezuweisung zulässig** (1 Deklaration = 1 Zeile)
	* Leerzeichen statt Zeilenumbruch nach öffnender Klammer `{`
	* Leerzeichen statt Zeilenumbruch vor schließender Klammer `}`


# Schachtelung ("Nesting")

Die Nutzung eines CSS-Präprozessors (z.B. Sass) bringt die Möglichkeit mit sich, Regeln zu schachteln.

```css
foo {
	position: absolute;
	top:           50%;
	left:            0;
	width:        100%;
	height:      200px;
	margin-top: -100px;
	
	&:hover {
		text-decoration: underline;
	}
	
	&:before {
		content: '»';
		margin-right: 1em;	
	}
	
	&.bar {
		color: red;
	}
	
	.baz,
	qux,
	#quux {
		font-weight: bold;
	}
	
	.norf & .bra {
		display: none;
	}
}
```

* **Schachtelung ist — wo immer möglich — zu vermeiden!**
* **Schachtelung ID-basierter Selektoren ist nicht zulässig** (z.B. `#foo #bar { ... }`) 
* **Schachtelung von mehr als 3 Selektorebenen ist schlechter Stil und nicht zulässig** (z.B. `#foo .bar > .norf & bra { ... }`; hier empfiehlt sich ggf. die Vergabe zusätzlicher CSS-Klassen als Ansatzpunkte) 
* Die Angaben innerhalb einer Regel sind zu sortieren und gruppieren:
	1. Deklarationen (Eigenschaft-Wert-Paare)
	2. Pseudo-Klassen (z.B. `:hover`, `:focus`)
	3. Pseudo-Elemente (z.B. `:before`, `:after`, `:first-letter`)
	4. Selektorvarianten durch Klassen (z.B. `&.bar`)
	5. Klassenbasierte Subselektoren (`.baz`) 
	6. Elementbasierte Subselektoren (`qux`) 
	7. ID-basierte Subselektoren (`#quux`) 
	8. Sonstige Selektoren (`.norf & bra`)
* Geschachtelte Regeln (Positionen 2. bis 8.) sind untereinander und zu ihrem Vorgänger jeweils durch eine Leerzeile abzusetzen (siehe auch [Sonderfälle](#sonderf-lle))
