---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

## Úvod
Nově příchozího hosta musíme na stránce nějak poutavě uvítat.

Vyskloňujte svoje jméno do souboru **autor_paady.txt**

``` plaintext
Radek Šmíd
Radka Šmída
Radku Šmídovi
Radka Šmída
Radku Šmíde
Radku Šmídovi
Radkem Šmídem
```

A pak spusťte náledující skript.

``` bash
#!/bin/bash
NAME_2P=`head -2 autor_paady.txt | tail -1`   # Uložíme si jméno v druhém pádu
echo -n "Vítejte na osobní stránce $NAME_2P." # Ošetříme proměnou pomocí '"'
```
## Vytahování
Osobní stránku můžeme využít jak příležitost k chlubení.
Nezapomeňte na stránce nenápadně zmínit (nebo mimochodem ukázat) jaké technologie umíme a co nám jde. 

``` sql
SELECT SUM(z.exps) AS "Total EXP" , techname AS "Technologie"
    FROM zkusenosti z JOIN technologie t ON t.techid=z.techid
    GROUP BY techname
    HAVING SUM(z.exps) > 9000
    ORDER BY "Total EXP" DESC;
```

## Tisk
Někteří zaměstnavetelé, nebo třeba babička, můžou požadovat životopis (nebo vysvědčení) v tištěné formě. V takovém případě je důležité mít už připravenou sazbu.

``` tex
\input opmac 	% Olšákova PlainTeXová makra
\chyph		% Používáme české dělení slov. Use CSplain!
\margins/1 a4 (2,2,,)cm
\typosize[13/15]% Nastaveni fontu 

% Definice sekce
\newcount\cisloSekce
\cisloSekce = 1
\eoldef\sekce#1{\bigskip\par%
{\bf\the\cisloSekce. #1}%
\advance\cisloSekce by 1\par\noindent}

%\sekce Název sekce
% ...

\bye
```

> POZOR! Takhle dlouhé úseky kódu čtenáře nudí. Raději za ně rychle vložte nějaký obrázek.
>![asdf](./fotky/f-jednorozec-s.png)

## Zpětná vazba
Poděkujeme čtenáři za jeho čas...

``` bash
#!/bin/bash
read -r -p "Užili jste si ukázku? [a/n]" CHOICE
if [ "$CHOICE" == 'a' ]
  then
    echo "$USER" >> sympataci.txt
    exit 0
fi
exit 1
```