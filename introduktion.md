#Introduktion till PHP på Svenska
Denna bok uppkom då det saknades kurslitteratur på rätt nivå för kursen "Webbutveckling med PHP" som ges vid Linnéuniversitetet. De böcker som finns på marknaden har antingen legat på för låg nivå där läsaren inte förväntats kunna programmera sedan tidigare. Eller så har de legat på en för hög nivå där läsaren förväntas att redan kunna PHP flytande. Då studenterna vid den kursen redan kan programmera andra objektorienterade programmeringsspråk, men inte garanterat är bekanta med PHP så skrev som komplement små texter för att förklara vissa delar. Dessa kompletterades sedan och sammanfogades för att i slutändan bli denna bok.

De förkunskaper som du förväntas att ha för att förstå denna bok är grundläggande kunskap om objektorienterad programmering. Du förväntas även kunna html och css. Denna bok kommer inte att gå in på sådant som vad en _if-sats_ är eller vad ett objekt är. Det som vi kommer att ta upp i denna boken är hur php fungerar objektorienterat, och då tillsammans med mjukvaruarkitekturen Model-View-Controller (__MVC__).

Målet med denna bok är att ge studenter tillgång till information som krävs för att lära sig använda PHP för att skapa webbapplikationer.

##Bokens uppbyggnad
Boken bygger på att gradvis introducera nya utmaningar för dig i PHP. I bokens första del kommer fokus att ligga på PHP, hur vi kan använda PHP för att skapa enklare applikationer och kortare förklaringar av grunderna i PHP (men inte i programmering).

Bokens andra del fokuserar mera på mjukvaruarkitekturer, varför vi bör göra på ett visst vis och vad fördelarna (och nackdelarna) med att arbeta på det viset är. Vi komemr även att förklara varför vissa val har gjorts och vilka problem som kan ha uppstått när vi gjorde detta val.

Bokens tredje del kan ses som ett uppslagsverk där vissa kringfunktioner och generella tankar om dem ifrån författarna kan hittas. Det är ingen del som du behöver läsa för att lära dig programmera i PHP, men det rekommenderas starkt att du läser denna del för att få en djupare förståelse för både programmering i PHP och programmering generellt.

Om du känner att någon del av boken är otydlig gällande PHP funktionaliteter eller liknande så rekommenderas den officiella dokumentationen av PHP som finns på [http://www.php.net](http://www.php.net). Där finns det både exempel och förklaringar av olika delar av PHP. Den sidan är ett måste att lära sig att hitta på och det rekommenderas starkt att använda den sidan för förklaringar av grundfunktionaliteter i PHP.

För att få ut så mycket som möjligt av boken så rekommenderas du att följa exemplen och även lösa de eventuella uppgifter som finns i boken. Lösningsförslag till uppgifterna går att hitta på bokens hemsida.

##Bokens exempel
Alla exempel i boken är skrivna av författarna. De går att hitta i sin helhet i bokens repositorium med kommentarer och dylikt. Exempel kommer att ligga i en katalogstruktur som består av kapitelnummer, sedan exempel, efter det följer exempelnummer (ex. ..._/1/exempel/4/_). Samtliga exempel finns även på bokens hemsida.

Vissa exempel kommer att bestå av flera filer. Ha därför i åtanke att alla filer behövs om du väljer att ladda ner ett exempel för att testköra det lokalt.

##Vad du behöver för att följa boken
Vad behöver då du för att kunna följa exempel ur denna bok och kunna skapa egna PHP-skript för att pröva dig fram? Du kommer att behöva ha detta när du börjar läsa kapitel ett.

###Utvecklingsmiljö
Du kommer att behöva en utvecklingsmiljö att skriva din kod i. Det går utmärkt att använda en vanlig texteditor som Notepad (Windows) eller Nano (*nix/Unix). Men det rekommenderas att använda en lite tyngre integrerad utvecklingsmiljö (__IDE__) så som Aptana eller Sublime. Vilken utvecklingsmiljö du väljer är upp till dig och beror på vilken av alla de som finns där ute som passar dig bäst. Eventuella bilder i boken kommer ifrån Aptana, Sublime och Notepad++. Det kommer inte garanterat att redogöras vilken av dessa som använts.

En integrerad utvecklingsmiljö finns det oftast en så kallad intellisense. Där programmet kan hjälpa dig med vanligt förekommande funktionsanrop och även egenskrivna klasser, funktionsanrop och liknande. Detta kan vara väldigt användbart då det med tiden som projekt växer blir väldigt många funktioner som du själv har skrivit.

###Utvecklingsserver
Du kommer att behöva någon form av servermiljö som har PHP installerat. Det finns väldigt många alternativ för olika operativsystem. Några som kan nämnas är easy PHP (http://www.easyphp.org/), XAMPP (http://www.apachefriends.org/index.html). Dessa två innehåller Apache, PHP och MySQL och är förhållandevis enkla att installera och administrera. Du kan givetvis även installera en egen server med hjälp av Apache (http://www.apache.org/), PHP (http://www.php.net/downloads.php), och valfri databas. Boken kommer att utgå ifrån att du använder dig av relationsdatabasen MySQL (http://www.mysql.com/). 

##Vad som kan underlätta
###Publik driftmiljö
Det kan underlätta för din utveckling som PHP-programmerare att ha en publik driftmiljö. Med publik driftmiljö menas en server där du inte själv kontrollerar installationen. Det finns många gratis , eller väldigt billiga, webbhotell som erbjuder både PHP och MySQL. Anledningen till att ha en servermiljö som du inte själv kan kontrollera är att du då kommer stöta på problem där en lösning kanske inte garanterat fungerar på grund av begränsningar i serverinställningarna. Det kan tillexempel vara att någon PHP-funktionalitet är avstängd p.g.a. säkerhetsskäl eller liknande. Det gör att du som programmerare måste hitta en lösning som fungerar även under de omständigheterna som kan uppkomma när du inte själv får bestämma allt.

###Versionshantering
Ett versionshanteringssystem rekommenderas starkt. Vilket av dem du väljer är helt upp till dig. Det finns många olika typer av versionshanteringssystem. Några värda att nämna är _git_, _Subversion_, och _CVS_. Det finns två olika typer av versionshantering. Centraliserade och decentraliserade versionshanteringssystem. Mer om detta finns att läsa i kapitlet om versionshantering. Författarna av denna bok har primärt använt sig av Git.

##Notera
Även om det rekommenderas att du använder en publik driftmiljö och ett versionshanteringssystem och att det krävs att du har en utvecklingsmiljö och en utvecklingsserver så kommer denna bok inte att handla om hur du använder dessa. Bokens primära syfte är PHP enligt mjukvaruarkitekturen MVC i kombination med en relationsdatabas.
