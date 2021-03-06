# git101 ![git-logo](images/Git-logo.png)
Git-opas Haaga-Helian opiskelijoille
Auttaa alkuun gitin käytön kanssa!

Sisällys
1. [Mikä on Git ja mihin sitä tarvitaan?](#1-mikä-git-on-ja-mihin-sitä-tarvitaan)
2. [Git:n asennus](#2-gitn-asennus)
3. [Komentorivin käyttö](#3-komentotulkin-käyttö)
4. [Yleisimpiä git-komentoja](#4-yleisimpiä-git-komentoja)
5. [Ensimmäisen repositoryn luonti omalle koneelle](#5ensimmäisen-repositoryn-luonti-omalle-koneelle)
6. [Miten viedä muutokset omasta repositorystä etärepositoryyn](#6-miten-viedä-muutokset-omasta-repositorystä-etärepositoryyn)
7. [Haarat ja miksi niitä tarvitaan](#7-haarat-ja-miksi-niitä-tarvitaan)
8. [Merge conflict! Mitä tapahtui, mitä teen?](#8-merge-conflict-mitä-tapahtui-mitä-teen)

### 1. Mikä Git on ja mihin sitä tarvitaan?
Git on versionhallinta. Versionhallinnalla tarkoitetaan palvelua, joka säilyttää koodia. Toisin sanoen varmuuskopio koodista. Versionhallinnan avulla voidaan muutosten tekemisen jälkeenkin palata aiempiin versioihin, jos esim. jotain menee pieleen. Koodin lisäksi versionhalinnan avulla tehdyt muutokset on helppo dokumentoida. Git on Ilmainen. Git on hajautettu, siinä ei siis ole minkäänlaista keskitettyä palvelinta. Jokainen Git-tietovarasto on itsenäinen.

### 2. Git:n asennus
Git:n käyttämiseksi on git-ohjelmisto oltava asennettuna tietokoneella, jolla sitä halutaan käyttää. Git-ohjelmiston asentamiseksi löytyy varmasti useita eri ohjeita ympäri internettiä, alla git:n omat ohjeet

[Git lataus](https://git-scm.com/downloads)<br>
[Git asennusohjeet](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

#### 2.1 Konfigurointi
##### 2.1.1 Käyttäjätiedot
Jokaiseen versionhallintaan talletettavaan muutokseen tallennetaan muutoksen tehneen käyttäjän nimi ja sähköpostiosoite. Git-ohjelmiston asentamisen jälkeen olisikin hyvä asettaa käyttäjätiedot komennoilla:

- `git config --global user.name "<username>"`
- `git config --global user.email <email>`

`<username>` ja `<email>` kohdat korvataan omalla nimellä ja sähköpostilla. Käyttäjätiedot tarvitsee asettaa vain kerran tietokoneelle. --global -tarkentimella tiedot asetetaan siten, että asetukset ovat tietokoneen käyttäjäkohtaiset.

##### 2.1.2 Tekstieditori
Git-ohjelmistoa käyttäessä tulee esiin tilanteita, joissa on tarve käyttää tekstieditoria. Ohjelmiston asentamisen jälkeen oletusarvoinen tekstieditori on [vi](https://fi.wikipedia.org/wiki/Vi). Vi:n käyttäminen voi tuntu haastavalta (ohjeita tosin löytyy esim [täältä](https://fi.wikipedia.org/wiki/Vi#Peruskomennot)), joten git-ohjelmistossa on mahdollista vaihtaa tekstieditoria komennolla:
- `git config --global core.editor "<editor-and-options>"`

Tekstieditoriksi voi yrittää asettaa varmaan minkä tahansa ohjelman. Perusteelliset ohjeet eri editorien asettamiseksi löytyy [täältä](https://git-scm.com/book/tr/v2/Appendix-C%3A-Git-Commands-Setup-and-Config#_core_editor).

### 3. Komentorivin käyttö
Komentorivi tai komentoliittymä on tapa kommunikoida tietokoneen kanssa. Komentoliittymässä ajetaan tyypillisesti komentotulkkia. Tällöin käyttäjä kirjoittaa komentoriville käynnistettävän ohjelman nimen tai komentotulkin sisäisen komennon mahdollisine parametreineen ja painaa syöttöpainiketta, jolloin komentotulkki käsittelee käskyn ja tulostaa vastineen näytölle.

Komentotulkkeja on [useita](https://en.wikipedia.org/wiki/List_of_command-line_interpreters) ja on tärkeää huomata, ettei kaikki komennot toimi kaikissa tulkeissa. Ehkä tärkeintä on tietää, että unixin kaltaisissa käyttöjärjestelmissä (Linux, Mac) on yleensä eri tulkki, kuin Windows käyttöjärjestelmissä. On kuitenkin hyvä huomata, että esimerkiksi [git for windows](https://gitforwindows.org/) asennuksen yhteydessä asennetaan bash-emulaattori, jossa käytetään Unix-shell komentoja.

Komentoliittymän käyttö ei välttämättä vaadi suurta järjestelmän tuntemusta, sillä komennot ovat usein lyhennyksiä selväkielisistä englanninkielisistä sanoista, ja niille on yleensä saatavilla käytönaikainen ohje komennoilla help tai man. Komennot annetaan komeentoriville muodossa:

    command param1 param2 param3 … paramN 

jossa:
- command = annettava komento
- param 1, param2, jne = komennon vaihtoehdot (options) ja argumentit

Komennon vaihtoehtoina (options) voidaan esimerkiksi antaa tarkennuksia, miten komento suoritetaan ja argumentteina esimerkiksi mille tiedostolle komento suoritetaan.

Yleensä kaikki git-komennot annetaankin komentoriviä käyttäen. Komennolla `git help` saadaan lista komennoista, jotka voidaan suorittaa.

Komentorivin komennoista ja käytöstä löytyy internetistä varmasti miljoonia ohjeita, [ihan](http://appro.mit.jyu.fi/itkp1011/luennot/cli/) [suomeksikin](http://users.jyu.fi/~nieminen/ohj1/materiaalia/tyokaluohjeet/komentorivi_selviytyminen.html). Tärkeintä on ehkä ymmärtää, että komentorivia käyttäessä, työskennellään aina jossain työhakemistossa (ts working directory tai kansio). Kaikki annetut komennot suoritetaan tässä työhakemistossa ellei toisin komenneta. Esimerkiksi komennon `git init` suorittaminen luo paikallisen tyhjän repositorion sen hetkiseen __työhakemistoon__.

Nykyisen työhakemiston saa selville shell-tulkissa komennolla `pwd` - **p**rint **w**orking **d**irectory. Komento toimii myös Windowsin PowerShellissä, mutta ei command promptissa (cmd).

Työhakemistossa olevat tiedostot ja alihakemistot saa selville suorittamalla komennon `ls` (ei toimi command promptissa, ks [`dir`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/dir)). `ls` -komennon voi suortittaa myös esimerkiksi vaihtoehdolla (option) `-a`, jolloin listataan myös tiedostot ja kansiot, jotka alkavat `.` merkillä ('piilotetut tiedostot/kansiot'). Esimerkiksi `git init` -komennolla luodaa `.git` hakemisto, joka ei näy pelkällä `ls` -komennolla, mutta näkyy suorittamalla `ls -a`. Komentoa voi myös käyttää antamalla sille argumenttina hakemisto, jonka tiedostot halutaan listata. Esimerkiksi suorittamalla `ls -a /c` -komento, saadaan listattua __kaikki__ tiedosto ja hakemistot, jotka sijaitsevat `/c` -hakemistossa (ts c-asema).

Nykyistä työhakemistoa vaihdetaan komennolla `cd` - ***c***hange ***d***irectory. Komento toimii sekä command promptissa, että shellissä. Ilman argumentteja annettaessa, Unix-ympäristössä (linux & mac), komennon suorittaminen vaihtaa työhakemistoksi käyttäjän kotihakemiston ja windows-ympäristössä tulostetaan senhetkinen työhakemisto. Yleensä komennolle kuitenkin annetaan argumenttina se hakemisto, jonka halutaan olevan uusi työhakemisto. Argumentin hakemisto voidaan antaa joko täydellisenä polkuna (absolute path) tai suhteellisena polkuna (relative path). Esimerkiksi, jos työhakemistoksi halutaan vaihtaa `C:\Users\Git-user\Documents`, voidaan käyttää ___mistä tahansa___ työhakemistosta komentoa: `cd /C/Users/Git-user/Documents` (__shell__) TAI jos nykyinen työhakemisto on `C:\Users\Git-user` antamalla komento: `cd Documents`.

### 4. Yleisimpiä git-komentoja

- `git init` - luo paikallisen tyhjän repositoryn

- `git add .` - vertaa hakemistoa local repoon ja siirtää kaikki muutokset tilaan staged, eli nyt ne ovat valmiita commitoitavaksi local repoon. Koskee myös tiedoston luomisia ja poistamisia.

- `git commit` - tallettaa staged tilassa olevat tiedostot local repositoryyn.

- `git commit --amend` - tällä voit lisätä edelliseen committiin muutoksia, jotka unohdit tehdä(ennen sitä stageta muutokset normaalisti git add:lla)

- `git status` - näyttää staged tilassa olevat tiedostot

- `git diff` - näyttää erot tiedostojen työtila versioissa verrattuna local repossa oleviin versioihin. Eli näyttää muutokset, joita ei ole commitettu

- `git reset` - tyhjentää tiedostot staged tilasta, eli jos olet tehnyt git add jonkun tiedoston niin git reset poistaa sen tiedoston staged tilasta

- `git rm <file name>` - poistaa tiedoston ja asettaa tiedoston poiston staged-tilaan, jonka jälkeen tiedoston poisto voidaan commitoida (jos halutaan poistaa kansio, käytetään laajenninta -r, eli `git rm -r <folder name>`)

- `git checkout` - poistaa muutokset työtilan versiosta ja palautuu local repossa olevan tuoreimman version
- `git checkout <branch name>` - vaihtaa työtilan nimettyyn haaraan

- `git revert <commit>` - jos olet jo commitoinut muutokset ja haluatkin palata takaisin aikaisempaan tilaan

- `git branch testing` - luo uuden testing-nimisen haaran

- `git checkout -b <branch name>` - luo uuden haaran ja vaihtaa työtilan tähän uuteen haaraan

- `git fetch <nameOfTheRemoteRepo>` - lataa remote repositoryn tiedot paikalliseen repositoryyn, mutta ei muuta paikallista repoa

- `git pull <remotenNimi>` - hakee nykyisen haaran tiedot etä-reposta ja tekee mergen automaattisesti

- `git merge <branch name>` - yhdistää nimetyn haaran muutokset työtilaan

- `git push` - tallentaa omat lokaalit muutokset etärepositoryyn.

- `git --help` - Listaa hyödyllisimmät git komennot.

 

### 5.Ensimmäisen repositoryn luonti omalle koneelle
Avaa bash-komentokehote kansiossa, josta haluat tehdä repositoryn tai siirry oikeaan kansioon komennolla 
`cd <kansio>`
Anna sitten seuraavat komennot:
1. `git init`
2. `git add .`
3. `git commit -m 'Ensimmäinen commit'`

### 6. Miten viedä muutokset omasta repositorystä etärepositoryyn
1. `git remote add origin https://github.com/user/example.git`
2. `git push origin master`

### 7. Haarat ja miksi niitä tarvitaan
Haarat `branch` ovat mainio keino pitää saman projektikokonaisuuden eri kehityisvaiheita erillään toisistaan kuitenkin pitäen ne samassa repositoryssä. Yleisimpiä haarakehyksiä ja haarojen käyttöä erilaisissa projekteissa löytyy [tästä linkistä](https://nvie.com/posts/a-successful-git-branching-model/).

Haarojen tarkoitusperä on siis pitää esimerkiksi kehityksessä olevan sovelluksen valmiit testatut osat master haarassa ja toteuttaa testausta sekä jatkokehitystä esimerkiksi development haarassa. Lisäksi voidaan hyvin käyttää omia haaroja ei niin tärkeille komponenteille tai ideoille.
Tällä tavoin ohjelmistokehittäjä voi turvata ettei mikään erillinen osuus projektissa vaikuta mihinkään muuhun, ennenkuin hän näin päättää ja yhdistää `merge` haaran masteriin.

Ennen kuin siirryt haaroista toiseen, muista aina commitoida muutoksesi! Staging-alue ei ole riippuvainen mistään haarasta, joten jos jätät staging-alueella olevat muutokset committoimatta ja vaihdat haaraa, nämä samat muutokset säilyvät staging-alueella. Muutokset siirtyvät haaraan vasta commit-komennon jälkeen.

Yleisesti ottaen masterissa ei koodata mitään ja se toimiikin vain loppusijaintina täydelliselle koodille mitä ei tulla enää muuttamaan.


### 8. Merge conflict! Mitä tapahtui, mitä teen?
Merge conflicteja tapahtuu silloin kun yhdistettävissä haaroissa on keskenään ristiriitaisia muutoksia ja git ei tiedä, mitkä niistä tulisi sisällyttää committiin.

 Tällöin on käsin ratkaistava konfliktit ja valittava pidettävät koodit. Git ilmoittaa, missä kansiossa konflikti on tapahtunut ja toisensa poissulkevat commitit on eroteltu tiedostossa:
 - `<<<<<<` kertoo,mistä konflikti alkaa
 - `======` erottaa muutokset haarojen välillä
 - `>>>>>>` ilmoittaa, milloin konflikti loppuu
 Tarkista kumpi otetaan käyttöön, jonka jälkeen poista konflikti merkit ja commitoi koodi.
