---
layout: page
title: Jak nainstalovat TeX + CSplain
permalink: /blbinky/tex/
---
# Jak nainstalovat TeX + CSplain na Fedoru

Pro nedočkavé kopyapasty je odpověď:
``` bash
sudo dnf install texlive texlive-collection-langczechslovak texlive-hyphen-italian texlive-hyphen-german texlive-hyphen-french texlive-hyphen-polish texlive-hyphen-spanish texlive-hyphen-slovenian texlive-hyphen-finnish texlive-hyphen-hungarian
sudo fmtutil-sys --all
sudo texhash
```

# Strasti instalace
Dobrá, chceme tedy pracovat v TeXu + CSplain + OPmac.

Víme, že instalace TeXu bude probíhat skrz repozitáře živého TeXu, tedy nainstalujeme pomocí dnf.
``` bash
sudo dnf install texlive
```

Pokusíme se vytechat naprosto základní dokument třeba *test1.tex*
``` tex
Hello World!
\bye
```

``` bash
pdftex test1.tex
```

a dostaneme pdfko s naším prvním TeXovským dokumentem. Gratuluji!

Pokud se ale pokusíme tímto způsobem pracovat s češtinou velice brzy skončíme na erroru:



Doinstalujeme proto i balík s češtinou. Fedora má připravený skvělý balík, který obsahuje CSplain a spoustu dalších vymožeností.

``` bash
sudo dnf install texlive-collection-langczechslovak
```

a pokusíme se nainstalovat 







# Úvod
Chtěl bych touto stránkou přiblížit slasti a strati začátečníka v TeXu. Krátce popíšu základní terminologii a pak ukážu jak to vlastně nainstalovat a použít.

## TeX / LaTeX / PlainTeX / CSplain - WTF?
Už jste se někdy pokusili nainstalovat TeX? Je mnohem lepší a čistější než LaTeX. Psaní maker je zábava a s většinou věcí nám pomůže sada maker od Petra Olšáka - OPmac. Jenže, jak vlastně začít? V knize TeX pro pragmatiky se dozvíme, že potřebujeme příkaz **csplain** nebo **pdfcsplain**. Jenže co to je? A jak si to vlastně nainstalovat?

### TeX
TeX je program od Donalda Knutha na sazbu. TeX je jenom jeden jediný kdo do něj může komitovat je sám autor - nebo předseda celosvětového sdružená milovníků TeXu (a to jenom po Knuthově smrti a jenom změnu čísla verze na Pí).

TeX se teď distribuuje pomocí balíků zvaných TeX Live, které jsou v každé pořádné distribci GNU/Linuxu.

### LaTeX
LaTeX je obrovksý moloch maker napsaný v TeXu který se používá k uživatelsky přístupnějšímu psaní různých vědeckých článků a prací.

### PlainTeX
Je takové holé minimum toho co je potřeba k sazbě dokumentů v TeXu aniž by člověk musel až zbytečně moc zacházet do primitivních příkazů TeXu. Připravil to také Donald Knuth.

### CSplain
Je soubor maker a nastavení TeXu aby byl použitelný s češtinou+slovenštinou. Součástí tohoto balíku je také soubor maker OPmac (Olšákova PlainTeXová makra), který poskytuje relativně velikou sílu v množství jednodušších maker. To nám pomáhá používat PlainTeX téměř až na úrovni LaTeXu. SPoustu věcí si musíte dodělat, ale zase pak víte jak fungují a nic vás nepřekvapí - nepoužíváte milion balíků/blackboxů jako v LaTeXu.

Intuice nás vede k tomu, že po nainstalování CSpolainu by TeX + čeština mělo jako kombinace na generování dokumentů fungovat. Bohuželk tomu tak není, ale to už předbíhám.

# Začínáme s TeXem.
## Cíle
Cílem je vytechat základní domuenty.





### Průměrně podle dnu v týdnu
![Bazén graf](https://docs.google.com/spreadsheets/d/e/2PACX-1vQe4UA54in-AgZxXh6yCUM8xljMo9P59vz1p1wCE0Pv3dkj_3zoUOEasor3eR6M49WfGjgqBkkATScZ/pubchart?oid=1073164936&format=image)

[Klikněte zde pro větší obrázek](https://docs.google.com/spreadsheets/d/e/2PACX-1vQe4UA54in-AgZxXh6yCUM8xljMo9P59vz1p1wCE0Pv3dkj_3zoUOEasor3eR6M49WfGjgqBkkATScZ/pubchart?oid=1073164936&format=image){:target="_blank"}
