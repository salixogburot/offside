# Offside for nybegynnere – ressursfil for visuell quiz

> Denne filen er ment som kontekst/ressurs for Claude Code når det skal bygges en enkel, visuell quiz om offside. Den inneholder formål, regelgrunnlag, forenklede forklaringer, scenarier med koordinater og et ferdig spørsmålsutkast.

---

## 1. Formål og målgruppe

- **Mål:** Spillerne skal forstå *konseptet* offside, ikke pugge reglementet.
- **Målgruppe:** Jenter født 2015 (11–12 år) som skal begynne med **9er-fotball i 2027**. De fleste har spilt 7er-fotball der det ikke er offside, så offside er nytt.
- **Forkunnskaper:** Kan fotball (mål, pasning, forsvarer, keeper), men har ikke noe forhold til offside.
- **Varighet:** 5–10 minutter. Ca. 10–12 spørsmål i basisløypa, flere i bonusløype.
- **Språk:** Norsk bokmål. Korte setninger, hverdagsord, ingen juridisk tekst.
- **Tone:** Oppmuntrende og leken. Ingen «feil!»-skam. Feil svar gir en vennlig forklaring og en ny sjanse.

## 2. Instruksjoner til Claude Code (designbrief)

**Teknisk forslag**
- Én selvstendig nettside (HTML + CSS + JavaScript, gjerne SVG for bane og spillere). Ingen backend, ingen innlogging, ingen sporing av personopplysninger.
- Må fungere godt på mobil og nettbrett (store trykkflater), og på PC.
- Spørsmålene legges i en separat datastruktur (f.eks. JSON-array) slik at det er lett å legge til/endre scenarier uten å røre logikken.

**Visuelt**
- Se banen **ovenfra**. Vis bare motstanderens halvdel pluss litt av midtlinjen (angrepsmålet øverst).
- Angrepslag og forsvarslag skal skilles med **både farge og form/nummer** (ikke bare farge – fargeblinde og små skjermer).
- Ballen er tydelig. Pasningen vises som en pil som kan animeres.
- **Offsidelinjen:** en stiplet horisontal linje gjennom nest siste forsvarer. Vises som «hjelpelinje» i forklaringen etter svaret, og gjerne som valgfri hjelp i de første spørsmålene.
- **«Frys-øyeblikket»:** Offside vurderes i det øyeblikket pasningen spilles. Vis scenen frosset ved pasningen, og animer deretter pasningen *etter* at spilleren har svart.
- Nyttig interaksjon: la spilleren *trykke på spilleren* eller *dra offsidelinjen* i enkelte spørsmål, ikke bare velge Ja/Nei.

**Pedagogisk flyt**
1. Kort intro (3 skjermer, se «Kjerneforklaringen» under).
2. Spørsmål i nivåer (se seksjon 6). Hvert spørsmål: scene → svar → forklaring med visuell markering → neste.
3. Oppsummering: «Du kan nå offside!» med de tre reglene (se seksjon 3) og eventuelt poeng/stjerner.
4. Ingen tidspress.

**Tilgjengelighet**
- God kontrast, stor skrift, alt-tekst/beskrivelse av hver scene.
- Ikke avhengig av lyd.

---

## 3. Kjerneforklaringen (til introskjermene)

Dette er forenklingen som hele quizen bygger på. Bruk gjerne akkurat disse formuleringene.

**Idé:** Offside finnes for at ingen skal kunne stå og vente helt fremme ved mål og bare få ballen.

**Regel 1 – Offsideposisjon (hvor står du?)**
Du står i *offsideposisjon* hvis du er **nærmere motstandernes mållinje enn både ballen og den nest bakerste motstanderen**.
- Som oftest er keeperen bakerst, og da er det den bakerste *utespilleren* som er «nest bakerst».
- Står du **på linje** med nest bakerste motstander, er du **ikke** offside.
- Er du **bak ballen** eller på linje med den, er du **ikke** offside.

**Regel 2 – Bare på motstanderens halvdel**
Du kan bare være offside på **motstandernes banehalvdel**. På din egen halvdel kan du aldri være offside.

**Regel 3 – Det er ikke ulovlig å stå offside, men å *bli med i spillet* fra offsideposisjon**
Du får bare offside hvis du står i offsideposisjon **og** blir med i spillet ved å:
- røre ballen, eller
- *forstyrre en motspiller* (f.eks. stå i veien for keeperens sikt, eller klart utfordre en motspiller om ballen), eller
- *dra nytte av posisjonen* (f.eks. få ballen etter at den spretter tilbake fra stolpe/tverrligger/motspiller).

**Regel 4 – Unntak**
Du kan **aldri** være offside når du får ballen **direkte** fra **målspark, innkast eller hjørnespark**.

**Regel 5 – Hva skjer når det er offside?**
Dommeren blåser, og motstanderlaget får **indirekte frispark** der offsidespilleren var da hun ble straffet.

**Huskeregel (forslag):** *«Se på tre ting: Hvor er ballen? Hvem er nest bakerst? Hvor står jeg – og tar jeg del i spillet?»*

---

## 4. Ordliste (kan brukes som «hjelp»-knapp i quizen)

| Ord | Enkel forklaring |
|---|---|
| Mållinje | Linjen bak målet, ytterst på banen. |
| Midtlinje | Linjen som deler banen i to halvdeler. |
| Nest siste motspiller | Den motstanderen som er nest nærmest sitt eget mål (keeperen er som regel nærmest). |
| Offsideposisjon | At du står nærmere motstandernes mål enn både ballen og nest bakerste motspiller. Dette alene er *ikke* ulovlig. |
| Offside | Når du står i offsideposisjon **og** deltar i spillet. Da blåser dommeren. |
| Indirekte frispark | Frispark som ikke kan gå rett i mål; en annen spiller må røre ballen først. |
| Målspark / Innkast / Hjørnespark | Igangsettinger der du aldri kan være offside når du får ballen direkte. |
| Synslinje | Linjen mellom keeperen og ballen. Står du i veien, kan du «blokkere sikten». |

---

## 5. Regelgrunnlag fra kildene

### 5.1 NFF – «Retningslinjer Regel 11 – Offside», april 2022
- **Offsideposisjon:** «en del av hodet, kroppen eller ben er nærmere motstanderens mållinje enn både ballen og nest siste motspiller.»
- **Kroppsdeler:** Den samme kroppsdelen som kan dømmes hands hvis den berører ballen, skal **ses bort fra** i offsidevurderingen. I praksis: **armene teller ikke** (overarmen fra armhulen og ned). Hode, overkropp (inkl. skulder) og bein teller.
- **Straffes kun hvis spilleren** deltar i spillet (berører ballen), forstyrrer motspiller (hindrer synslinje, klart utfordrer om ballen, åpenbart forsøker å spille ballen) eller drar fordel av posisjonen (etter retur/stuss fra stolpe/tverrligger/motspiller, eller etter bevisst redning av motspiller).
- **Kun på motstanderens halvdel:** Straffbar offsideposisjon forutsetter at *hele kroppen* har krysset midtlinjen.
- **På linje** med nest siste forsvarsspiller = ikke straffbar offsideposisjon.
- **Motspiller spiller ballen til deg:** Hvis en motspiller *spiller* ballen og du mottar den, har du ikke fått noen fordel og skal ikke straffes (forskjellig fra at ballen bare *stusser* av motspiller/stolpe).
- **Stuss eller retur** fra stolpe, tverrligger, dommerteam eller motspiller(e), eller etter at ballen er *reddet* av motspiller, gir fordel → offside kan dømmes.
- **Redning** = en spiller stopper (eller forsøker å stoppe) en ball som er på vei i mål eller veldig nær, med en hvilken som helst kroppsdel unntatt armene (unntatt målvakten i eget straffesparkfelt).
- **Forstyrrer motspiller (illustrasjon):** Hvis en angriper i offsideposisjon klart står i veien for keeperens synslinje, skal hun straffes. Hvis hun ikke forstyrrer noen og ikke berører ballen, skal hun ikke straffes.
- **Drar fordel (illustrasjon):** En angriper som er offside når en medspiller *spiller* ballen, kan straffes hvis ballen deretter blir endret/spretter/reddes og hun spiller den. Men hvis den *første* spilleren var onside da ballen ble spilt, og ballen deretter går via en annen onside medspiller, kan spilleren ikke straffes bare fordi posisjonen er annerledes senere – avgjørende er posisjonen **da ballen ble spilt av medspilleren**.
- **Unntak:** Direkte fra **målspark, innkast, hjørnespark** → aldri straffbar offsideposisjon.
- **Igangsetting:** Indirekte frispark fra stedet der spilleren var da hun ble straffet (gjelder også på egen banehalvdel).
- **Tilleggsvurderinger (avansert):** Forsvarer som forlater banen uten tillatelse regnes som å stå på mållinjen/sidelinjen. Angriper som forlater banen bak mållinjen og kommer inn igjen før første stans, regnes som å ha stått på mållinjen. Bevisst å forlate banen for å unngå offside og så komme ulovlig inn igjen gir advarsel (gult kort). **Anbefaling: Utelates fra quizen for denne målgruppen.**

### 5.2 «Spilleregler – 9er fotball» (relevant for offside)
- Det følges spilleregler for **elleverfotball** med tilpasninger.
- **Spillebanen:** På tvers av elleverbanen (dvs. mindre bane enn full bane).
- **Spillere:** 9 per lag inkludert keeper.
- **Offside:** «Offsideregel praktiseres som i elleverfotball. NB! Det er ikke offside ved målspark.»
- Andre tilpasninger i 9er (innbytter, spilletid 2 × 15 min, straffespark fra 8 m, utvisningsregler for gult kort m.m.) er **ikke relevante for offsidequizen**.

### 5.3 Supplement utover kildene (standardregel, ikke eksplisitt i de to dokumentene)
- Offsideposisjon vurderes i **det øyeblikket ballen spilles av en medspiller**. Hva spilleren gjør *etter* det, endrer ikke posisjonen. Dette er sentralt for «frys-øyeblikket» i quizen.
- Forsvarende keeper regnes som en motspiller på lik linje med utespillere.

### 5.4 Forbehold
Kilden er fra **april 2022**. Før quizen deles med laget/foreldre bør innholdet **sjekkes mot gjeldende Fotballens Lover/NFF-veiledning**, og at 9er-tilpasningene fortsatt gjelder for 2027-sesongen.

---

## 6. Pedagogisk trapp (nivåer)

| Nivå | Tema | Innhold |
|---|---|---|
| **1 – Grunnidé** | Hvor står jeg i forhold til forsvarerne? | Nest bakerste, offsidelinjen, «på linje er OK», «bak ballen er OK» |
| **2 – Når blir det faktisk offside?** | Delta i spillet | Offsideposisjon alene er lov; røre ballen; egen halvdel; unntak (målspark/innkast/hjørne); frispark |
| **3 – Bonus (valgfritt)** | Litt vanskeligere | Blokkere keeperens sikt, retur fra stolpe, armer teller ikke, motspiller spiller ballen til deg |

Anbefaling: Nivå 1 og 2 er «kjernen» (ca. 10 spørsmål). Nivå 3 som valgfri bonusrunde.

---

## 7. Scenemodell for visuelle scenarier

**Koordinatsystem (normalisert, 0–100):**
- `x`: 0 = venstre sidelinje, 100 = høyre sidelinje.
- `y`: 0 = eget mål (mållinje), **50 = midtlinjen**, 100 = motstandernes mållinje (angrepsretning = økende y).
- «Nærmere motstandernes mållinje» betyr **høyere y**.
- Angrepslag (spillerens lag) = «A-spillere»; forsvarslag (motstander) = «D-spillere» og keeper «K».
- **Nest siste motspiller** = den av D/K med nest høyest y. (Keeper er vanligvis høyest y.)
- Offsideposisjon (for en angriper X) ⇔ `X.y > ball.y` **og** `X.y > nestSiste.y` **og** `X.y > 50`.

Under er scenene som forslag. Plasser gjerne spillerne litt ulikt i x for å se naturlig ut, men **ikke endre y-verdiene** uten å sjekke fasiten.

### Scene S1 – Onside (på riktig side av forsvareren)
- Ball/pasningsgiver A1: x=40, y=30
- Mottaker A2: x=55, y=60
- D1: x=45, y=75 (nest siste), D2: x=65, y=55, K: x=50, y=96
- Pasning A1 → A2 (løp).
- **Fasit:** Ikke offside. A2.y (60) < nest siste (75).

### Scene S2 – Offside (foran nest siste)
- A1 (ball): x=40, y=30
- A2: x=55, y=85
- D1: x=45, y=75 (nest siste), D2: x=65, y=55, K: x=50, y=96
- Pasning A1 → A2, A2 tar imot.
- **Fasit:** Offside. A2.y (85) > nest siste (75) og > ball (30), og hun rører ballen.

### Scene S3 – På linje
- A1 (ball): x=40, y=30
- A2: x=60, y=75
- D1: x=45, y=75, D2: x=65, y=55, K: x=50, y=96
- **Fasit:** Ikke offside – på linje med nest siste.

### Scene S4 – Bak ballen
- A1 med ball: x=40, y=88
- A2: x=55, y=80 (bak/ved siden av ballen, men foran D1)
- D1: x=45, y=70 (nest siste), K: x=50, y=96, D2: x=65, y=55
- **Fasit:** Ikke offside – hun er bak ballen (A2.y < ball.y).

### Scene S5 – Egen halvdel
- A1 (ball): x=40, y=20
- A2: x=55, y=45 (egen halvdel)
- D1: x=45, y=40, D2: x=65, y=30, K: x=50, y=96 (forsvarerne har rykket høyt)
- **Fasit:** Ikke offside – A2 er på egen banehalvdel (y < 50).

### Scene S6 – Offsideposisjon, men ikke med i spillet
- A1 (ball): x=40, y=30
- A2: x=20, y=85 (offsideposisjon, langt unna spillet)
- A3: x=55, y=60 (onside, mottar pasningen)
- D1: x=45, y=75, D2: x=65, y=55, K: x=50, y=96
- Pasning A1 → A3. A2 rører ikke ballen, forstyrrer ingen.
- **Fasit:** Ikke offside. A2 står i offsideposisjon, men deltar ikke i spillet.

### Scene S7 – Målspark
- Keeper (eget lag) sparker ut fra eget mål. A2: x=55, y=85 mottar direkte.
- D1: x=45, y=75, K (motstander): x=50, y=96
- **Fasit:** Ikke offside – direkte fra målspark.
- *Varianter:* Samme scene med innkast eller hjørnespark.

### Scene S8 – Blokkerer keeperens sikt (bonus)
- A1 skyter fra x=50, y=70 (ball). A2: x=48, y=92, rett foran keeperen K (x=50, y=96), uten å røre ballen.
- D1: x=40, y=78, D2: x=60, y=75
- **Fasit:** Offside hvis A2 er i offsideposisjon (y=92 > nest siste) **og** står i veien for keeperens sikt.
- *Motstykke S8b:* A2 står i offsideposisjon men langt til siden (x=10), ikke i synslinjen → ikke offside.

### Scene S9 – Retur fra stolpe (bonus)
- A1 skyter, ballen treffer stolpen. A2 (x=60, y=85) var i offsideposisjon da skuddet ble tatt, og tar returen.
- **Fasit:** Offside – hun drar fordel av posisjonen (retur fra stolpe).

### Scene S10 – Armen (bonus)
- A2: kroppen (skulder/bein) er på linje med nest siste forsvarer, mens armen strekker seg litt forbi.
- **Fasit:** Ikke offside – armene teller ikke.

### Scene S11 – Motspiller spiller ballen til deg (bonus)
- En forsvarer spiller bevisst ballen, og den går til A2 som står i offsideposisjon.
- **Fasit:** Ikke offside – hun fikk ballen fra en motspiller som *spilte* den.

### Scene S12 – Hvor tas frisparket?
- A2 (x=70, y=82) blir dømt offside.
- **Fasit:** Indirekte frispark til forsvarerne, tatt fra der A2 sto (x=70, y=82).

---

## 8. Spørsmålsutkast (norsk, klart til bruk)

Format per spørsmål: `id`, `nivå`, `scene`, `spørsmål`, `svaralternativer`, `riktig svar`, `forklaring (vises etter svar)`.
Bruk gjerne «Pip! Offside!» som tilbakemelding når det er offside og «Spillet går videre!» når det ikke er det.

### Nivå 1 – Grunnidé

**Q1** · scene S1
- *Spørsmål:* Pasningen spilles nå! Står den blå spilleren (A2) offside?
- *Alternativer:* Ja / Nei
- *Riktig:* **Nei**
- *Forklaring:* Hun står *bak* den nest bakerste forsvareren. Da er hun ikke i offsideposisjon.

**Q2** · scene S2
- *Spørsmål:* Pasningen spilles nå! Står A2 offside?
- *Riktig:* **Ja**
- *Forklaring:* A2 er nærmere mål enn både ballen og den nest bakerste forsvareren (keeperen er bakerst), og hun tar imot ballen. Da blåser dommeren!

**Q3** · scene S2 (interaktiv)
- *Spørsmål:* Trykk på den forsvareren som er **nest bakerst** (ikke regn med keeperen som bakerst).
- *Riktig:* D1.
- *Forklaring:* Keeperen er bakerst. D1 er nest bakerst. Offsidelinjen går gjennom henne.

**Q4** · scene S3
- *Spørsmål:* A2 står på samme linje som nest bakerste forsvarer. Offside?
- *Riktig:* **Nei**
- *Forklaring:* Står du *på linje* er du ikke offside. Du må være *foran* linjen.

**Q5** · scene S4
- *Spørsmål:* A1 har ballen. A2 står litt foran forsvarerne, men *ved siden av/bak* ballen. Offside?
- *Riktig:* **Nei**
- *Forklaring:* Du kan ikke være offside hvis du er bak ballen. Du må være foran ballen *og* foran nest bakerste forsvarer.

### Nivå 2 – Når blir det offside?

**Q6** · scene S5
- *Spørsmål:* A2 står foran forsvarerne, men på *vår egen* halvdel. Offside?
- *Riktig:* **Nei**
- *Forklaring:* Du kan bare være offside på motstandernes halvdel.

**Q7** · scene S6
- *Spørsmål:* A2 står langt framme i offsideposisjon, men A3 får pasningen. A2 gjør ingenting. Offside?
- *Riktig:* **Nei, spillet går videre**
- *Forklaring:* Det er ikke ulovlig å *stå* i offsideposisjon. Du blir bare dømt offside hvis du tar del i spillet.

**Q8** · scene S7
- *Spørsmål:* Keeperen sparker ut fra målspark, og A2 står langt framme og får ballen direkte. Offside?
- *Riktig:* **Nei**
- *Forklaring:* Ved målspark kan du aldri være offside. Det samme gjelder innkast og hjørnespark.

**Q9** · variant av S7 (innkast)
- *Spørsmål:* Du får ballen rett fra et innkast mens du står foran nest bakerste forsvarer. Offside?
- *Riktig:* **Nei**
- *Forklaring:* Innkast gir aldri offside når du får ballen direkte.

**Q10** · scene S2 (tidspunkt)
- *Spørsmål:* Når avgjøres det om A2 står offside – i det pasningen spilles, eller når hun tar imot ballen?
- *Alternativer:* Når pasningen spilles / Når hun tar imot ballen
- *Riktig:* **Når pasningen spilles**
- *Forklaring:* Dommeren «fryser bildet» i det en medspiller spiller ballen. Hvor du står *da*, er det som teller.

**Q11** · scene S12
- *Spørsmål:* Dommeren dømmer offside. Hva skjer?
- *Alternativer:* Straffespark / Indirekte frispark til motstanderne / Innkast / Dropp-ball
- *Riktig:* **Indirekte frispark til motstanderne**, tatt der offsidespilleren sto.

**Q12 (oppsummering)** · tilfeldig scene
- *Spørsmål:* Hva må ALLE tre stemme for at det skal bli offside?
- *Riktig:* (1) Du er nærmere mål enn ballen og nest bakerste motstander, (2) du er på motstandernes halvdel, (3) du tar del i spillet.

### Nivå 3 – Bonus (valgfritt)

**Q13** · scene S8 – Står i veien for keeperen → **Offside.** Forklaring: Hun forstyrrer keeperen ved å blokkere sikten.
**Q13b** · scene S8b – Samme posisjon, men langt til siden → **Ikke offside.**
**Q14** · scene S9 – Retur fra stolpe → **Offside.** Forklaring: Hun var i offsideposisjon da skuddet gikk, og får fordel av returen.
**Q15** · scene S10 – Armen foran → **Ikke offside.** Forklaring: Armene teller ikke, men hode, kropp og bein gjør det.
**Q16** · scene S11 – Motspiller spiller ballen til deg → **Ikke offside.**

---

## 9. Vanlige misforståelser (bygg gjerne spørsmål/«Visste du at?» rundt disse)

1. «Hvis jeg står foran forsvarerne, er jeg offside.» → Nei, bare hvis du også tar del i spillet.
2. «Keeperen teller ikke.» → Keeperen er en motspiller, men er som regel *bakerst*; det er **nest bakerste** som avgjør.
3. «Jeg er offside hvis jeg er foran ballen.» → Du må også være foran nest bakerste motspiller.
4. «Man kan bli offside på egen halvdel.» → Nei.
5. «Offside gjelder ved innkast/hjørnespark/målspark.» → Nei, aldri direkte fra disse.
6. «Det er når jeg tar imot ballen at posisjonen vurderes.» → Nei, når pasningen *spilles*.
7. «På linje er offside.» → Nei, på linje er lov.

---

## 10. Utenfor omfang (ikke ta med i quizen)

- Forsvarere/angripere som forlater banen og offsidevurdering av dette.
- Gult kort og utvisningsregler i 9er.
- Detaljer om VAR/tekniske hjelpemidler.
- Tidsbestemte utvisninger, straffespark (8 m) og innbytteregler.

---

## 11. Eksempel på datastruktur (forslag)

```json
{
  "id": "Q2",
  "level": 1,
  "scene": "S2",
  "type": "yes_no",
  "question": "Pasningen spilles nå! Står A2 offside?",
  "options": ["Ja", "Nei"],
  "correct": "Ja",
  "explanation": "A2 er nærmere mål enn både ballen og nest bakerste forsvarer, og hun tar imot ballen.",
  "highlight": ["offsideLine", "A2", "D1"],
  "players": [
    {"id": "A1", "team": "attack", "x": 40, "y": 30, "hasBall": true},
    {"id": "A2", "team": "attack", "x": 55, "y": 85},
    {"id": "D1", "team": "defence", "x": 45, "y": 75},
    {"id": "D2", "team": "defence", "x": 65, "y": 55},
    {"id": "K",  "team": "keeper",  "x": 50, "y": 96}
  ],
  "pass": {"from": "A1", "to": "A2"}
}
```

---

## 12. Kilder

- NFF: *Retningslinjer – Regel 11 – Offside* (april 2022).
- NFF: *Spilleregler – 9'er fotball* (tilpasninger til elleverfotball).
- Seksjon 5.3 er standardregler som supplement; sjekk mot gjeldende Fotballens Lover.
