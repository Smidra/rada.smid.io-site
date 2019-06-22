---
layout: post

---
Tak, a je po všem. Náš nový malikatý blog na cesty po USA je hotový.

#### Ale jak to funguje?

Forestry.io je v podstatě něco jako malý markdown editor, který umí komitovat do GitHubu. Na forestry si tedy přes tablet nebo mobil napíšeme text nového postu a pak jenom klikneme publish.

#### No a co pak?

GitHub má definovaný webhook na každý push, který se pošle na Kovárnu (smid.io) , tam si ho odchytí Jenkins. 

Pro Jenkinse je to znamení, že má spustit nový build. Udělá git pull na repozitář a následně pustí moje shellovské příkazy. 

#### Jak se z .md stane .html?

Příkazy v shellu pustí progam Jekyll. Ten překládá .md na .html a umí i spoustu jiných vychytávek, mimo jiné i na blogování. Jekyll sestaví celou statickou HTML stránku a nakopíruje jí 