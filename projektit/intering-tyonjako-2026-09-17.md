# Intering-frontti: työnjako ja sen talous

**SISÄINEN. Ei mene Vipetille, Viiville eikä Tommille.** Tommin oma dokumentti on
[tommi-tyopaketit-2026-09-17.md](tommi-tyopaketit-2026-09-17.md), eikä siinä ole
kapasiteetti- eikä katelukuja.

**Päivämäärä:** 2026-09-17
**Tilanne:** projekti tilattu 15.9. (kiinteä hinta), julkaisu 30.10.

## 1. Jako

|              | Osuus             | Tunteina (7,5 h/htp)           | Tarjouksen rivit       |
| ------------ | ----------------- | ------------------------------ | ---------------------- |
| Mikko        | 7,25 - 13 htp     | 54 - 98 h, keskikohta **76 h** | 1, 2, 3, 6, 12, 13, 14 |
| Tommi        | 7,25 - 12 htp     | 54 - 90 h, keskikohta **72 h** | 4, 5, 7, 8, 9, 10, 11  |
| **Yhteensä** | **14,5 - 25 htp** |                                | vastaa tarjousta       |

Mikon keskikohta on **10,1 htp**, joka oli tavoite.

**Profiilisivu (rivi 3) siirtyi kokonaan Mikolle.** Aiemmassa versiossa se oli jaettu
datakerrokseen ja esitykseen, mikä oli suunnitelman heikoin kohta. Profiilisivu on
hakukonelupauksen ydin ja kytkeytyy suoraan kenttäkartoitukseen, joka tehdään asiakkaan
kanssa. Tommille jää profiilikortti listauksessa, Mikolle koko sivu.

**Illat:** varattu aika on 12 h/vko, josta kertyy julkaisuun 22.10. mennessä 64 h. Keskikohta
vaatii 76 h, eli vajaa on **12 h koko jaksolta = noin 2,3 h viikossa.** Yksi ilta viikossa
riittää. Jos htp on käytännössä 6 h, tarve on 61 h eikä iltoja tarvita lainkaan.

## 2. Talous

Tommi 60 €/h. Könttä riippuu siitä montako tuntia htp on, ja haarukka on leveä:

|           | alaraja 7,25 htp | keskikohta 9,6 htp | yläraja 12 htp |
| --------- | ---------------- | ------------------ | -------------- |
| 6 h/htp   | 2 610 €          | 3 465 €            | 4 320 €        |
| 7,5 h/htp | 3 262 €          | **4 331 €**        | 5 400 €        |
| 8 h/htp   | 3 480 €          | 4 620 €            | 5 760 €        |

Koko haarukka on siis **2 600 - 5 800 €**, mikä on 31 - 68 % projektin hinnasta. Se on liian
leveä tuntilaskutukseen kiinteähintaisessa projektissa.

**Suositus: 4 000 € könttänä paketeista T1 - T7 sellaisina kuin ne on kirjattu.**

| Könttä      | Osuus hinnasta | Jää Mikolle | Mikon €/pv | Tommin €/h jos 72 h |
| ----------- | -------------- | ----------- | ---------- | ------------------- |
| 3 500 €     | 41 %           | 5 000 €     | 494 €      | 49 €                |
| **4 000 €** | **47 %**       | **4 500 €** | **444 €**  | **56 €**            |
| 4 300 €     | 51 %           | 4 200 €     | 415 €      | 60 €                |
| 5 000 €     | 59 %           | 3 500 €     | 346 €      | 69 €                |

**Miksi könttä eikä tunnit.** Viiville myytiin kiinteä hinta, eli ylityksen riski on jo Aihulla.
Jos Tommille maksetaan tunneista, sama riski kertautuu: jos hänen osuutensa venyy ylärajaan,
lasku on 5 400 € ja Mikolle jää 3 100 € omasta 13 htp:staan eli 238 €/pv. Könttä siirtää
saman rakenteen eteenpäin: Tommi saa varmuuden, Aihu saa katon. Se on sama kauppa jonka Mikko
teki Viivin kanssa.

Ehto: könttä sitoo laajuuden. Jos Tommille tulee lisää, siitä sovitaan erikseen eikä sitä
oleteta sisältyvän.

**Se mitä tämä paljastaa hinnoittelusta.** 8 500 € on 14,17 htp à 600 €/pv, eli **alle arvion
oman alarajan 14,5**, ja se laskettiin yhdelle tekijälle. Kahden tekijän kokonaistyö on sama
14,5 - 25 htp, mutta nyt siitä pitää maksaa kahdelle. Mikään könttä ei siis pidä Mikkoa
600 eurossa päivältä: jotta niin kävisi, Tommille jäisi 2 400 €, mikä on 40 tuntia eli
selvästi alle sovitun laajuuden. Kate tulee Mikon päivähinnasta, ja se on 444 € suositellulla
köntällä. Tämä ei ole uusi tieto vaan sama asia joka kirjattiin tarjousta tehdessä: myönnytys
ei tullut laajuudesta vaan katteesta.

## 3. Miten kaksi tekijää mahtuu samaan koodipohjaan

Tarjouksen kohdassa 3.6 lukee: _"Kaksi tekijää samassa koodipohjassa kiinteällä hinnalla on
tapa hidastaa molempia."_ Se pitää paikkansa, ja siksi jako ei ole tehtävälista vaan
**tiedostoraja**.

**Mikko omistaa datakerroksen:** Softr-haku, profiilisivu, uudelleenohjaukset, julkaisu.
**Tommi omistaa esityskerroksen:** komponentit, listaus, lohkot, sivupohjat, tyylit.

Väliin kirjoitetaan kaksi tiedostoa, jotka jäädytetään:

```
src/lib/profile-contract.ts   Profiilin tyypit
src/lib/mock-profiles.ts      66 keksittyä profiilia oikeassa muodossa
```

Testidata jäljittelee oikean aineiston reunatapauksia: 5 % ilman sijaintia, 26 % ilman CV:tä,
47 % ilman Y-tunnusta, tageja 1 - 18 per profiili. Näin tyhjät kentät löytyvät kehittäessä
eivätkä tuotannossa.

**Tommi ei saa Softrin avaimia, Vercelin tunnuksia eikä asiakkaan henkilötietoja.** Se seuraa
jaosta luonnostaan ja on tietosuojan kannalta oikein: 66 ihmisen yhteystiedot pysyvät yhdellä
koneella.

## 4. Mikon osuus

| Rivi | Mitä                                                                                    | Arvio      |
| ---- | --------------------------------------------------------------------------------------- | ---------- |
| 1    | Perustus: ympäristöt, tietokanta, verkkotunnukset, julkaisuputki                        | 1 - 2      |
| 2    | Softr-integraatio, kenttäkartoitus asiakkaan kanssa, liitteiden kopiointi omaan mediaan | 2 - 3,5    |
| 3    | Profiilisivu kokonaan: data, esitys, rakennettu data, hakukonekentät                    | 1,5 - 2,5  |
| 6    | Sivukartoitus nykyisestä sivustosta                                                     | 0,25 - 0,5 |
| 12   | Osoitteet ja uudelleenohjaukset                                                         | 1 - 2      |
| 13   | Jäsenalueen linkitys                                                                    | 0,5        |
| 14   | Julkaisu ja mittaus                                                                     | 1 - 2      |

Ennen kuin Tommi voi aloittaa, Mikolta tarvitaan noin 0,5 htp: tyyppisopimus ja testidata
`main`iin. Se on koko jaon edellytys ja sisältyy riviin 2.

Lisäksi Mikolta tarvitaan Tommille kaksi syötettä, jotka eivät ole koodia: **nykyisen sivuston
sisällöt tekstinä** (T3) ja **etusivun ja liity-sivun tekstit** (T5).

## 5. Kriittinen polku

Kulkee Tommin T3:n kautta. Sen siirtolista vanhoista osoitteista on edellytys Mikon riville 12,
eikä julkaisua ole ilman uudelleenohjauksia. T3 pitää siis aloittaa aikaisin eikä jättää
loppuun, vaikka se on esityskerrosta.

Toinen riippuvuus on asiakkaalla: kenttätaulukko ja sijaintikentän siistiminen Softrissa,
takaraja 1.10. Ilman niitä rivi 3 rakennetaan oletuksilla ja mahdollisesti kahdesti.

## 6. Mitä menee projektirepoon

Repoon `intering-frontti` menee vain se mikä on teknisesti tarpeen: tyyppisopimus, testidata ja
PR:t. **Omistajuus ei mene repon `TODO.md`:hen.** Rekisteri kertoo mitä on tehty ja millä
todisteella, ei kuka teki. Se on oikea rajaus muutenkin: rekisteri on asiakkaalle luovutettava
dokumentti, resursointi ei.

Tarjous ei lupaa henkilökohtaista suoritusta vaan kiinteän hinnan ja sen että Aihu vastaa
luovutetusta sivustosta, joten kokoonpanon kertomatta jättäminen ei ole ristiriidassa minkään
kanssa mitä asiakkaalle on sanottu.

Jos repon historian halutaan näyttävän yhdeltä tekijältä, tavallinen tapa on repokohtainen
commit-identiteetti (`git config user.name "Aihu Agency"` repon sisällä). Punnittavaa: jos
Viivi ostaa kohdan 8.1 ja saa repon, historia on hänelle ylläpidon työkalu, ja siinä
hyödyllisintä on hyvä commit-viesti eikä tekijän nimi.
