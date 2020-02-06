---
layout: page
title: Jak nainstalovat TeX + CSplain na Fedoru 31
permalink: /blbinky/tex/
---
Pro nedočkavé COPY+PASTEry je odpověď:
``` bash
sudo dnf install texlive texlive-collection-langczechslovak texlive-hyphen-english texlive-hyphen-italian texlive-hyphen-german texlive-hyphen-french texlive-hyphen-polish texlive-hyphen-spanish texlive-hyphen-slovenian texlive-hyphen-finnish texlive-hyphen-hungarian
sudo fmtutil-sys --all
sudo texhash
```

# Základní instalace
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

Součástí nainstalovaného balíku je i pdftex, který místo původního DVI generuje nám, značně bližší PDF.

``` bash
pdftex test1.tex
```

a dostaneme pdfko s naším prvním TeXovským dokumentem. Gratuluji!

# TeX Live + CSplain
Vytvoříme nový dokument. *test2.tex*
``` tex
\chyph %czech hyphenation
Žluťoučký kůň úplěl ďábelské ódy.
\bye
```

Krátkým hrabáním v repozitáři nalezneme, že existuje balík se jménem kolekce jazyka českého. Skvělé, to zní jako něco co potřebujeme. (jeho součástí je mimochodem CSplain)
``` bash
sudo dnf install texlive-collection-langczechslovak
```

Jenže i teď mrška příkaz:

``` bash
pdfcsplain test2.tex
```

... hodí neočekávaný error

```
mktexfmt [ERROR]: running `luatex -ini   -jobname=pdfcsplain -progname=pdfcsplain -etex csplain.ini >&2 </dev/null' return status 1
mktexfmt [ERROR]: return error due to options --strict
mktexfmt [ERROR]: running `pdftex -ini   -jobname=pdfcsplain -progname=pdfcsplain -etex -enc csplain-utf8.ini >&2 </dev/null' return status 1
mktexfmt [ERROR]: return error due to options --strict
mktexfmt [ERROR]: running `xetex -ini   -jobname=pdfcsplain -progname=pdfcsplain -etex csplain.ini >&2 </dev/null' return status 1
mktexfmt [ERROR]: return error due to options --strict
mktexfmt [INFO]: Not selected formats: 20
mktexfmt [INFO]: Failed to build: 3 (luatex/pdfcsplain pdftex/pdfcsplain xetex/pdfcsplain)
mktexfmt [INFO]: Total formats: 23
mktexfmt [INFO]: exiting with status 3
I can't find the format file `pdfcsplain.fmt'!
```

S tím se popereme. Pan Olšák na [svých stránkách](http://petr.olsak.net/csplain.html) radí vygenerovat **pdfcsplain.fmt** ručně pomocí příkazu. (Ručně zkontrolovat jeho existenci můžete v afdresáři /var/lib/texmf/web2c/pdftex/pdflatex.fmt )

```
pdftex -jobname pdfcsplain -ini -etex -enc csplain-utf8.ini
```
, ale ten hodí chybu.

```
! I can't find file `hyph-en-gb'.
<argument> \input hyph-en-gb 
                             
\loadpatterns ...encoding, \string #1=#2 (#3).} #5
                                                   \endgroup \expandafter \g...
l.199 ...  {\input hyph-en-gb }23 \relax \engbPatt
                                                  
(Press Enter to retry, or Control-D to exit)
Please type another input file name: 
```

Dobrá tak tedy jinak. Lidé na [internetu](https://bugzilla.redhat.com/show_bug.cgi?id=578426) radí, přepočítat a přehashovat pomocí. 
```
sudo fmtutil-sys --all
sudo texhash
```

Jenže to také nefunguje a spadne s errorem.

```
...
fmtutil [ERROR]: return error due to options --strict
fmtutil [INFO]: Successfully rebuilt formats: 16
fmtutil [INFO]: Failed to build: 5 (pdftex/pdfcsplain luatex/pdfcsplain xetex/pdfcsplain luatex/luacsplain pdftex/csplain)
fmtutil [INFO]: Total formats: 21
fmtutil [INFO]: exiting with status 5
```

A jejda. No dobrá. Začíná detektivní práce. Podle erroru výše si domyslím, že chybí balík dělení slov - angličina - Velká Británie (Hyphenation EN GB). Po dalším pátrání zjistíme, že tento balík lze nalézt v **texlive-hyphen-english**, proces opakujeme a časem zjistíme, že není potřeba doinstalovat jenom angličtinu, ale i Italštinu, Němčinu, Franzouzštinu, Polštinu, Španělštinu, Slovinštinu, Finštinu a Maďarštinu. Proč? Mě se neptejte. Ale vystopoval jsem [commit, který za to asi může](https://git.texlive.info/texlive/commit/?id=e6ecf62a1727571cc47129fa4b4e198eadbe2ed3) v repozitáři TeX Live.

Doinstalujeme požadované jazyky a zkusíme přegenerovat **pdfcsplain.fmt**

``` bash
sudo dnf install texlive-hyphen-english texlive-hyphen-italian texlive-hyphen-german texlive-hyphen-french texlive-hyphen-polish texlive-hyphen-spanish texlive-hyphen-slovenian texlive-hyphen-finnish texlive-hyphen-hungarian
sudo fmtutil-sys --all
sudo texhash
```

A pak vše (včetně OPmac) začne fungovat.

Pěkné TeXování!

*PS: Pokud má někdo zájem o návod i na jiné distribuci dejte vědět.*
