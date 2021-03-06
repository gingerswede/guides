#Kapitel 1
##Hello world!
Till en början med så kommer vi inte att skriva ett objektorienterat skript. Utan vi börjar med ett klassiskt exempel för att kontrollera att du har fått igång din utvecklingsmiljö och utvecklingsserver. Vi kommer sedan att gå vidare och göra detta till synes enkla exempel objektorienterat och mer dynamiskt än vad vi började.

Alla PHP-skript bör startas med en öppnande "PHP-tagg". Då PHP kan varvas med HTML så måste vi tala om för servern att det är PHP den skall tolka. Den öppnande PHP-taggen ser ut såhär: `<?php`. Den stängs med en avslutande tagg som ser ut såhär: `?>`. Om du blandar PHP med HTML så behöver du avsluta dina PHP-sektioner för att det inte ska bli några komplikationer. Men när du skriver rena PHP-objekt så utelämnas den avslutande taggen med fördel. Anledningen till detta är för att det då garanterat inte skrivs ut något, och HTTP-huvudet skickas, innan vi vill att det ska skrivas ut något. Många fall där det blir fel beror det på att ett mellanslag eller radavbrott har skickats av misstag när ett PHP-objekt har lästs in.

Vårat första exempel är att enbart skriva ut texten "Hello world" i din webbläsare. Det görs med fördel med hjäl av den inbyggda funktionen `echo`. Det finns flera olika funktioner för att skriva ut strängar i PHP, men vi rekommenderar `echo` på grund av att den är snabbare än de andra. Börja med att skapa ett nytt PHP-dokument som du kan döpa till "helloworld.php". Skriv sedan in följande text i det dokumentet:

	<?php
		echo "Hello world";
	?>

Om du nu dubbelklickar på det dokumentet så kommer det antingen att öppnas i din webbläsare eller i din IDE (integrated development environment) beroende på hur du valt att binda filändelsen php. Öppnas det i din webbläsare så kommer det inte att se så intressant ut:

![Hello world utan server](img/helloworldbrowsernoserveractive.png)

Det beror på att en webbläsare i sig inte kan tolka PHP. För att kunna se det som vi har tänkt oss (det vill säga, inte kunna se php-taggarna och php funktionerna som text) måste du titta på den via en webbserver. Om vi istället tittar på filen via en webbserver så kommer den att se ut mer som vi vill att den ska se ut:

![Hello world med server](img/helloworldbrowserserveractive.png)

Men, tittar vi närmare på källkoden så kan vi se att det inte är någon riktig HTML utan vi har bara fått ut texten "Hello world". Precis så som vi har det i våran php-fil. För att få en korrekt html-sida så måste vi utöka våran php-fil något. Vi börjar med att göra en sekventiell version av vårat php-skript så att vi får se en korrekt html-sida. Så vi lägger till lite html runt våran php-del som nedan:

	<!DOCTYPE html>
	<html>
		<head>
			<title>Hello world</title>
		</head>
		<body>
		<?php
			echo "Hello world";
		?>
		</body>
	</html>

Om vi nu tittar på dokumentet via en webbläsare så kommer det inte att synas några större förändringar. Men om vi tittar på källan för hemsidan så kommer det att se annorlunda ut.

![Hello world via källa](img/helloworldsource.png)

Som du ser så skrivs det ut korrekt html, och som body har vårat "Hello world" skrivits ut, utan att ha `<?php` och `?>` runt sig.

##Dags för objektorientering
Vi börjar nu med att göra vårat första PHP-objekt. Det kommer att vara ett enkelt exempel där vi inte använder någon nämnvärd mjukvaruarkitektur. Så vi kommer att nyttja sekventiell php för att skriva ut våran text, men objekt för att seperera funktionalitet ifrån HTML. Så vi utökar vårat php-skript genom att skapa ett php-objekt under våran html.

	<?php
		class HelloWorld {
			public function printMessage() {
				echo "Hello world";
			}
		}
	?>

I html notationen så instansierar vi nu istället ett objekt av typen "HelloWorld" och ropar på funktionen "printMessage" så i helhet kommer vårat exempel nu att se ut såhär:

	<!DOCTYPE html>
	<html>
		<head>
			<title>Hello world</title>
		</head>
		<body>
		<?php
			$helloWorld = new HelloWorld();
			$helloWorld->printMessage();
		?>
		</body>
	</html>

	<?php
		class HelloWorld {
			public function printMessage() {
				echo "Hello world";
			}
		}
	?>

Du noterar nog säkert att jag har använt en variabel. Variabler i php deklareras med hjälp av att inleda namnet med ett dollartecken (__$__). Du märkte även att jag inte angav någon typ på variabeln. Det beror på att PHP är ett så kallat otypat språk. Det innebär att du inte behöver ange vilken typ din variabel är, och den kan innehålla både textsträngar, heltal, objekt eller liknande. Du ser även att jag anropar funtionen `printMessage()` genom en pil (__->__) och inte en punkt (**.**) som i många andra språk.

##Upprätta en arkitektur
En del programmerare kan hävda att PHP är osäkert och bör inte användas på grund av detta. Detta är något av en myt. PHP är varken säkrare eller mindre säkert än övriga språk som finns där ute. En av de sakerna som kan vara anledningen till denna myt är att det är ett extremt populärt språk som är enkelt att lära sig. Det innebär att det finns väldigt många applikationer som använder sig av PHP. Vilket i sin tur leder till att det finns ett större utbud av applikationer där missöden kan ha inträffat. Det samma gäller att PHP är billigt att driftsätta och har funnits sedan 1995, vilket gör att i början av PHPs varande så var det inte det säkraste språket som fanns. Men språket i sig var egentligen inte problemet. PHP är precis som alla andra webbapplikationer inte säkrare än den servern som huserar det. PHP har däremot en nackdel som exempelvis ASP.NET eller JSP inte har. Det saknar ett ramverk och kompilering där det finns inbyggda felsäkringar eller valideringar. Därför är det av stor vikt när du programmerar PHP applikationer att du använder dig av en stabil mjukvaruarkitektur, och framförallt håller dig till denna arkitektur. I denna bok kommer vi att använda oss av mjukvaruarkitekturen Model View Controller (__MVC__).

För att börja upprätta denna arkitektur så skapar vi nu tre mappar i rooten på vårat nya projekt. Vi kallar dessa för "model", "view", och "controller". Vi skapar sedan i katalogen som heter "model" en fil som vi kallar för "helloworldmodel.php". I katalogen som heter view skapar vi en fil som vi namnger "helloworldview.php", och i katalogen "controller" skapar vi filen "helloworldcontroller.php". Vi tar även bort helloworld.php i rooten och skapar filen "index.php" istället.

![Katalogstruktur för projektet med de filerna som bör finnas.](img/helloworldmvcfolderstructure.png)

###Modellen
Vi börjar med att skapa modellen för våran applikation. Så då öppnar vi filen "helloworldmodel.php". Vi kommer i denna fil nu både ha en klass med ett namespace och den funktionalitet som avgör vad för något som applikationen ska kunna göra som vi inte vill att användaren direkt ska kunna påverka. Så i filen skriver vi denna källkod:

	<?php	
	namespace HelloWorld\Model;
	
	class HelloWorldModel {
		private $m_message = "Hello World";
			
		public function getMessage() {
			return $this->m_message;
		}
	}

Som du säkert noterat så är namespace definerat som `HelloWorld\Model` och inte `HelloWorld.Model` som i exempelvis Java eller C#. Det är något som helt enkelt är definerat som standard i PHP att använda backslash (__\\__) istället för punkt (**.**) i namespace definitionen. Något annat som du noterat är att det står m_ framför den privata medlemsvariabeln message. Detta är något som kallas för hungarian notation där m_ helt enkelt visar att detta är en medlemsvariabel. Det är något som kommer att användas konsekvent i denna bok för att visa saker så som medlemsvariabler. I övrigt borde inte denna klass innehålla något som är nytt för dig som läsare. Det är en klass med en privat medlemsvariabel som innehåller strängen "Hello World". Vi har sedan funktionen `getMessage` som returnerar det värde som finns i medlemsvariabeln `$m_message`.

Som du säkert noterat så har jag inte angivit något returvärde i metodsignaturen för funktionen `getMessage()`. Det behövs inte då PHP är otypat och det går därför att returnera ifrån funktioner när man själv känner att det är lämpligt. Detta är en av sakerna som gör det än viktigare att ha en strukturerad arkitektur för dina applikationer.

###Vyn
När vi har modellen klar så kommer vi nu att börja arbeta på våran vy. Det är där vi presenterar all information vi  vill att användaren ska se. Det är även här som all information som användaren kan påverka hanteras (exempelvis cookies och postparametrar). Men det är även här som all html och liknande saker byggs ihop för att visa användaren något. Det första vi kan fundera på nu är vad vi behöver i våran vy. En av de sakerna som vi har i modellen är ju funktionen `getMessage()`. Så vi kommer vilja hantera detta på något vis. Så i våran vy kommer vi alltså att behöva ha en variabel för detta. Vi kommer även att behöva skapa html på något vis som liknar det som vi hade i början av kapitlet. Ett exempel kan vara att göra koden som nedan:

	<?php
	namespace HelloWorld\View;
	
	class HelloWorldView {
		private $m_message;
		
		public function getMessage() {
			return $this->m_message;
		}
		
		public function setMessage(String $message) {
			$this->m_message = $message;
		}
		
		public function generateHTML() {
			$html = "
			<!DOCTYPE html>
			<html>
				<head>
					<title>Hello World example</title>
				</head>
				<body>
					<p>
						$this->m_message
					</p>
				</body>
			</html>
			";
			
			return $html;
		}
	}

Vi går igenom detta kodstycke uppifrån och ner. Först så talar jag om att det är PHP som vi skriver. Därefter berättar jag vilket namespace som vi ska jobba i just nu. Sedan talar jag om att vi ska jobba i en klass med namnet HelloWorldView. Efter det så skapar jag den privata medlemsvariabeln `$m_message`. Än så länge inget nytt i detta skript. Efter det så har jag skapat två funktioner som kallas för "getter" och "setter". Det är två funktioner vars enda syfte är att ge tillgång till den privata medlemsvariabeln `$m_message`. Anledningen till detta är för att vi här kan lägga till olika kontroller och formateringar som vi önskar. Vi har även kapslat in den privata medlemsvariabeln så att inga klasser utanför denna kan komma åt den och ändra i den hur som helst.

Därefter så har vi funktionen `generateHTML()`. I denna funktion så skapas en textsträng som är den HTML som behövs för att skapa ett html-dokument som valideras enligt standarden för html 5. I denna textsträng så finns även `$this->m_message` inskjutet direkt i strängen. Det är fullt tillåtet när du skapar strängar med hjälp av dubbelcitation (__"__), det fungerar dock inte när man skapar det med hjälp av enkelcitation (**'**). 

###Kontrollern
Nu när vi har en vy och en modell färdiga så behöver vi något som kan transportera ett meddelande ifrån modellen till vyn. Det gör vi med hjälp av en controller. En kontroller tillhör en av de typer av klass som får kommunicera med både vyer och modeller. De är lite som en spindel i nätet som bestämmer vad som ska hänta beroende på vad vi gör i våran applikation. Nu i början så kommer våran kontroller att vara relativt enkel då vi enbart har en sak som kan hända.

	<?php
	namespace HelloWorld\Controller;
	
	require_once '../model/helloworldmodel.php';
	require_once '../view/helloworldview.php';
	
	class HelloWorldController {
		private $m_model;
		private $m_view;
		
		public function __construct() {
			$this->m_view = new \HelloWorld\View\HelloWorldView();
			$this->m_model = new \HelloWorld\Model\HelloWorldModel();
			
			$this->m_view->setMessage($this->m_model->getMessage());
			
			echo $this->m_view->generateHTML();
		}	
	}

Om vi går igenom detta kodstycke rad för rad så ser vi några saker vi inte hade tidigare. Till en början med så har vi det bekanta php-taggen `<?php` och sedan `namespace HelloWorld\Controller` först. 

Därefter så har vi `require_once '../model/helloworldmodel.php';`. Vad det gör är att vi länkar in en fil. Sökvägen bör anges relativ till filen vi befinner oss i just nu och använd med fördel samma typ av slash (/) som används i Unix och på webben. Det går att på windowsservrar använda både framåtslash (\) och bakåtslash (/). Men för att undvika eventuella problem vid driftsättning bör enbart framåtslash (/) användas.

Vi går vidare så är det en deklarering av klassen `HelloWorldController` och därefter så följer deklarerandet av två privata medlemsvariabler. Men funktionen vi har här skiljer sig ifrån de vi tidigare har skrivit. Det är funktionen `__construct()`. `__construct()` är en vad man i php kallar för "magic method". Det vill säga en metod som php själv automatiskt kan kalla på utan att använda det namnet som metoden har. 

>Metod är ett annat namn för funktion. Vi kommer härefter att kalla allt för funktion och inte metod.

I det här fallet så använder vi konstruktorfunktionen `__construct()` för att kunna få funktionalitet att inträffa när vi skapar objektet. Precis som i C# eller Java så körs konstruktorn automatiskt när ett objekt instansieras.

I våran konstruktor så instansierar vi sedan våran vy och även våran kontroller till de två medlemsvariablerna med namnen `$m_view` och `$m_model`. Detta gör vi med hjälp av det reserverade ordet `new`. Sedan, precis som i Java och C#, så instansierar vi objekten med hjälp av objektnamnet och avslutande paranteser. Hade vi haft en konstruktor som tar en inparmeter i något av objekten så skickar vi med de parametrarna innanför paranteserna.

>Du märker säkert här att jag måste ha med hela namespace för de andra klasserna. Vi kommer i senare kapitel att gå in på hur vi kan göra för att inte behöva skriva ut hela namespacet.

Det vi gör sedan är att vi ropar på funktionen `setMessage()` som finns på vyobjectet vi har lagrat i `$m_view`. Denna funktion tar en inparameter som är meddelandet som skall visas i vyn så måste vi på något vis hämta detta ifrån modellen. Det gör vi genom att ropa på funktionen `getMessage()` på modellobjektet som vi har sparat i variablen `$m_model`.

Det vi vill göra sedan är att generera och skriva ut all HTML som vi genererar i vårat vyobjekt med hjälp av funktionen `generateHTML()`. Det görs enklast via den inbyggda funktionen `echo`.

##Använda funktioner och reserverade ord
I detta kapitel så har vi använd några inbyggda funktioner och annat. Som du säkert har märkt så fungerar PHP i mångt och mycket som många andra språk. Syntaxen är inspirerad främst ifrån språken Java, C, och C++. De funktioner vi framförallt använt har även vissa andra motsvarigheter eller andra liknande funktioner.

###Variabler
Vi har använt variabler i detta kapitel. För mer information om hur variabler fungerar i php besök [http://www.php.net/manual/en/language.variables.php](http://www.php.net/manual/en/language.variables.php).

###echo
Echo är ett kommando för att skriva ut saker på skärmen. I exempelvis Java så används istället `System.out.print` och i C++ används `cout`. I php finns flera olika vis att skriva ut saker på skärmen. Några av dessa är t.ex. `print` och `print_r`. Den sistnämnda skiljer sig något ifrån `print` och `echo`. Den största skillnaden mellan `print` och `echo` är att echo sägs vara snabbare. För mer information om echo besök [http://php.net/echo](http://php.net/echo).

###namespace
Namespace används för att deklarera vilket namespace (namnrymd) som våran kod ska tillhöra. Detta måste alltid följa direkt efter php-taggarna. För mer information om namespace besök [http://php.net/namespace](http://php.net/namespace).

###return
Return är en inbyggd funktionalitet i php för att ge ett returvärde. Det används inom funktioner för att kunna göra mer dynamiska funktionaliteter och arbeta med strukturerad programmering. En funktion måste inte innehålla ett returvärde. För mer information om return besök [http://php.net/return](http://php.net/return)

###function
Function är ett reserverat ord för att deklarera funktioner med. I php går det inte att specificera vilket returvärde en funktion har. Utan enbart om den är public, private, protected etc. För mer information om funktioner besök [http://www.php.net/manual/en/functions.user-defined.php](http://www.php.net/manual/en/functions.user-defined.php).

###Synlighet (Visibility)
Synlighet innebär vilka som kan se en funktion eller variabel. I php fungerar det på samma sätt som i t.ex. Java eller C#. För mer information om synlighet i php besök [http://www.php.net/manual/en/language.oop5.visibility.php](http://www.php.net/manual/en/language.oop5.visibility.php).

##Nästa kapitel
I nästa kapitel så kommer vi att arbeta om våran Hello World applikation. Vi kommer att titta på namngivning och även hur vi kan göra för att hämta information ifrån en användare.

##Övningsuppgifter
1. Installera en utvecklingsmiljö av modellen *AMP (där * står för __L__inux, **W**indows, eller __M__ac).
2. Skapa ett dokument som via php skriver ut texten "Hello World gång X" 100 gånger med hjälp av en loop. Istället för X så ska det vara vilken gång som loopen har körts. Texten skall skrivas ut på en egen rad och sidan som genereras skall validera i W3C html validator ([http://validator.w3.org/](http://validator.w3.org/)). (För svårare uppgift, gör lösningen objektorienterad enligt MVC mönstret vi har tagit upp i kapitlet.)
3. Skapa ett script som tar in en array och sedan vänder på denna array. Scriptet skall fungera på både numeriska och associativa arrayer. (Tips: den inbyggda funktionen `var_dump()` kan användas för att skriva ut innehållet i en array).

##Tankeuppgifter
1. Vad finns det för fördelar med att använda sig av MVC? Motivera gärna med några exempel.
2. Vad finns det för nackdelar med att använda sig av MVC? Motivera gärna med några exempel.
3. Varför är det viktigt i ett språk som PHP att använda sig av en mjukvaruarkitektur?
4. PHP är ett otypat språk. Vad finns det för fördelar och nackdelar med detta?