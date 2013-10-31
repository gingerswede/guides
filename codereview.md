#Kodgranskning/Code review

##Innehållsförteckning
* [Vad är kodgranskning?](#vad-är-kodgranskning)
	* [Kritik](#kritik)
* [Vem kan utföra kodgransgkning?](#vem-kan-utföra-kodgranskning)
* [Best practice](#best-practice)
	* [Förslag på best practice](#förslag-på-best-practice)

##Vad är kodgranskning?
Kodgranskning, eller code review, är ett stort begrepp. Kärnan i en kodgranskning är att förbättra. Det kan vara att förbättra en befintlig kodbas, men det kan lika gärna vara för att förbättra sina egna kunskaper i språket. Men ledordet i varje kodgranskning är "förbättra".

Det handlar inte som många nybörjare tror om att hitta fel. Om du går in i en kodgranskning med ursprungspunkten att leta fel eller tar emot en kodgranskning i tron om att den är till för att hitta dina fel kommer din upplevelse av en kodgranskning att vara tämligen dålig. Om du istället har utgångspunkten att den är till för att förbättra koden eller att förbättra dina kunskaper så kommer det istället att bli en mycket angenäm upplevelse.

Vad är det vi är ute efter att förbättra? Kort sagt - allt. Vi vill få ner antalet logiska fel, vi vill förbättra läsbarheten i våran kod, och även minska antalet brott mot mjukvaruarkitekturen vi använder. Det gör att man i slutändan kommer att få sin kod mer effektiv och även mer lättöverskådlig.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

###Kritik
En del av en kodgranskning kan vara att ge kritik. Därför bör man lära sig att ge konstruktiv kritik. Både till sig själv och till andra. Jag kommer utgå ifrån att alla som läser detta någon gång har fått destruktiv kritik. Det är oftast något som inte tillför något till den som blir kritiserad. "Men vilken ful teckning" säger egentligen inget om teckningen eller hur den kan förbättras. Jämför det med "Jag gillar din teckning, men jag tror den kan bli ännu bättre om..." är ett bättre sätt att framföra det. Det finns oftast ett skäl till att en betraktare ogillar något, det kan t.ex. vara färgval på bakgrund i fallet av en teckning.

Detta är även något vi bör tänka på när vi lägger fram kritik om kod. "Den här koden är jättedålig" är inte ett så bra sätt att göra att dina resultat av en kodgranskning blir välmottaget. Att istället säga "Jag tror att om du gör såhär så kommer det bli effektivare" är ett bättre sätt att lägga fram det på. Både mot andra och mot sig själv.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Vem kan utföra kodgranskning?
Här kan buden vara olika. Men det finns några gemensamma nämnare.

* [Granskaren bör ha språkspecifika kunskaper.](#språkspecifika-kunskaper)
* [Granskaren måste känna till lokal best practice.](#lokal-best-practice)

Utöver de två så finns inte så många andra krav som behövs. Vad menas då med dessa två kryptiska rubriker?
###Språkspecifika kunskaper
Med detta menas att den som utför en kodgranskning bör kunna språket, men vissa delar av en kodgranskning kräver inte detta. Det är inte säkert att detta alltid är ett krav. Men olika språk kan ha olika funktionaliteter. Det gör att det kan bli svårt för en C programmerare att hitta språkspecifika fel i ett Javaprojekt och vice versa. Men det går även att använda en granskare som kan ett väldigt närbesläktat språk (exempelvis så kan en java-programmerare troligtvis granska C# kod etc.).
###Lokal best practice
Best practice är något som oftast är lokalt. Vad det är och ett förslag på best practices att hålla sig till går att finna [här](#förslag-på-best-practice). Men det finns oftast någon sorts lokal best practice på olika företag eller inom olika projekt. I större sådana finns dessa oftast nedskrivna. Om du inte känner till de lokala best practice föreskrifterna så fråga en kollega om vad dessa är.

För att utföra en kodgranskning bör du kunna dessa. En kodgranskning utgår nämligen till stor del utifrån vad en eventuell best practice säger i många fall. 

[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Best practice
Best practice är en uppsättning nedskrivna (men även i vissa fall onedskrivna) regler över hur kod bör utformas. Ibland är det uppenbart varför en viss regel finns, i andra fall så kan det vara gammal hävd som gör att regeln lever kvar. En sak som är ganska huvudgående för best practice är att de inte tillför till hur programmet körs, utan tillför till hur en programmerare kan tolka källkoden.

Till skillnad ifrån många andra språk så finns det ingen officiell best practice för php. Det kan skilja mellan individuella projekt och individuella företag. Det kan vara saker som i hur klammerparanteser ({ och }) skall placeras, eller hur variabler skall typsättas (ex. camel casing) men även hur många tecken en rad maximalt får innehålla.

Nedan finns några förslag på best practices, dessa kan användas som start och sedan förändras efter dina behov, eller användas till 100%.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

###Förslag på best practice
* Rader bör hållas under 80 tecken och skall hållas under 135 tecken.
	> Detta är för att text inte skall hamna utaför en läsares skärm så att de behöver bläddra i sidled i sin editor.
* Konstanter bör skrivas med versaler (stora bokstäver).
	> De flesta konstanter i php är redan i versaler. Så det finns redan en sådan standard inbyggd i språket. Detta är för att särskilja konstanter ifrån vanliga variabler och medlemsvariabler.
* Variabler och metodnamn bör skrivas med camel casing med inledande gemen.
	> I php finns det tre olika standarder i detta. De flesta ramverk och större programmeringspråk (inklusive php) använder sig av camel casing med inledande gemen (ettExempelPåCamelCasing). Detta är något som blev vanligare efter intåget av [Java](http://www.java.com/en/download/faq/whatis_java.xml). I php går det även att finna ord separerade med underscore (_) och även [hungarian notation](http://web.mst.edu/~cpp/common/hungarian.html).
* Metoder bör hållas under 30 rader.
	> Detta har samma skäl som att raders längd bör begränsas. Vid 30 rader så får oftast hela metoden plats på en skärm i höjd.
* Undvik kedjade metodanrop (train wrecks).
	> Metodanrop som är kedjade över tre led (_$obj->var->func()_) bör undvikas. Detta är för att öka spårbarheten i hur en funktion och dess resultat har kommit till sitt slutskede. Ibland kan kedjade metodanrop öka läsbarhet (se [active records](http://en.wikipedia.org/wiki/Active_record_pattern)).
* Metod- och variabelnamn skall vara talande.
	> Du bör undvika variabelnamn som `$tmp` och `$t`. Även funktionsnamn så som `c()` eller `a()` bör undvikas. Detta för att underlätta för läsare att förstå vad en variabel innehåller eller vad en funktion gör. Om variabeln innehåller ett användarnamn, kalla den då för `$username`.
* Undvik magic numbers.
	> Magic numbers är siffror som helt plötsligt befinner sig i koden. Det kan vara exempelvis `time() + 3600`. En bättre lösning är att skapa en variabel som heter `$oneHour` och tilldela den värdet `60*60`.
* Enbart dokumenterade förkortningar används.
	> Om förkortningar används (exempelvis hungarian notation) bör dessa förkortningar finnas dokumenterade så att en utvecklare som är ny till projektet kan läsa om dessa och få en förklaring på vad de betyder. Betänk att förkortningar som är uppenbara för dig kan vara grekiska för någon annan (ex. _[sut](http://xunitpatterns.com/SUT.html)_).

[Tillbaka till innehållsförteckning](#innehållsförteckning)


##Skrivet av
Ursprungligen skrivet av:

Emil Carlsson (info at gingerswede dot com) (2013-10-31)

Editerat av:

[Tillbaka till innehållsförteckning](#innehållsförteckning)