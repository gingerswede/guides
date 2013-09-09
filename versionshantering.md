#Versionhantering
Denna guide innehåller några enkla förklaringar vad versionshantering är och tips och tricks hur man kan tänka när man versionshanterar sin kod. Den kommer inte att ta upp funktionalitet hos olika typer av versionshanteringssätt. För djupare information om hur du använder olika modeller av versionshantering bör du rådfråga den officiella dokumentationen för det systemet. Informationen här är baserad på egen erfarenhet och även till viss del forskning i ämnet.

##Innehållsförteckning
* [Vad är versionshantering?](#vad-är-versionshantering)
* [Olita typer av versionshantering?](#olika-typer-av-versionshantering)
	* [Decentraliserat](#decentraliserad-versionshantering)
	* [Centraliserat](#centraliserad-versionshantering)
* [Varför versionshantera?](#varför-versionshantera)
* [Vilka andra kan vara intressrade av min versionshantering?](#vilka-andra-är-intresserade-av-min-versionshantering)
* [När ska jag versionshantera?](#när-ska-jag-versionshantera)
* [Skrivet av](#skrivet-av)

##Vad är versionshantering
Versionshantering är ett sätt att spara olika tillstånd av din källkod. Det kan vara bra att ha för att kunna experimentera lite med olika lösningar på din kod och fortfarande ha ett tillstånd av din kod att gå tillbaka till.

[Tillbaka till innehållsförteckning](#innehallsforteckning)

##Olika typer av versionshantering
Det finns några olika sorters versionshantering. De flesta i dagsläget känner till exempelvis Git eller Subversion. Det finns givetvis flera, men jag kommer inte lista dem alla här. Det jag kommer att ta upp är skillnaden mellan centraliserad versionshantering och decentraliserad versionshantering.
###Decentraliserad versionshantering
Detta innebär att all versionhantering sker lokalt. Du kan använda en server (remote host) för att ladda upp det du har lokalt, men det sker inte automatiskt och är inte ett krav i decentraliserade versionshanteringar. Några exempel på decentraliserade versionshanteringar är [Git](http://git-scm.com/) och [Mercurial](http://mercurial.selenic.com/). Avlägsna servrar för att hålla ordning på detta och för att ladda upp information till via dessa finns att tillgå på exempelvis [GitHub](http://www.github.com), [BitBucket](http://www.bitbucket.com) eller [Google Code](http://code.google.com/). Denna typ av versionshantering är yngre än centraliserad versionshantering.
###Centraliserad versionshantering
En centraliserad versionhantering bygger på att du har en avläsgsen server (remote host) som du sparar dina commits till. Det går givetvis att ha denna server lokalt, men den är i detta fallet ett krav för att kunna versionshantera. Några mer kända centraliserade versionshanteringar är [Subversion](http://subversion.tigris.org/) och [CVS](http://cvs.nongnu.org/). Denna typ av versionshantering har funnits längre än decentraliserad versionshantering.

[Tillbaka till innehållsförteckning](#innehallsforteckning)

##Varför versionshantera
Varför ska du versionshantera då? Det finns lite olika skäl för varför du skulle vilja versionshantera. Du kanske har en jättebra fungerande applikation men känner att du vill se om du kan refaktorera eller optimera en klass. I arbetet när du refaktorerar så kommer du nästan garanterat göra fel och helt plötsligt så får du fel och din klass kan inte längre interagera med övriga applikationen. Då kan det vara bra att kunna gå tillbaka till en fungerande version. Det kanske är så att du har ett projekt med öppen källkod, då vill du säkert att andra ska ha tillgång till din kod och även visa hur du har byggt fram hela projektet. Kortfattat så handlar versionshantering i mångt och mycket om att kunna göra fel utan att du måste börja om från början med din kod. Ibland så har man ju faktiskt gjort mer än var "ångra" kommer ihåg.

[Tillbaka till innehållsförteckning](#innehallsforteckning)

##Vilka andra är intresserade av min versionshantering
När man versionshanterar kan det vara lätt att man tänker "det här är ju bara jag intresserad av" eller "dethär var en bra backup, jag laddar upp konstant". Detta är ett tankesätt som fungerar bra om du är ensam och använder en privat versionshantering. Men vad händer om du har ett publikt repositorium eller har flera kollegor som använder samma repositorium?

Några andra som kan vara intresserade av ditt repositorium kan vara:

* [Kollegor](#kollegor)
* [Forskare](#forskare)
* [Indexerings robotar](#indexerings-robotar)
* [Andra programmerare](#andra-programmerare)
* [Slutanvändare](#slutanvandare)
* [Du själv](#du-sjalv)

Dessa olika grupper har givetvis olika intresse av din kod. Men förvånansvärt nog så har de ofta liknande behov. I många fall utgår detta ifrån att ditt repositorium är publikt och open source. I några av fallen är grupperna snarlika.

###Kollegor
Dina kollegor är oftast intresserade av att ha den senaste fungerade versionen eller en viss version av applikationen för att kunna utvidga den.

###Forskare
Forkare kan vara intresserade av ditt repositorium för att exempelvis se hur din kodbas har förändrats i exempelvis refaktoriering, se hur du har byggt upp dina kommentarer, eller hur din mjukvaruarkitektur ser ut.

###Indexerings robotar
Kända förövare här är exempelvis google, yahoo och bing. Men det kan även vara exempelvis github eller bitbucket. De använder indexering för att det ska gå att söka igenom ditt projekt både i filer och i commits.

###Andra programmerare
Du kanske har löst något som andra programmerare har problem med eller skrivit ett populärt API. Då kan andra programmerare var intresserade av att använda din kod eller till och med bidra egna lösningar.

###Slutanvändare
Slutanvändare kanske besöker ditt repositorium för att få information om hur de ska använda ditt program eller så kanske din slutanvändare är andra programmerare som hämtar hem den senaste versionen via ditt repositorium.

###Du själv
Du är själv en en användare och är intresserad av ditt repositorium. Du kommer själv troligtvis vilja gå tillbaka till olika versioner av din kod någon gång under din applikations livstid.

[Tillbaka till innehållsförteckning](#innehallsforteckning)

##När ska jag versionshantera
En ledtråk finns i namnet. Versionshantering - Det säger oss att du ska hantera versioner. Versionshantering är inte ett sätt att skapa en "nu har jag slutat för dagen" backup av din kod. För sådant kan jag rekommendera en extern hårddisk, USB-minne, Network Attached Storage (NAS), Storage Area Network (SAN) eller en filserver av något annat slag. Så kort och gott ska du versionshantera när du har (av vad du vet) fungerande kod till 100%.

###Varför ska jag inte använda mitt repositorium som backup?
Varför ska jag inte använda mitt githubrepositorium (eller annan sorts repositorium) som en backup plats? För det får vi gå tillbaka och titta på vilka som kan vara intresserade av att använda ditt repositorium. Hur glada skulle dina kollegor bli om du gör en commit som inte innehåller körbar kod?  Om du själv har besökt ett repositorium och du laddar hem den senaste versionen av ett kodprojekt, det första som händer när du kör ditt projekt är att du får ett fel under kompilering. Felet är i en obskyr klass som du inte har använt men som finns i kärnfunktionaliteten av projektet. Denna fil är ungefär 2000 rader stor och det undantaget du har fått upp är beroende av något i denna fil men du vet inte riktigt var. Allt detta för att den som äger projektet sitter i australien, den programmeraren tänkte "äh, jag fixar dethär imorgon" och gjorde en backup-commit och gick hem. I commit meddelandet stod enbart information om vad som förändrats, men inget om att det fanns fel i koden som körs.

Eller du har precis gjort en backup-commit och du har tydligen märkt ut "I denna commit finns följande fel som måste rättas till". Sedan kommer en potentiell användare och tittar på vad ditt projekt går ut på, denna användare tycker att det verkar vara jättebra och är precis vad den söker... ...men så läser den "detta repositorium innehåller följande fel". Ja, det är ju bra att informationen finns där. Men troligtvis kommer användaren då välja ett annat projekt som gör snarlika saker just för att det fanns fel. Skulle du själv orka leta igenom mer än 5 commits för att hitta en commit som är 100% fungerande?

Det tidigare exemplen visserligen ett extremt exempel. Det är användare i det som kan manuellt ändra det som har blivit fel. Men det finns grupper som är intresserade av ditt repositorium som gör allt sådant automatiserat. Forkare är ett exempel, de kanske har med ett script som kontrollerar om ordet "backup" finns i din kommentar till din commit. Det kan även vara programmerare som automatiskt uppdaterar sig mot ditt repositorium och då kanske får hem felaktigt icke fungerande kod till sina projekt.

###Vem bryr sig?
Men är det mitt problem om andra inte kan använda mitt repositorium? Det är en fråga som är befogad att ställa. Kort sagt, ja. Du förlorar användare och du kan framstå som en sämre programmerare än vad du är. Det kanske är experimentell kod som gör att det inte fungerar. Du är medveten om att det kanske inte fungerar. Men kommer en potentiell arbetsgivare titta igenom och leta efter senaste fungerande commit om de tittar på det här repositoriumet. Användare som märker att din kod ofta inte fungerar kommer sluta använda ditt API och gå över till ett som alltid fungerar vid senaste version. Så i slutändan blir det defacto ditt problem då det är ditt varumärke som programmerare som tar skada av detta.

###Hur undviker jag detta?
Men jag vill ju experimentera och kunna versionshantera! - Ja, det vill vi alla. Det borde du få göra också. I många moderna versionshanteringssystem finns det en funktionalitet som kallas för branching. Det innebär att du skapar ett sidospår av din kod. Där kan du mycket väl experimentera och kanske till och med lägga ut versioner med avsnitt där du har kommenterat bort kod och lagt kommentaren "Andra programmerare, hjälp mig få detta att fungera. Det är en supersweet sätt men jag får det inte att fungera helt" eller liknande. Men du bör hålla ditt huvudrepositorium så rent som möjligt. Det kommer du tacka dig själv för och andra kommer att uppskatta det också. Det kommer i slutändan att leda till att om du gör en applikation, ett bibliotek eller ett API som andra faktiskt har nytta av att du får fler användare.

[Tillbaka till innehållsförteckning](#innehallsforteckning)

##Skrivet av
Ursprungligen skrivet av:

Emil Carlsson (info at gingerswede dot com) (2013-09-09)

Editerat av:


[Tillbaka till innehållsförteckning](#innehallsforteckning)
