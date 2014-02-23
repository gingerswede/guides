#Globala variabler
##Innehållsförteckning
* [Superglobaler](#superglobaler)
	* [$_POST](#post)
	* [$_GET](#get)
	* [$_FILES](#files)
	* [$_COOKIE](#cookie)
	* [$_SESSION](#session)
	* [$_SERVER](#server)
	* [$_REQUEST](#request)
	* [$_ENV](#env)

#Superglobaler
I PHP så finns det en uppsättning av variabler som alltid finns tillgängliga för dig oberoende av scope som du arbetar i. Dessa variabler kallas för globaler alternativt superglobaler. De innehåller information som antingen skickas över http-headers eller som sparas temporärt på serversidan. Det finns även information om servermiljön i några av dessa.

De flesta superglobaler är associativa arrayer. Det innebär att de har en nyckel av typen sträng. Olika superglobaler har olika uppgifter och är till för att nyttjas på olika vis. Några av dem består av en uppsättning fördefinerade nycklar medan andra skapas dynamiskt beroende på situationen.

##POST
Superglobalen $_POST innehåller information som skickas igenom ett [htmlfomulär som använder metoden post](#post-form). Detta är ett av de mer vanliga sätten att skicka information mellan användaren och php-applikaitonen.

I [exemplet](#post-form) har inputfältet fått __`inputField`__ som namnattribut. Det gör att vi kan få tillgång till det via superglobalen __`$_POST`__ på ett enkelt vis. Denna superglobal är en associativ array där nycklarna är just namnattributen (i detta fall __`name="inputField"`__) som finns i fomuläret som har skickats. Så för att komma åt det inputfältet så skriver vi helt enkelt __`$_POST['inputField']`__.

__O.B.S.__ Ingen av datan som skickas i denna superglobal är validerad eller kontrollerad. Glöm inte att detta är en kontroll du som programmerare måste utföra!

##GET
Get fungerar i stort sätt på samma vis som post. Det är skillnad i hur dessa transporteras via http-headers men i utförande i PHP för dig som programmerare är funktionaliteten identisk. Det är en associativ array som får sina nyckelvärden ifrån nameattributen. Precis som $_POST gör.

Både $_POST och $_GET används i samband med formulär.

__O.B.S.__ Ingen av datan som skickas i denna superglobal är validerad eller kontrollerad. Glöm inte att detta är en kontroll du som programmerare måste utföra!

##Files
Denna superglobal är lite speciell. Den används för att transportera filer ifrån klienten till din applikation via ett formulär som använder sig av metoden post. Det är en superglobal som innehåller flera fördefinerade arraynycklar där information om filen som skall laddas upp kan hämtas. För att använda post som ett sätt att ladda upp filer så krävs det att du använder ett formulär som ser något annorlunda ut än vanliga formulär. Du måste använda dig av encruptattributet _multipart/form-data_, se [exempelformuläret](#files-form).

##Exempelkod
###Post form
Ett exempel på ett htmlformulär där post används som metod.

	<form action="" method="post">
		<fieldset>
			<input type="text" name="inputField" placeholder="An input field" class="inputField" />
			<input type="submit" name="send" value="Send!" />
		</fieldset>
	</form>

Hur åtkomst till inputfältet sker.

	<?php
		$textField = $_POST['inputField']; //$textField innehåller nu värdet ifrån textfältet.

###Get form
Ett exempel på ett htmlformulär där get används som metod.

	<form action="" method="get">
		<fieldset>
			<input type="text" name="inputField" placeholder="An input field" class="inputField" />
			<input type="submit" name="send" value="Send!" />
		</fieldset>
	</form>

Hur åtkomst till inputfältet sker.

	<?php
		$textField = $_GET['inputField']; //$textField innehåller nu värdet ifrån textfältet.

###Files form
	<form action="" method="post" encode="multipart/form-data">
		<input type="hidden" name="MAX_FILE_SIZE" value="30000">
		Välj fil: <input name="fileToUpload" type="file" />
		<input type="submit" value="Ladda upp fil" />
	</form>