### 01
**Be ChatGPT och AIZO att applicera de fyra datalogiska delprocesserna på tärningsspelet **Stegen** från veckans övningskompendium. Skiljer sig svaren åt, och isåfall på vilket/vilka sätt?**

Skillnaden mellan dessa är att ChatGPT gav ett mer djupgående svar och bröt ner de olika delprocesserna ytterligare jämfört med svaret vi fick från AIZO.

### 02
**Be ChatGPT och Aizo att utifrån sina skapade flödesscheman även skapa pseudokod för spelet. Ser båda svaren likadana ut, eller hur skiljer de sig åt? Klistra in ett av svaren och skriv från vilken tjänst lösningen kommer från.**

Svaren såg hyfsat likadana ut. Tankeprocessen var samma. Det som skiljde de åt var att ChatGPT gav även kommentarer på pseudokoden för att få oss att förstå vad de olika delarna gör. Pseduokoden under kommer ifrån svaret vi fick från ChatGPT:

Start:
   goal ← 1                // Målet börjar vid 1

   total_rolls ← 0         // Räknare för totala antal kast



While goal ≤ 6:             // Fortsätt så länge vi inte nått steg 6

   roll ← random(1, 6)     // Slå en tärning (generera ett tal mellan 1 och 6)

   total_rolls ← total_rolls + 1   // Öka kast-räknaren



   If roll == goal:        // Kontrollera om kastet når målet

   goal ← goal + 1     // Gå till nästa mål i stegen



   Print "Total rolls:", total_rolls   // Skriv ut totala antal kast

End

### 03
**Be ChatGPT och Aizo att fixa den färdiga JavaScript-koden för spelet, samt att logga ut kontroller och resultat i konsollen. Testa koden i det medskickade programmet om det fungerar och redovisa resultatet**

Koden var identisk och fungerade, med skillnaden att Aizo använde variabelnamn på svenska. Lite skillnad i ordval till konsollmeddelanden. ChatGPT lämnade en kommentar som förklarade varje steg i koden.

### 04
**Hur tror ni att ChatGPT och Aizo skulle lösa större och mer komplicerade kodproblem? Var någonstans går gränsen tror ni för vilken typ av uppkodning där det skulle börja uppstå problem?**

Vanligt problem är att gamla metoder föreslås, t.ex. tekniker som inte längre har stöd (“depricated”), eller som inte anses vara god standard. Det känns som om ai kan föreslå mindre säkra lösningar ibland (något som ibland uppdagas om man ifrågasätter detta). Det kan nog snabbt uppstå problem när data måste valideras i flera steg.

### 05
Klistra in nedanstående CSS och be ChatGPT och Aizo att förklara vad som händer.

```
box-shadow: 12px 12px 2px 1px rgba(0, 0, 255, .2);
```

Vilka språkliga skillnader, om det finns några, kan ni se?

AIZO gav ett förenklat och mer tydligt svar än ChatGPT. Exempelvis så svarade AIZO att skuggan förflyttas nedåt och åt höger istället för på sin X- och Y-axel som ChatGPT gav som svar. Det som skilde dem åt innehållsmässigt var att ChatGPT gav även ett kodexempel på hur det skulle kunna se ut i praktiken.

### 06
Klista in följande prompt i ChatGPT:

```
Skriv om följande kod så att den fungerar:

import { errorHandler } from "../../middlewares/errorHandler.mjs";
import { validateKey } from "../../middlewares/validateKey.mjs";
import { validateRegistration } from "../../middlewares/validateRegistration.mjs";
import { sendResponse } from "../../responses/index.mjs";
import middy from '@middy/core';
import { db } from "../../services/db.mjs";
import { hashPassword } from "../../utils/index.mjs";

export const handler = middy(async (event) => {
    const user = JSON.parse(event.body);

    try {
        await db.put({
            TableName: 'user-db',
            Item: {
                username : user.username,
                password : await hashPassword(user.password)
            }
        }); 
    } catch(error) {
        return sendResponse(404, { message : 'Could not add user'});
    }

  return sendResponse(201, 'Registration successful!');
}).use(validateKey())
  .use(validateRegistration())
  .use(errorHandler());

```

Upprepa sedan steget ytterligare tre gånger genom att skriva ```Skriv om följande kod så att den fungerar:```, och klistra in den kod ChatGPT föreslagit under föregående runda.

Får ni någon gång tillbaks samma kod som ni först skickade in? Gissningsvis kommer ChatGPT lägga till ```.promise()``` i slutet av följande del i koden:

```
await db.put({
    TableName: 'user-db',
    Item: {
        username: user.username,
        password: hashedPassword,
    },
}).promise();
```

**Detta är en utdaterad funktion som inte längre fungerar på den typ av databasanrop vi gör. Varför tror ni att ChatGPT isåfall föreslår den lösningen?**

Vi fick aldrig tillbaka orginalkoden som vi skickade in. ChatGPT föreslår den lösningen (som innehåller .promise) och ger svaret för det att “Lägg till .promise(): Om du använder AWS SDK version 2, behöver du kalla .promise() för att få tillbaka ett löfte.” I senare varianter hävdar den att den ger stöd för både AWS SDK v2 och v3. Sedan tar den bort logiken för v3 igen, men ger förslag på hur man kan implementera uppdateringar.

### 07 - Anpassa ChatGPT

Be ChatGPT att beskriva skillnaderna mellan begreppen *pattern recognition* och *abstraction*, samt att ge exempel.

Klicka därefter på er profilbild uppe i det högra hörnet, och välj därefter alternativet *Anpassa ChatGPT*.

I det övre fältet skriver du in följande:

```
Jag är en nybörjare på webbutveckling som nyligen påbörjat mina studier inom frontendutveckling.
```

Och i det undre fältet skriver du in detta:

```
Jag vill att du förklarar saker för mig som att jag vore en nybörjare. Jag vill heller inte ha några raka svar, utan snarare tips på hur jag skall tänka för att lösa uppgiften själv.
```

Testa därefter att ställa samma fråga som innan om skillnaderna mellan begreppen *pattern recognition* och *abstraction*.

**Skiljer sig svaren åt, och isåfall på vilket sätt? Märker ni om er anpassning gjorde någon skillnad.**

Vi fick färre programmerings-/dator-anpassade förklaringar när vi faktiskt hade förpromtat chatGPT att förklara för oss i egenskap av frontendutvecklare, ironiskt nog. Delvis fick vi något enklare exempel (färre facktermer) när vi hade promotat den.


### 08
Klistra in följande prompt i ChatGPT:

```
Kan du skapa en funktion som tar emot ett ord och returnerar ordet med en stor bokstav i början, samt efter alla mellanslag och bindestreck?
```

**Ta sedan bort era anpassningar och ställ samma fråga igen. Märker ni några skillnader i sättet som ChatGPT svarar?**

Vi fick samma svar, med den lilla skillnaden att exemplet på användningsområdet såg lite annorlunda ut (en extra if-sats).

### 09
**I vilka scenarion kan ni som **studenter** känna att det är okej att be AI om hjälp? Och i vilka scenarion är det inte okej?**

Scenario 1 (Inte okej):
“Skriv färdig kod för hela den här hemsidan åt mig, jag vill ha en färdig hemsida med en stor herobild och en bokningsfunktion”

När man tar koden “at face value” utan att förstå vad den faktiskt gör innan man klistrar in den.

Scenario 2 (Okej):
“Någonstans i min kod förstörs layouten av ett felaktigt lagd HTML tag. Kan du hitta var denna ligger?”

“Finns det några möjliga säkerhetsrisker eller andra problem i min kod?”

### 10
**Förutom att åka dit för fusk, diskutera vilka de tre största riskerna för er som **studenter** är att använda er av AI verktyg för att lösa era uppgifter.**

Att man förlitar sig för mycket på AI när man skriver kod och därmed skriver kod som är fel då AI inte alltid gör rätt. Man kan även bli för bekväm med att använda AI och då inte lära sig det man behöver utan låter AI göra jobbet åt en. Det kan ta bort hela momentet kring att lära sig problemlösning och det tankesätt som krävs för att bli en bra programmerare.

### 11
**Vilka styrkor och svagheter / risker ser ni hos Github Copilot för er som **studenter**?**

Styrkor:
Hjälper en att snabbt skriva syntax och lägga större fokus på andra delar av kodningen. 
Man kan även stöta på “best practice”-kod när AI:n skriver korrekt kod.
AI kan användas för att underlätta felsökning när man exempelvis har mycket kod att gå igenom så kan man fråga vart problemet ligger, om man har tur så kommer AI med rätt förslag.

Svagheter:
AI kanske genererar kod som fungerar men den kanske inte alltid förklarar VARFÖR det fungerar och därmed tappar man ett inlärningsmoment.
Man kan även bli för bekväm med att använda AI och då inte lära sig det man behöver utan låter AI göra jobbet åt en. Då förstörs inlärningsmomentet.
Vid de tillfällen man får kod som fungerar men som kanske är outdated så lär man sig att använda kod som inte längre är relevant. Exempelvis HTML som ej är semantisk och använder sig av DIV:ar.

### 12
**Kan ni se några scenarion för er som **studerande** där Github Copilot skulle vara okej att använda?**

När student har förståelse för ett programmeringskoncept och kan behöva en skjuts påvägen att komma igång och få idéer. När det är tradigt att skriva alla långa ord och kommandon så är det smidigt med något som helt enkelt minskar antalet knapptryckningar. Se i övrigt fråga 9.

### 13
**Vad tycker ni verkar vara mest "najs" med Github Copilot?**

Se svaret på fråga 12.

### 14 
**Hur ser ni på våra roller som utvecklare i framtiden, där vissa oroliga röster höjs inför hotet om AI som skall ta över våra jobb på lång sikt?**

Vi är inte så oroliga för att utvecklare försvinner helt, men att tröskeln för nya utvecklare höjs. Vilket kan leda till att antalet jobb för juniora utvecklare skulle kunna bli färre.

### 15
**Vilka risker ser ni med att använda sig av AI som en källa för kodskrivande i yrkeslivet?**

Att företagshemligheter eller personuppgifter läcker ut i “etern” och kan utnyttjas av någon form av mining-teknologi. Att man tränar ai till att göra det man gör till den grad att man faktiskt gör sig själv arbetslös.

### 16
**Vilka andra AI tjänster kan vara relevanta för oss utvecklare att känna till och använda oss utav. Leta reda på 3 tjänster och skriv 3-4 meningar om vardera.**

**Algolia**
Algolia erbjuder sökverktyg för webbsidor som använder AI för att ge dynamiska resultat. Dess AI-drivna funktioner inkluderar felstavningskorrigering, synonymhantering och personalisering.

**Contentful AI**
Contentful erbjuder AI-funktioner för att generera innehåll automatiskt och föreslå förbättringar för webbplatser. Detta sparar tid vid skapandet av text och översättningar för globala sidor.

**Microsoft Azure Cognitive Services**
Azure tillhandahåller API:er för att använda AI för tal-till-text, bildigenkänning och sentimentanalys. Ett potenitellt val för webbapplikationer som behöver förbättra interaktivitet och tillgänglighet. Enkel molnbaserad implementering för skalbara AI-funktioner.

### 17
**Av de verktyg som ni letat upp samt de som tagits upp i tidigare frågor, vilket tror ni att ni skulle ha mest användning av i er roll som **studerande**, samt i er yrkesroll? Motivera.**

Vi tror att Github Copilot är det som är mest användbart i allmänhet både som student och i yrkesrollen. Det går att ställa frågor i chattverktyget som ingår och det går även att få kodförslag baserat på det som används i det projektet. Så antingen anpassat efter hur du själv skriver din kod eller hur det ser ut i koden du stöter på i din yrkesroll.
