---
title: Planera för automatisering av uppgifter
titleSuffix: Configuration Manager
description: Planera innan du skapar aktivitetssekvenser för att automatisera aktiviteter med Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723567"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Planera för automatisering av uppgifter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan skapa aktivitetssekvenser för att automatisera aktiviteter i din Configuration Managers miljö. Dessa uppgifter sträcker sig från att fånga ett operativ system på en referens dator för att distribuera operativ systemet till en eller flera mål datorer. Åtgärderna i en aktivitetssekvens definieras i de olika stegen i sekvensen. När aktivitetssekvensen körs körs åtgärderna för varje steg på kommando rads nivå i det lokala system sammanhanget. Det här beteendet innebär att aktivitetssekvensen körs helt automatiserad utan att användaren behöver göra något.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a>Steg och åtgärder för aktivitetssekvenser  

Steg är de grundläggande komponenterna i en aktivitetssekvens. De kan innehålla kommandon som:

- Konfigurera och avbilda operativ systemet på en referens dator
- Installera Windows, maskin varu driv rutiner, Configuration Manager klienten och program vara på mål datorn

Åtgärderna i steget definierar kommandon för ett steg i en aktivitetssekvens. Det finns två typer av åtgärder:  

- En åtgärd som du definierar med en kommando rads sträng kallas en *anpassad åtgärd*  
- En åtgärd som är fördefinierad av Configuration Manager kallas för en *inbyggd åtgärd*.  

En aktivitetssekvens kan göra en kombination av anpassade och inbyggda åtgärder.  

Steg i aktivitetssekvensen kan också innehålla villkor som styr hur steget fungerar. Dessa beteenden omfattar att stoppa aktivitetssekvensen eller att fortsätta med aktivitetssekvensen om ett fel inträffar. En typ av villkor är en aktivitetssekvens-variabel. Använd exempelvis variabeln **SMSTSLastActionRetCode** för att testa villkoret för föregående steg. Lägg till villkor i ett enskilt steg eller en grupp med steg.  

Aktivitetssekvensen bearbetar steg sekventiellt. Den här sekvensen omfattar åtgärdens steg och eventuella villkor för steget. När Configuration Manager börjar bearbeta ett steg i en aktivitetssekvens startar inte nästa steg förrän den föregående åtgärden har slutförts.

En aktivitetssekvens anses vara slutförd när:

- Alla steg har slutförts  
- Ett misslyckat steg innebär att Configuration Manager stoppa aktivitetssekvensen innan alla steg har slutförts.  

Om steget i en aktivitetssekvens till exempel inte kan hitta en refererad avbildning eller ett paket på en distributions plats, innehåller aktivitetssekvensen en bruten referens. Configuration Manager stoppar körningen av aktivitetssekvensen vid den punkten, om inte det misslyckade steget har ett villkor för att fortsätta när ett fel uppstår.  

> [!IMPORTANT]  
> Som standard kan en aktivitetssekvens inte fortsätta om ett steg eller en åtgärd misslyckas. Om du vill att aktivitetssekvensen ska fortsätta även om ett steg Miss lyckas, redigerar du aktivitetssekvensen, växlar till fliken **alternativ** och väljer sedan **Fortsätt vid fel**.  

Mer information om de steg som kan läggas till i en aktivitetssekvens finns i avsnittet om [aktivitetssekvenser](../understand/task-sequence-steps.md).  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Aktivitetssekvensgrupper  

Du kan gruppera flera steg i en aktivitetssekvens. En aktivitetssekvens består av ett namn, en valfri beskrivning och eventuella valfria villkor. Aktivitetssekvensen utvärderar grupp villkoren som en enhet innan den fortsätter med nästa steg. Kapsla grupper inom varandra eller ta med en blandning av steg och under grupper. Grupper är användbara om du vill kombinera flera steg som har samma villkor.  

Tilldela ett namn till aktivitetssekvenser. Det behöver inte vara unikt. Du kan även ange en valfri beskrivning av aktivitetssekvensgruppen.  

> [!IMPORTANT]  
> Om ett steg eller en inbäddad grupp i gruppen misslyckas, kan aktivitetssekvensen som standard inte fortsätta. Om du vill att aktivitetssekvensen ska fortsätta när ett steg eller en inbäddad grupp Miss lyckas, anger du alternativet **Fortsätt vid fel** i steget eller gruppen.  

I följande tabell visas hur alternativet **Fortsätt vid fel** fungerar när du grupperar steg.  

I det här exemplet finns det två grupper med aktivitetssekvenser som innehåller tre steg i aktivitetssekvensen.  

|Aktivitetssekvensgrupp eller -steg|Inställningen Fortsätt vid fel|  
|---------------------------------|-------------------------------|  
|**Aktivitetssekvens grupp 1**|**Fortsätt vid fel** valt.|  
|Aktivitetssekvens steg 1|**Fortsätt vid fel** valt.|  
|Aktivitetssekvens steg 2|Inte inställt.|  
|Aktivitetssekvens steg 3|Inte inställt.|  
|**Aktivitetssekvens grupp 2**|Inte inställt.|  
|Aktivitetssekvens steg 4|Inte inställt.|  
|Aktivitetssekvens steg 5|Inte inställt.|  
|Aktivitetssekvens steg 6|Inte inställt.|  

- Om steg 1 för aktivitetssekvensen Miss lyckas fortsätter aktivitetssekvensen med aktivitetssekvens steg 2.  

- Om steg 2 för en aktivitetssekvens Miss lyckas, körs inte aktivitetssekvensen steg 3. Eftersom grupp 1 för aktivitetssekvens har kon figurer ATS för att **fortsätta vid fel**, fortsätter aktivitetssekvensen till aktivitetssekvens grupp 2. Den kör aktivitetssekvensen steg 4 härnäst.  

- Om steg 4 i aktivitetssekvensen Miss lyckas körs inga fler steg. Aktivitetssekvensen Miss lyckas eftersom inställningen **Fortsätt vid fel** inte är konfigurerad för aktivitetssekvensen 2.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Lägg till underordnade aktivitetssekvenser i en aktivitetssekvens

<!--1261338-->

Lägg till ett nytt steg i aktivitetssekvensen som kör en annan aktivitetssekvens. Det här steget skapar en överordnad-underordnad relation mellan aktivitetssekvenser. Med det här steget kan du skapa fler modulära aktivitetssekvenser som du kan återanvända.  

Mer information finns i [köra aktivitetssekvens](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a>Variabler för aktivitetssekvens  

Variabler för aktivitetssekvens är en uppsättning namn-och värdepar. De tillhandahåller konfigurations-och distributions inställningar för datorer, operativ system och konfigurations uppgifter för användar tillstånd på en Configuration Manager-klient. Aktivitetssekvensvariablerna innehåller en funktion för att konfigurera och anpassa stegen i en aktivitetssekvens.  

När du kör en aktivitetssekvens lagras många av inställningarna för aktivitetssekvens som miljövariabler. Du kan komma åt eller ändra värdena för inbyggda variabler för aktivitetssekvens. Du kan också skapa nya variabler för aktivitetssekvens för att anpassa hur en aktivitetssekvens körs på mål datorn.  

Använd variabler för aktivitetssekvens för att utföra följande åtgärder:  

- Konfigurera inställningar för en aktivitetssekvens  

- Ange kommando rads argument för ett steg i en aktivitetssekvens  

- Utvärdera ett villkor som avgör om ett steg eller en grupp körs i en aktivitetssekvens  

- Ange värden för anpassade skript som används i en aktivitetssekvens  

Du kan till exempel ha en aktivitetssekvens som innehåller steget **Anslut till domän eller arbets grupp** . Distribuera aktivitetssekvensen till olika samlingar, där medlemskapet i samlingen bestäms av domän medlemskap. Ange en aktivitetssekvens per samling för varje samlings domän namn. Använd sedan den aktivitetssekvensen för att ange rätt domän namn i aktivitetssekvensen.  

Mer information finns i [använda variabler för aktivitetssekvens](../understand/using-task-sequence-variables.md).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a>Skapa en aktivitetssekvens  

Aktivitetssekvenser skapas med hjälp av guiden Skapa aktivitetssekvens. Guiden kan skapa inbyggda aktivitetssekvenser som utför vissa aktiviteter eller anpassade aktivitetssekvenser som kan utföra många olika uppgifter. Med guiden kan du skapa följande typer av aktivitetssekvenser:

- Installera en befintlig operativ system avbildning på en måldator  

- Bygga och avbilda en operativ system avbildning av en referens dator  

- Uppgradera till Windows 10 från ett uppgraderings paket för operativ system på mål datorn

- Skapa en anpassad aktivitetssekvens som utför en anpassad aktivitet eller specialiserad OS-distribution  

Mer information finns i [skapa aktivitetssekvenser](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Redigera en aktivitetssekvens  

Redigera aktivitetssekvensen med hjälp av **Redigeraren för aktivitetssekvens**. Redigeraren kan göra följande ändringar i aktivitetssekvensen:  

- Lägga till eller ta bort steg i aktivitetssekvensen  

- Ändra ordningen på stegen i aktivitetssekvensen  

- Lägg till eller ta bort grupper av steg  

- Ange om aktivitetssekvensen ska fortsätta när ett fel inträffar  

- Lägg till villkor i stegen och grupperna i en aktivitetssekvens  

> [!IMPORTANT]  
> Om aktivitetssekvensen har associerade referenser till ett objekt som ett resultat av redigeringen, kräver redigeraren att du korrigerar referensen innan den kan stängas. Möjliga åtgärder är:  
>
> - Korrigera referensen
> - Ta bort det refererade objektet från aktivitetssekvensen  
> - Inaktivera tillfälligt det misslyckade steget i aktivitetssekvensen tills den brutna referensen har åtgärd ATS eller tagits bort  

Mer information om hur du redigerar aktivitetssekvenser finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a>Distribuera en aktivitetssekvens  

Distribuera en aktivitetssekvens till mål datorer som finns i en Configuration Manager samling. Använd den inbyggda samlingen **alla okända datorer** för att distribuera operativ system till okända datorer. Du kan inte distribuera en aktivitetssekvens till användar samlingar.  

> [!IMPORTANT]  
> Distribuera inte aktivitetssekvenser som installerar operativ system på olämpliga samlingar. Se till att den samling som du distribuerar aktivitetssekvensen till bara innehåller de datorer där du vill installera operativ systemet. Du kan förhindra oönskade OS-distributioner genom att konfigurera inställningar för distributioner med hög risk. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Varje måldator som tar emot aktivitetssekvensen kör aktivitetssekvensen enligt de inställningar som anges i distributionen. Själva aktivitetssekvenserna innehåller inga tillhör ande filer eller program. Alla filer som en aktivitetssekvens refererar till måste redan finnas på mål datorn eller lagras på en distributions plats som klienterna har åtkomst till.

> [!NOTE]  
> Aktivitetssekvensen installerar paket som refereras av program, även om programmet eller paketet redan är installerat på mål datorn.
>
> Om aktivitetssekvensen installerar ett program installeras programmet endast om krav reglerna för programmet är uppfyllda och programmet inte redan är installerat, baserat på den identifierings metod som har angetts för programmet.  

Configuration Manager-klienten kör en aktivitetssekvensdistribution när klient principen laddas ned. Om du vill utlösa den här åtgärden i stället för att vänta till nästa avsöknings cykel, se [Starta princip hämtning för en Configuration Manager-klient](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

När du distribuerar aktivitetssekvenser till Windows Embedded-enheter som är aktiverade med ett Skriv filter kan du ange om Skriv filtret ska inaktive ras på enheten under distributionen och sedan starta om enheten efter distributionen. Om Skriv filtret inte är inaktiverat distribueras aktivitetssekvensen till ett tillfälligt överlägg och är inte tillgänglig när enheten startas om.  

> [!NOTE]  
> När du distribuerar en aktivitetssekvens till en Windows Embedded-enhet måste du kontrol lera att enheten är medlem i en samling som har en konfigurerad underhålls period. På så sätt kan du hantera när Skriv filtret ska inaktive ras och aktive ras och när enheten startas om.  
>
> Om klienter laddar ned aktivitetssekvenser utanför underhålls perioden laddas aktivitetssekvensen ned två gånger. I det här scenariot laddar klienten ned aktivitetssekvensen, inaktiverar Skriv filtret, startar om datorn och hämtar sedan aktivitetssekvensen igen. Detta beror på att aktivitetssekvensen ursprungligen hämtades till det tillfälliga överlägget, vilket rensas när enheten startas om.  

Mer information om hur du distribuerar aktivitetssekvenser finns i [distribuera en aktivitetssekvens](../deploy-use/deploy-a-task-sequence.md).  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a>Exportera och importera

Configuration Manager låter dig exportera och importera aktivitetssekvenser. När du exporterar en aktivitetssekvens kan du ta med de objekt som aktivitetssekvensen refererar till.

Mer information finns i [Exportera och importera aktivitetssekvenser](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Köra en aktivitetssekvens  

Aktivitetssekvenser körs alltid med det lokala system kontot. När aktivitetssekvensen körs kontrollerar Configuration Manager klienten först om det finns några refererade paket innan den startar stegen i aktivitetssekvensen. Om det inte går att verifiera eller hämta ett refererat paket, returnerar aktivitetssekvensen ett fel för det associerade steget i aktivitetssekvensen.  

> [!Note]  
> I steget **Kör kommando rad** i aktivitetssekvensen kan du köra ett kommando som ett annat konto.  

Om du konfigurerar en aktivitetssekvensdistribution för hämtning och körning laddar Configuration Manager-klienten ned allt beroende innehåll till dess cacheminne. Om klientens cachestorlek är för liten eller om det inte går att hitta innehållet går det inte att hitta aktivitetssekvensen. Klienten genererar ett status meddelande.

Du kan också ange att klienten bara ska ladda ned innehållet när det behövs. För att utföra den här åtgärden väljer du **Hämta innehåll lokalt vid behov genom att köra aktivitetssekvensen** i aktivitetssekvensdistribution. Ett annat alternativ är att **köra program från distributions platsen**. Med det här alternativet installerar klienten filerna direkt från distributions platsen utan att först ladda ned dem till cachen.

När du konfigurerar aktivitetssekvensdistribution som **tillgänglig**, om klienten inte kan hitta beroende innehåll för aktivitetssekvensen, skickar den omedelbart ett fel. För en **nödvändig** distribution väntar Configuration Manager klienten i den här situationen. Det försöker att ladda ned innehållet fram till tids gränsen, om innehållet ännu inte har repliker ATS till en innehålls plats som klienten har åtkomst till.  

När en aktivitetssekvens slutförs eller Miss lyckas, Configuration Manager registrerar detta tillstånd i klient historiken.

När en aktivitetssekvens startar på en dator kan du inte avbryta eller stoppa den.  

> [!IMPORTANT]  
> Om ett steg i en aktivitetssekvens kräver att datorn startas om måste klienten kunna starta till en formaterad diskpartition. Annars Miss lyckas aktivitetssekvensen oavsett eventuell fel hantering som du anger i aktivitetssekvensen.  

När ett beroende objekt i en aktivitetssekvens uppdateras till en nyare version, uppdateras alla aktivitetssekvenser som refererar till paketet automatiskt. Den refererar till den senaste versionen oavsett hur många uppdateringar du har distribuerat.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a>Använd underhålls fönster

Du kan ange när aktivitetssekvensen kan köras genom att definiera en underhålls period för enhets samlingen. Du konfigurerar underhålls perioder med ett start datum, en start-och slut tid samt ett upprepnings mönster. När du ställer in schemat för underhålls fönstret kan du ange att underhålls perioden bara gäller för aktivitetssekvenser. Mer information finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

> [!IMPORTANT]  
> När du konfigurerar en underhållsperiod då en aktivitetssekvens ska köras och aktivitetssekvensen sedan startas, fortsätter aktivitetssekvensen att köras även om underhållsperioden avslutas.  

Om en enhet har fler än ett underhålls fönster kan klienten ignorera ett fönster för underhåll av **distributioner** . Från och med version 1810 använder du följande klient inställning för att styra detta beteende: **Aktivera installation av program uppdateringar i underhålls fönstret för alla distributioner när underhålls fönstret för program uppdatering är tillgängligt**. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a>Aktivitetssekvenser och kontot för nätverks åtkomst  

> [!Important]  
> Vissa distributions scenarier för operativ system kräver inte att nätverks åtkomst kontot används. Mer information finns i [Enhanced http](#enhanced-http).

Även om aktivitetssekvenser bara körs inom kontexten för det lokala system kontot, kan du behöva konfigurera [kontot för nätverks åtkomst](../../core/plan-design/hierarchy/accounts.md#network-access-account) i följande fall:  

- Om aktivitetssekvensen försöker komma åt Configuration Manager innehåll på distributions platser. Konfigurera kontot för nätverks åtkomst, annars kommer aktivitetssekvensen inte att fungera.

- När du använder en start avbildning för att starta en OS-distribution. I det här fallet använder Configuration Manager Windows PE-miljön, som inte är ett fullständigt operativ system. Windows PE-miljön använder ett automatiskt genererat, slumpmässigt namn som inte är medlem i någon domän. Om du inte konfigurerar kontot för nätverks åtkomst korrekt kan datorn inte komma åt det begärda innehållet för aktivitetssekvensen.  

> [!NOTE]  
> Kontot för nätverks åtkomst används aldrig som säkerhets kontext för att köra program, installera program, installera uppdateringar eller köra aktivitetssekvenser. Kontot för nätverks åtkomst används bara för att få åtkomst till de associerade resurserna i nätverket.  

Mer information om kontot för nätverks åtkomst finns i [konto för nätverks åtkomst](../../core/plan-design/hierarchy/accounts.md#network-access-account).  

### <a name="enhanced-http"></a>Förbättrad HTTP
<!--1358278-->

När du aktiverar **utökat http**kräver följande scenarier inte något konto för nätverks åtkomst för att ladda ned innehåll från en distributions plats:

- Aktivitetssekvenser som körs från startmedia eller PXE  
- Aktivitetssekvenser som körs från Software Center  

Dessa aktivitetssekvenser kan vara för distribution av operativ system eller anpassade. Det finns också stöd för arbets grupps datorer.

Mer information finns i [Enhanced http](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> Följande distributions scenarier för operativ system kräver fortfarande användning av ett konto för nätverks åtkomst:
>  
> - [Distributions alternativet](../deploy-use/deploy-a-task-sequence.md)för aktivitetssekvens har **åtkomst till innehåll direkt från en distributions plats vid behov genom att köra aktivitetssekvensen**
> - Steget [begär tillstånds lager](../understand/task-sequence-steps.md#BKMK_RequestStateStore) , **om dator kontot inte kan ansluta till ett tillstånds lager, använder du nätverks åtkomst kontot**
> - Vid anslutning med en obetrodd domän eller över Active Directory skogar
> - Med steget [Använd operativ Systems avbildning](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) kan du **komma åt innehåll direkt från distributions platsen**
> - Den [avancerade inställningen](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) för aktivitetssekvens för att **köra ett annat program först**
> - [Multicast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a>Skapa media

Du kan skriva aktivitetssekvenser och deras relaterade filer och beroenden till flera olika typer av medier. Configuration Manager stöder flyttbara medier som DVD eller USB-minne för avbildning, fristående och startbara media. För beredda medier använder en WIM-fil (Windows Image).  

När du skapar media anger du ett lösen ord för att kontrol lera åtkomsten. Sedan måste en person ange lösen ordet på mål datorn för att köra aktivitetssekvensen.  

När du kör en aktivitetssekvens från medier, känns inte den angivna processor arkitekturen på mediet igen. Om den angivna arkitekturen inte stämmer överens med mål datorn, försöker aktivitetssekvensen fortfarande att köras. Om medie arkitekturen inte matchar mål datorns arkitektur, Miss lyckas aktivitetssekvensen.  

Mer information finns i [skapa media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Mediatyper

Configuration Manager stöder följande typer av medier:  

#### <a name="capture-media"></a>Avbilda Media

Det här mediet samlar in en OS-avbildning som du konfigurerar och skapar utanför Configuration Manager-infrastrukturen. Avbildningsmedier kan innehålla anpassade program som kan köras före en aktivitetssekvens. Det anpassade programmet kan interagera med Skriv bordet, uppmana användaren att ange värden eller skapa variabler som ska användas av aktivitetssekvensen.  

Mer information finns i [skapa avbildnings medier](../deploy-use/create-capture-media.md).  

#### <a name="stand-alone-media"></a>Fristående media

Fristående medier innehåller aktivitetssekvensen och alla tillhörande objekt som krävs för att aktivitetssekvensen ska kunna köras. Aktivitetssekvenser för fristående media kan köras när Configuration Manager har begränsad eller ingen anslutning till nätverket. Kör fristående media på följande sätt:  

- Om mål datorn inte har startats används den Windows PE-avbildning som är kopplad till aktivitetssekvensen från det fristående mediet och aktivitetssekvensen börjar.  

- Starta det fristående mediet manuellt. Om en användare är inloggad på datorn kan de initiera aktivitetssekvensen från mediet.  

> [!IMPORTANT]  
> Stegen i en aktivitetssekvens för fristående media måste kunna köras utan att hämta några data från nätverket. Annars Miss lyckas det steg i aktivitetssekvensen som försöker hämta data. Ett steg i en aktivitetssekvens som kräver en distributions plats för att hämta ett paket Miss lyckas till exempel. Om det fristående mediet innehåller det nödvändiga paketet slutförs steget i aktivitetssekvensen.  

Mer information finns i [skapa fristående media](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Startbart medium

Startbara medier innehåller de filer som krävs för att starta en måldator så att den kan ansluta till Configuration Manager-infrastrukturen. Den avgör sedan vilka aktivitetssekvenser som ska köras baserat på dess samlings medlemskap. Det här mediet omfattar inte aktivitetssekvensen eller beroende objekt. I stället laddar klienten ned innehållet över nätverket. Den här metoden är användbar för nya datorer eller Bare Metal-distributioner, när inget operativ system finns på mål datorn.  

Mer information finns i [Skapa startbara media](../deploy-use/create-bootable-media.md).  

#### <a name="prestaged-media"></a>Förberett medium

För beredda medier distribuerar en operativ system avbildning till en måldator som inte är etablerad. Det för beredda mediet lagras som en WIM-fil (Windows Image). Den här filen kan installeras på en dator utan operativ system av tillverkaren eller vid ett företags mellanlagrings Center. En fördel med för beredda medier är att dessa platser inte kräver någon anslutning till din Configuration Managers miljö.  

Mer information finns i [skapa för beredda medier](../deploy-use/create-prestaged-media.md).  

## <a name="next-steps"></a>Nästa steg

- [Säkerhet och sekretess för distribution av operativsystem](security-and-privacy-for-operating-system-deployment.md)

- [Förbereda platssystemroller för distribution av operativsystem](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
