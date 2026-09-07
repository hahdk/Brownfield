# PRD – CisTisp Prototype

## 1. Produktvision

CisTisp (**Customer Investment Selection Translator Into SecID Portfolio**) oversætter kundens investeringsvalg i Flex-universet til en vægtet portefølje af Morningstar SecID’er, som kan analyseres i Appension/Fondliste.

Prototypen skal demonstrere:

**Kundevalg ? CisTisp ? SecID’er og vægte ? Appension-analyse**

## 2. Problem

Flex-universet er profilbaseret, mens analyseværktøjet forventer konkrete fonds-ID’er og vægte.

Kunden vælger blandt andet:

- Livscyklus
- Fastprofil
- Selvvælger
- Gennemsnitsrente
- Produkt eller investeringsvalg
- Risikoniveau, hvor det er relevant
- Tid til pension for Livscyklus
- Fordeling mellem flere investeringsvalg

Kunden vælger ikke nødvendigvis de underliggende risikofonde direkte. Der mangler derfor et oversættelseslag mellem kundevalget og de konkrete fonds-ID’er.

Hvert investeringsvalg skal holdes i sin egen sub-portefølje, indtil sub-porteføljerne samles til den endelige portefølje.

## 3. Mål

Prototypen skal kunne:

1. Modtage et eller flere investeringsvalg.
2. Gruppere hvert investeringsvalg i sin egen sub-portefølje.
3. Oversætte Livscyklus og Fastprofil til underliggende risikofonde via konfigurerede fordelingsregler.
4. Håndtere Gennemsnitsrente med produktet AP Stabil.
5. Håndtere Selvvælger med 32 individuelle fonde, som senere bindes direkte til vores fondsliste.
6. Knytte risikofonde til deres unikke Morningstar SecID.
7. Beregne og aggregere vægte i sub-porteføljerne.
8. Samle sub-porteføljerne til en samlet portefølje.
9. Vise porteføljesammensætning og beholdningsdata.
10. Generere et link til Appension/Fondliste med SecID’er og vægte.

## 4. Brugere

### Primære brugere

- Rådgivere og mæglere.
- Kunder med opsparing i AP Pension.

### Prototypebrugere

- En rådgiver, der vil vise, hvad kundens investeringsvalg består af.
- En kunde, der vil simulere konsekvenserne af nye investeringsvalg.

## 5. MVP-scope

Der skal være en enkel webfront, hvor brugeren kan sammensætte sin portefølje af flere investeringsvalg.

For hvert investeringsvalg skal brugeren kunne angive:

- Investeringstype.
- Produkt eller investeringsvalg.
- Relevant risikovalg.
- Relevant tid til pension.
- Andel af den samlede portefølje i procent.

Alle beløb er i DKK.

Prototypen skal vise:

- Den samlede porteføljeværdi.
- Fordelingen mellem investeringsvalgene.
- Den anvendte oversættelsesregel.
- De underliggende fonde.
- Morningstar SecID’er.
- Beregnede vægte.
- Samlet portefølje.
- Link til Appension/Fondliste.

Fordelingsreglerne baseres i første omgang på manuelt transskriberede screendumps og gemmes i versionerede JSON-filer.

## 6. Produkter og valgmuligheder

### 6.1 Livscyklus

Investeringsvalg:

- Active
- Omtanke
- Basis

Risikovalg:

- Høj
- Mellem
- Lav

Tid til pension:

- 0–30 år

Livscyklus har både:

- Andel i procent.
- Værdi af andelen i DKK.

Andelens værdi beregnes ud fra den samlede porteføljeværdi:

`andelens værdi = samlet porteføljeværdi × andel i procent / 100`

### 6.2 Fastprofil

Investeringsvalg:

- Active
- Omtanke
- Basis

Risikovalg:

- Lille aktieandel
- Mellem aktieandel
- Stor aktieandel
- Meget stor aktieandel

Fastprofil har ikke noget valg for tid til pension eller udløb.

### 6.3 Gennemsnitsrente

Gennemsnitsrente indeholder kun:

- AP Stabil

Der er ikke behov for valg af risikoniveau eller tid til pension for Gennemsnitsrente.

### 6.4 Selvvælger

Selvvælger indeholder 32 individuelle fonde.

De 32 fonde har allerede unikke SecID’er, men de skal ikke mappes gennem CisTisps fordelingsregler. De skal senere bindes direkte til vores fondsliste, når fondlisten leveres.

I prototypen kan pladserne håndteres som placeholders, indtil fondlisten er tilgængelig.

## 7. Primært brugerflow

1. Brugeren åbner prototypen.
2. Brugeren tilføjer et investeringsvalg.
3. Brugeren vælger investeringstype.
4. Brugeren vælger produkt eller investeringsvalg.
5. Brugeren vælger relevant risikoniveau.
6. Brugeren vælger tid til pension, hvis investeringstypen er Livscyklus.
7. Brugeren angiver investeringsvalgets andel i procent.
8. Brugeren kan tilføje flere investeringsvalg.
9. Systemet viser andelens værdi i DKK, hvor det er relevant.
10. Systemet validerer, at de samlede andele er 100 %.
11. CisTisp anvender de konfigurerede fordelingsregler.
12. Hvert investeringsvalg oversættes til sin egen sub-portefølje.
13. Resultater med samme SecID lægges sammen.
14. Den samlede portefølje vises.
15. Brugeren kan åbne eller kopiere et Appension/Fondliste-link.

## 8. Forretningsregler

1. En samlet portefølje består af en procentandel af Livscyklus, Fastprofil, Selvvælger og/eller Gennemsnitsrente.
2. Brugeren skal kunne angive procentandelen for hvert investeringsvalg.
3. Summen af alle investeringsvalg skal være 100 %.
4. Livscyklus indeholder Active, Omtanke og Basis.
5. Fastprofil indeholder Active, Omtanke og Basis.
6. Active, Basis og Omtanke er investeringsvalg under Livscyklus og Fastprofil.
7. Livscyklus har risikoniveauerne Høj, Mellem og Lav.
8. Livscyklus har tid til pension fra 0 til 30 år.
9. Fastprofil har risikovalgene Lille aktieandel, Mellem aktieandel, Stor aktieandel og Meget stor aktieandel.
10. Fastprofil har ingen tid til pension eller udløb.
11. Gennemsnitsrente indeholder kun AP Stabil.
12. Kunden vælger ikke de underliggende risikofonde direkte for Livscyklus og Fastprofil.
13. Risikoniveau og tid til pension bestemmer fordelingsreglen for Livscyklus og Fastprofil, hvor det er relevant.
14. En risikofond er samtidig en intern fond og udgør ikke et separat fondslag.
15. Hver risikofond har præcis ét unikt Morningstar SecID.
16. Selvvælgerfondene har allerede unikke SecID’er og skal ikke mappes gennem fordelingsregler.
17. Selvvælgerfondene skal senere bindes direkte til vores fondsliste.
18. Sub-porteføljerne holdes adskilt, indtil den samlede portefølje beregnes.
19. Den underliggende fondsvægt beregnes som:

    `inputvægt × fordelingsvægt`

20. Identiske SecID’er skal aggregeres.
21. Summen af outputvægtene skal være 100 %.
22. Beregninger skal udføres med høj præcision.
23. Vægte vises med to decimaler.
24. Efter afrunding justeres den største post, hvis det er nødvendigt for at få den viste sum til 100 %.
25. Manglende SecID i en mapping for Livscyklus, Fastprofil eller Gennemsnitsrente er en valideringsfejl.
26. Et Selvvælger-slot uden binding til fondlisten kan vises som placeholder, men må ikke bruges til at generere et endeligt link.
27. Beregningsregler og mappings skal ligge i konfiguration og ikke i UI-koden.

## 9. Inputvalidering

Systemet skal validere:

- Påkrævede felter.
- Gyldig investeringstype.
- Gyldigt produkt eller investeringsvalg.
- Gyldigt risikoniveau.
- Tid til pension mellem 0 og 30 år for Livscyklus.
- Ingen tid til pension for Fastprofil.
- Andele mellem 0 og 100 %.
- Samlet porteføljefordeling på præcis 100 %.
- Positiv samlet porteføljeværdi, hvis den angives.
- At fordelingsregler summerer til 100 %.
- At alle nødvendige risikofonde har et SecID.
- At Selvvælger-fonde er bundet til fondlisten, før et endeligt link genereres.

Hvis inputvægtene ikke summerer til 100 %, skal systemet afvise beregningen og vise en tydelig fejl. Automatisk normalisering er ikke standardadfærd.

## 10. Standardanbefaling

Brugeren skal kunne indlæse en preset med:

- 66,67 % Active.
- 33,33 % Omtanke.
- Samme relevante risikoniveau.
- Samme tid til pension, hvis valgene er Livscyklus.

## 11. Konfiguration

Mappings gemmes i JSON og versioneres, eksempelvis:

- `mappings/v1.json`
- `mappings/schema.json`

Konfigurationen skal kunne indeholde:

- Version og metadata.
- Investeringstype.
- Produkt.
- Risikoniveau.
- Tid til pension, hvis relevant.
- Underliggende risikofonde.
- Fordelingsvægt.
- Unikt SecID.
- Selvvælger-slots og senere binding til fondlisten.

Den første version af mappings baseres på manuelt transskriberede screendumps. Senere kan maskinel levering, upload eller API understøttes.

## 12. Appension/Fondliste-link

Linket skal genereres med følgende format:

`https://appension.fondliste.dk/da/2/portfolio/analysis?holdings=...`

Parameteren `holdings` indeholder en URL-encodet JSON-liste med:

- `securityId`
- `weight`

Eksempel på data i linket:

```json
[
  {
    "securityId": "F00002701P",
    "weight": 6.67
  },
  {
    "securityId": "F00002701Q",
    "weight": 6.67
  }
]
```

Linket skal kunne åbnes og kopieres fra resultatvisningen.

## 13. UI-krav

Prototypen skal have tre hovedområder:

### Kundevalg

Formular til:

- Investeringstype.
- Produkt eller investeringsvalg.
- Relevant risiko.
- Tid til pension for Livscyklus.
- Andel i procent.
- Samlet porteføljeværdi i DKK.
- Tilføjelse, redigering og sletning af investeringsvalg.

### Oversættelse

Vis en forklaring af:

- Hvilken fordelingsregel der anvendes.
- Hvilke underliggende fonde der anvendes.
- Fordelingsvægten for de underliggende fonde.
- Hvilken sub-portefølje valget tilhører.

### Resultat

Vis:

- Fond.
- Morningstar SecID.
- Beregnet vægt.
- Samlet porteføljevægt.
- Samlet portefølje.
- Link til Appension/Fondliste.
- Mulighed for at kopiere linket.

UI’et skal være på dansk, fungere på desktop og være enkelt nok til en rådgiverdemo.

## 14. Fejlhåndtering

- Feltfejl vises inline ved det relevante felt.
- Beregningsfejl vises tydeligt ved beregningsområdet.
- Manglende mappings eller SecID’er skal forklare, hvad der mangler.
- Linkgenerering blokeres, hvis porteføljen indeholder ubundne Selvvælger-fonde.
- Brugeren skal kunne se, hvorfor en beregning ikke kan gennemføres.

## 15. Acceptkriterier

Prototypen accepteres, når:

- Brugeren kan oprette, redigere og slette investeringsvalg.
- Brugeren kan kombinere flere investeringstyper.
- Livscyklus viser de korrekte produkter, risici og pensionshorisont.
- Fastprofil viser de korrekte produkter og aktieandelsvalg uden pensionshorisont.
- Gennemsnitsrente kun viser AP Stabil.
- Selvvælger understøtter 32 slots som placeholders.
- Inputfordelingen valideres til 100 %.
- Underliggende vægte beregnes korrekt.
- Identiske SecID’er aggregeres korrekt.
- Outputvægtene summerer til 100 %.
- Anvendte fordelingsregler vises.
- Appension/Fondliste-link genereres i det aftalte format.
- Linket kan kopieres.
- Standardanbefalingen kan indlæses.
- Demoen kan åbnes som en selvstændig HTML-fil uden serverafhængighed.
