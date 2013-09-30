#Strängberoede
Denna text ämnar att reda ut begreppet strängberoende något. Det innehåller vissa förklaringar till varför och även exempel på hur ett strängberoende uppstår och hur det går att arbeta bort detta strängberoende.

##Innehållsförteckning
* [Vad är ett strängberoende?](#vad-är-ett-strängberoende)
* [Varför vill vi undvika strängberoenden?](#varför-vill-vi-undvika-strängberoenden)
* [Hur undviker vi strängberoenden?](#hur-undviker-vi-strängberoenden)
* [Dåligt exempel](#dåligt-exempel)
* [Bra exempel](#bra-exempel)
* [Skrivet av](#skrivet-av)

## Vad är ett strängberoende?
Ett strängberoende är när du har en del av din applikation som bygger på att du upprepar ett värde som kan lagras i en variabel. Det kan tillexempel vara att du söker efter en post i $_GET globalen i php genom att skriva `$_GET["action"]`.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Varför vill vi undvika strängberoenden?
Detta är något som många frågar sig när de får höra av elaka människor som hävdar att deras kod har mycket strängberoenden. Inte allt för sällan så kommer kommentaren "men det fungerar ju! det är väl inte så viktigt?".

Det är ofta något som kan te sig oviktigt när kodbasen är tre till fyra filer, varje fil innehåller kanske 250 rader kod på sin höjd och strängberoendet uppenbarar sig bara fyra till fem gånger per fil (även om vi redan där har 12 till 20 strängberoenden!). Det är faktiskt 12 till 20 ställen som det kan råka bli fel i applikationen.

Vad händer om vi går tillbaka till `$_GET["action"]` exemplet under föregående rubrik och vi skriver `$_GET["Action"]` istället? Helt plötsligt har vi hämtat något helt annat än vi hade tänkt ifrån början. Ofta brukar det finnas postfält som heter saker som `userName`, `email` eller `password`. Det är inte allt för sällan som det kommer ett fel som beror på att i ett ställe i koden skrevs istället `$_POST['user_name']` istället för `$_POST['userName']`. Då är det bara en person som har varit med och skrivit koden. Hur många ställen kan det då inte bli fel om det är flera personer som skriver en applikation ihop?

Vi vill därför undvika strängberoenden för att det ökar risken för fel under run-time för en applikation. Fel som skapats för att programmeraren råkat skriva fel värde när värdet används för att utföra någon funktionalitet som är viktig för applikationen.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Hur undviker vi strängberoenden?
Hur kan vi då undvika detta otrevliga tillfälle där vårat fel egentligen bara bestod av att vi råkat skriva usreName istället för userName?

Grundtanken vi kan ha är att vi vill bara kunna skriva fel på ett ställe i hela applikationen. Det gör att vi kan lägga värdet i en variabel av något vis. Det betyder att vi får ett mer talande fel oftast. Det gör även att om vi stavar fel på ett ställe så kommer vi att ha samma felstavning i hela applikationen. Därför rekommenderas det att denna information läggs som en privat statisk variabel eller en konstant som är åtkomlig av alla klasser som kan tänkas använda den.

Huruvida du bör använda en konstant eller en statisk privat variabel kan du avgöra i om det kan tänkas behöva vara åtkomlig externt eller inte. Konstanter bör hållas publika medan statiska variabler kan vara privata. Det kan vara en tanke att inte vara lat och lägga alla variabler som skapas för att undvika strängberoenden som konstanter. Det har med att göra hur det publika interfacet för en klass bör se ut. För att inte göra detta till infomration om hur publika interface bör utformas så får du som läsare i detta läge acceptera att ett publikt interface bör vara så litet som möjligt. Även detta för att undvika fel. Därför bör enbart strängar som behövs utanför klassen läggas som konstanter. För att leta efter användarinput krävs ytterst sällan att det är publikt. Så normalläget för detta är att de bör generellt hållas som privata statiska medlemsvariabler.

Varför de ska vara statiska har helt och hållet att göra med att de inte ska kunna ändras i run-time. Om de kan ändras i runtime så har vi egentligen inte löst problemet att bli av med den mänskliga faktorn då det blir lika lätt att råka skriva över värdet som att hämta det.

[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Dåligt exempel
Nedan följer ett exempel med strängberoenden. Detta är ett exempel på dålig kod och bör därför undvikas att efterlikna. I detta korta exempel så finns elva strängberoenden. Kan du hitta alla?

	<?php
	
	namespace view;
	
	require_once("product.php");
	
	class ProductView {
		public function getAmount() {
			if (isset($_POST['amount'])) {
				return $_POST['amount'];
			} else {
				return null;
			}
		}
		
		public function getProductId() {
			if (isset($_POST['productId'])) {
				return $_POST['productId'];
			} else {
				return null;
			}
		}
		
		public function getAction() {
			if (isset($_GET['action'])) {
				return $_GET['action'];
			} else {
				return null;
			}
		}
		
		public function getProductField(\model\Product $product) {
			return "
				<form action='?action=addProduct' method='post'>
					<fieldset>
						<legend>Order $product->getName()</legend>
						<input type='hidden' name='productId' value='$product->getUnique()' />
						<p>
							Price: $product->getCostSEK()
						</p>
						<p>
							<label for='amount'>Amount</label>
							<input type='text' name='amount' value='1' id='amount' />
						</p>
						<p>
							<input type='submit' name='addProduct' value='Add Product' />
						</p>
					</fiedset>
				</form>
			";
		}
	}


[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Bra exempel
Detta är exakt samma kod som är i det dåliga exemplet. Men denna gång så är strängberoendena borttagna.

	<?php
	
	namespace view;
	
	require_once("product.php");
	
	class ProductView {
		
		private static $amount = 'amount';
		private static $productId = 'productId';
		private static $action = 'action';
		
		//Denna ligger som konstant för att den troligtvis behövs i en controller.
		const ACTION_ADD_PRODUCT = 'addProduct'; 
		
		public function getAmount() {
			if (isset($_POST[self::$amount])) {
				return $_POST[self::$amount];
			} else {
				return null;
			}
		}
		
		public function getProductId() {
			if (isset($_POST[self::$productId])) {
				return $_POST[self::$productId];
			} else {
				return null;
			}
		}
		
		public function getAction() {
			if (isset($_GET[self::ACTION])) {
				return $_GET[self::ACTION];
			} else {
				return null;
			}
		}
		
		public function getProductField(\model\Product $product) {
			return "
				<form action='?".self::ACTION."=".self::ACTION_ADD_PRODUCT."' method='post'>
					<fieldset>
						<legend>Order $product->getName()</legend>
						<input type='hidden' name='".self::$productId."' value='$product->getUnique()' />
						<p>
							Price: $product->getCostSEK()
						</p>
						<p>
							<label for='".self::$amount."'>Amount</label>
							<input type='text' name='".self::$amount."' value='1' id='".self::$amount."' />
						</p>
						<p>
							<input type='submit' name='".self::$productId."' value='Add Product' />
						</p>
					</fiedset>
				</form>
			";
		}
	}


[Tillbaka till innehållsförteckning](#innehållsförteckning)

##Skrivet av
Ursprungligen skrivet av:

Emil Carlsson (info at gingerswede dot com) (2013-09-30)

Editerat av:

[Tillbaka till innehållsförteckning](#innehållsförteckning)