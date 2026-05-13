# Specifikacija zahtev

## Informacijski sistem za program lojalnosti Maestro

## Dokumentni podatki

| Polje                  | Vrednost                 |
| ---------------------- | ------------------------ |
| Oznaka dokumenta       | N1-LLM                   |
| Verzija                | 1.1                      |
| Status                 | Delovni osnutek          |
| Datum izdaje           | 2026-03-18               |
| Datum zadnje spremembe | 2026-03-25               |
| Jezik                  | Slovenščina              |
| Vir zahtev             | 01-Program-lojalnosti.md |
| Avtor                  | Martin Hovnik            |

## Zgodovina verzij

| Verzija | Datum      | Opis spremembe                                                                                              |
| ------- | ---------- | ----------------------------------------------------------------------------------------------------------- |
| 1.0     | 2026-03-18 | Pripravljena začetna strukturirana specifikacija zahtev.                                                    |
| 1.1     | 2026-03-18 | Dodani naslovnica, dokumentni metapodatki, status in formalna struktura dokumenta.                          |
| 1.2     | 2026-03-25 | Dodani diagrami sistema in slovar izrazov.                                                                  |
| 1.3     | 2026-04-08 | Odstranjene sekcije o konceptualnem modelu in povezovalni tabeli, saj so zdaj vključene v ločene dokumente. |

## Namen dokumenta

Dokument opredeljuje funkcionalne in nefunkcionalne zahteve, omejitve, vmesnike ter terminologijo za rešitev, ki podpira program lojalnosti trgovske verige Maestro.

## Obseg dokumenta

Dokument zajema zahteve, ki izhajajo iz izhodiščnega opisa problema in nalog v dokumentu 01-Program-lojalnosti.md.

---

# 1. Kratek opis sistema

Sistem podpira program lojalnosti trgovske verige Maestro. Namen sistema je povečati ponovne nakupe in dolgoročno zvestobo strank z dodeljevanjem točk ter upravljanjem statusov lojalnosti (osnovni, bronasti, srebrni, zlati).  
Strankam omogoča registracijo, pregled in koriščenje točk ter vpogled v nakupe, podjetju pa centralizirano upravljanje pravil, nagrad, statistik in statusov.

---

# 2. Funkcionalne zahteve

Oznake prioritet: **[M] Must**, **[S] Should**, **[C] Could**, **[W] Won't (v tej fazi)**.

_Upravljanje članstva in računov_:

| Oznaka | Funkcionalna zahteva                             | Opis                                                                                                                                                                            | Prioriteta |
| ------ | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| <a id="fz1"></a>FZ1    | Vključitev stranke v program lojalnosti          | Sistem omogoči registracijo stranke z osebnimi podatki in varnim preverjanjem e-naslova. Ob uspešni registraciji se ustvari uporabniški račun in dodeli začetni status osnovni. | [M]        |
| <a id="fz2"></a>FZ2    | Spletna registracija stranke                     | Sistem omogoči spletno registracijo z vnosom osebnih podatkov.                                                                                                                  | [M]        |
| <a id="fz3"></a>FZ3    | Varno preverjanje e-naslova ob registraciji      | Sistem zagotovi mehanizem, ki prepreči registracijo z ne-lastniškim e-naslovom.                                                                                                 | [M]        |
| <a id="fz4"></a>FZ4    | Ustvarjanje uporabniškega računa ob registraciji | Ob registraciji sistem ustvari uporabniški račun za prijavo v portal.                                                                                                           | [M]        |
| <a id="fz5"></a>FZ5    | Izdaja kartice lojalnosti in priprava pošiljanja | Ob uspešni vključitvi sistem podpre izdajo kartice lojalnosti in pripravo pošiljanja po navadni pošti.                                                                          | [S]        |
| <a id="fz6"></a>FZ6    | Dodelitev začetnega statusa                      | Ob včlanitvi stranka dobi začetni status osnovni.                                                                                                                               | [M]        |

_Nivoji lojalnosti_:

| Oznaka | Funkcionalna zahteva             | Opis                                                         | Prioriteta |
| ------ | -------------------------------- | ------------------------------------------------------------ | ---------- |
| <a id="fz7"></a>FZ7    | Podpora nivojem lojalnosti       | Sistem podpira nivoje: osnovni, bronasti, srebrni, zlati.    | [M]        |
| <a id="fz8"></a>FZ8    | Konfigurabilnost delitve nivojev | Sistem omogoča možnost kasnejše spremembe delitve na nivoje. | [C]        |

_Mesečni izračun točk zvestobe_:

| Oznaka | Funkcionalna zahteva                 | Opis                                                                                                 | Prioriteta |
| ------ | ------------------------------------ | ---------------------------------------------------------------------------------------------------- | ---------- |
| <a id="fz9"></a>FZ9    | Mesečni obračun točk                 | Sistem 1x mesečno izračuna točke za pretekli mesec.                                                  | [M]        |
| <a id="fz10"></a>FZ10   | Uporaba podatkov iz poslovnega IS    | Za izračun točk sistem uporabi zneske nakupov iz poslovnega informacijskega sistema trgovske verige. | [M]        |
| <a id="fz11"></a>FZ11   | Dodelitev točk po razredu in statusu | Sistem dodeli točke glede na zneskovni razred nakupov in status stranke.                             | [M]        |
| <a id="fz12"></a>FZ12   | Spreminjanje pravil točkovnika       | Sistem omogoča kasnejše spreminjanje pravil oziroma vrednosti točkovnika.                            | [M]        |

_Pravila prehajanja med statusi_:

| Oznaka | Funkcionalna zahteva                    | Opis                                                                                                                                                       | Prioriteta |
| ------ | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| <a id="fz13"></a>FZ13   | Začetni status ob včlanitvi             | Ob včlanitvi je status stranke osnovni.                                                                                                                    | [M]        |
| <a id="fz14"></a>FZ14   | Prehod v srebrni status                 | Ko stranka prvič preseže 499 EUR mesečnih nakupov, preide v srebrni status.                                                                                | [M]        |
| <a id="fz15"></a>FZ15   | Prehod v zlati status                   | Če stranka nato še dvakrat preseže prag 500 EUR, preide v zlati status.                                                                                    | [M]        |
| <a id="fz16"></a>FZ16   | Ohranjanje srebrnega statusa            | Za ohranjanje srebrnega statusa mora stranka imeti vsaj 200 EUR mesečnih nakupov.                                                                          | [M]        |
| <a id="fz17"></a>FZ17   | Ohranjanje zlatega statusa              | Za ohranjanje zlatega statusa mora stranka imeti vsaj 500 EUR mesečnih nakupov.                                                                            | [M]        |
| <a id="fz18"></a>FZ18   | Znižanje iz zlatega v srebrni status    | Če stranka ne izpolni pogoja za zlati status, se status zniža na srebrni.                                                                                  | [M]        |
| <a id="fz19"></a>FZ19   | Znižanje iz srebrnega v bronasti status | Če stranka dva zaporedna meseca ne izpolni pogoja za srebrni status, preide v bronasti status.                                                             | [M]        |
| <a id="fz20"></a>FZ20   | Pravila obnašanja v bronastem statusu   | V bronastem statusu stranka ostane, dokler dva zaporedna meseca ne opravi vsaj 200 EUR nakupov; če opravi nakup pod 50 EUR, preide nazaj v osnovni status. | [M]        |
| <a id="fz21"></a>FZ21   | Zaporedje mesečne obdelave              | Pri mesečni obdelavi sistem najprej posodobi status in šele nato dodeli točke.                                                                             | [M]        |

**Predpostavka A2:** izraza `>499` in `>500` se obravnavata kot prag preseganja 500 EUR.

_Portal za člane_:

| Oznaka | Funkcionalna zahteva       | Opis                                                 | Prioriteta |
| ------ | -------------------------- | ---------------------------------------------------- | ---------- |
| <a id="fz22"></a>FZ22   | Pregled zbranih točk       | Portal članom omogoča pregled zbranih točk zvestobe. | [M]        |
| <a id="fz23"></a>FZ23   | Unovčevanje točk           | Portal članom omogoča koriščenje (unovčevanje) točk. | [M]        |
| <a id="fz24"></a>FZ24   | Pregled nakupnega programa | Portal članom omogoča pregled nakupnega programa.    | [S]        |
| <a id="fz25"></a>FZ25   | Pregled zneskov nakupov    | Portal članom omogoča pregled zneskov nakupov.       | [S]        |

_Administracija_:

| Oznaka | Funkcionalna zahteva                        | Opis                                                                                                                     | Prioriteta |
| ------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------- |
| <a id="fz26"></a>FZ26   | Pregled statusov strank                     | Administratorski del omogoča pregled statusov strank za poljubno obdobje.                                                | [M]        |
| <a id="fz27"></a>FZ27   | Pregled statistike nakupov                  | Administratorski del omogoča pregled statistike nakupov.                                                                 | [M]        |
| <a id="fz28"></a>FZ28   | Poljubne poizvedbe po podatkovni bazi       | Administratorski del podpira poljubne poizvedbe po podatkovni bazi.                                                      | [W]        |
| <a id="fz29"></a>FZ29   | Upravljanje programa nagrad                 | Administratorski del omogoča upravljanje programa nagrad, ki je na voljo za točke.                                       | [M]        |
| <a id="fz30"></a>FZ30   | Upravljanje pravil statusov in nagrajevanja | Administratorski del omogoča upravljanje pravil prehajanja med statusi in nagrajevanja, predvsem spreminjanje vrednosti. | [M]        |

---

### Točkovnik

| Znesek nakupov v mesecu | Osnovni | Bronasti | Srebrni | Zlati |
| ----------------------- | ------: | -------: | ------: | ----: |
| do 200 EUR              |       5 |        0 |     7.5 |    10 |
| med 200 EUR in 1000 EUR |      10 |        5 |      15 |    20 |
| nad 1000 EUR            |      20 |       10 |      30 |    40 |

**Predpostavka A1:** zaradi mej v opisu se razredi interpretirajo kot:

- `znesek <= 200`,
- `200 < znesek <= 1000`,
- `znesek > 1000`.

# 3. Nefunkcionalne zahteve

Oznake prioritet: **[M] Must**, **[S] Should**, **[C] Could**, **[W] Won't (v tej fazi)**.

## Zmogljivost in kapaciteta

- [S] Sistem mora podpirati vsaj ~500.000 članov (vsaj 70 % strank).
- [S] Arhitektura mora omogočati bistveno večje število uporabnikov (širitev izven Slovenije).
- [M] Mesečni obračun točk mora biti izvedljiv nad celotno bazo članov.

## Varnost

- [M] Registracija mora vključevati varen mehanizem potrditve lastništva e-poštnega naslova.
- [M] Uporabniški računi morajo omogočati identifikacijo uporabnikov pri prijavi v portal.

## Razširljivost in vzdrževanje

- [M] Pravila točkovanja in statusnih prehodov morajo biti nastavljiva brez spremembe koncepta sistema.
- [C] Sistem mora podpirati morebitno spremembo delitve statusnih nivojev.

## Uporabniška izkušnja

- [S] Uporabniški vmesnik mora biti intuitiven.
- [S] Uporabljene morajo biti sodobne tehnologije.

## Lokalizacija

- [S] Celotna rešitev mora podpirati dva jezika: **slovenščino** in **angleščino**.

**Predpostavka A3:** podpora jezikom velja za članski in administratorski del portala.

---

## Omejitve

- Podatkovna baza mora biti **Oracle** (obstoječe licence v podjetju).
- Izračun točk je periodičen in vezan na mesečni cikel (1x mesečno za pretekli mesec).
- Sistem je odvisen od podatkov o nakupih iz obstoječega poslovnega IS.
- Kartica lojalnosti se pošilja po navadni pošti (operativna omejitev procesa).
- Pravila programa so v grobem statična; pričakovane so spremembe vrednosti, ne pa popolna sprememba logike.
- Eksplicitne pravne zahteve (npr. skladnost s predpisi varstva osebnih podatkov) v izvoru niso navedene.

---

# 4. Vmesniki

## Podatkovni vmesnik do Oracle DB

- Branje/pisanje članov, statusov, točk, pravil, nagrad in analitičnih podatkov.

## Vmesnik za potrjevanje e-pošte

- **Predpostavka A4:** potreben je integracijski mehanizem za pošiljanje/verifikacijo e-pošte ob registraciji.

## Podpora procesu pošiljanja kartic

- **Predpostavka A5:** sistem mora zagotoviti podatke/izvoz za proces fizičnega pošiljanja kartic po pošti.

---

# 5. Slovar izrazov

| Izraz                   | Opis                                                                     |
| ----------------------- | ------------------------------------------------------------------------ |
| Program lojalnosti      | Sistem pravil in ugodnosti za nagrajevanje nakupne aktivnosti strank.    |
| Član programa           | Stranka, ki je vključena v program in ima kartico/račun.                 |
| Status lojalnosti       | Nivo člana (osnovni, bronasti, srebrni, zlati), ki vpliva na točkovanje. |
| Točke zvestobe          | Enote nagrajevanja, dodeljene na podlagi mesečnih nakupov in statusa.    |
| Mesečni obračun         | Periodični izračun točk za pretekli mesec.                               |
| Točkovnik               | Pravila za pretvorbo zneska nakupov + statusa v točke.                   |
| Prehod statusa          | Sprememba statusa člana glede na izpolnjevanje pragov nakupov.           |
| Poslovni IS             | Obstoječi informacijski sistem trgovske verige, vir podatkov o nakupih.  |
| Portal                  | Spletna aplikacija za člane in administratorje.                          |
| Unovčevanje točk        | Koriščenje zbranih točk za nagrade/ugodnosti.                            |
| Nakupni program         | Vsebine, povezane s ponudbo za člane (izraz iz izvornega besedila).      |
| Program nagrad          | Nabor nagrad/ugodnosti, ki so na voljo za točke.                         |
| Konfigurabilnost pravil | Možnost spreminjanja vrednosti pravil brez večjih sprememb sistema.      |
