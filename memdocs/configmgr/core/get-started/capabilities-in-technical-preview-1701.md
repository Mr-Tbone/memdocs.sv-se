---
title: Funktioner i Technical Preview 1701
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 20c560925b2c1abec282b8c5f8dae3f6f42f4d64
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591213"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Funktioner i Technical Preview 1701 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*



Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1701. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Förbättringar av gränser grupper för program uppdaterings platser
Från och med den här för hands versionen använder du nu gränser grupper för att koppla klienter till program uppdaterings platser. Detta är en del av fortsatt arbete för att expandera ändringarna för gränser grupper för att hantera ytterligare plats system roller.  Ändringar för gränser grupper introducerades först i Technical Preview 1609 och Current Branch i version 1610.  

Med den här för hands versionen använder du den nya gränser grupp beteendet för att hantera vilka program uppdaterings platser en klient kan använda, på samma sätt som du hanterar vilken distributions plats en klient kan använda:  

- Du konfigurerar gränser grupper för att associera en eller flera servrar som är värdar för en program uppdaterings plats.
- Klienter som söker efter en ny program uppdaterings plats kommer att försöka använda en som är associerad med den aktuella gränser gruppen.
- När klienten inte når sin aktuella program uppdaterings plats och inte kan hitta någon från den aktuella gräns gruppen, använder klienten återställnings beteende för att expandera den tillgängliga poolen med program uppdaterings platser som kan användas.    

Mer information om avgränsnings grupper finns i [gränser grupper](../servers/deploy/configure/boundary-groups.md) i innehållet för Current Branch.

Men med den här för hands versionen implementeras bara gränser grupper för program uppdaterings platser delvis. Du kan lägga till program uppdaterings platser och konfigurera intilliggande gräns grupper som innehåller program uppdaterings platser, men återställnings tiden för program uppdaterings platser stöds inte ännu, och klienterna kommer att vänta två timmar innan återställningen påbörjas.

Här följer en beskrivning av beteendet för program uppdaterings platser med den här tekniska för hands versionen:  

- **Nya klienter använder gränser grupper för att välja program uppdaterings platser.** En klient som du installerar efter att du har installerat version 1701 väljer en program uppdaterings plats från de som är associerade med klientens gränser grupp.

  Detta ersätter föregående beteende där klienter väljer en program uppdaterings plats slumpmässigt från en lista över de som delar klienternas skog.   

- **Tidigare installerade klienter fortsätter att använda sin aktuella program uppdaterings plats tills de återgår till att hitta en ny.**
  Klienter som tidigare har installerats och som redan har en program uppdaterings plats fortsätter att använda den program uppdaterings platsen tills de återställs. Detta omfattar program uppdaterings platser som inte är associerade med klientens aktuella gränser grupp. De försöker inte omedelbart hitta och använda en program uppdaterings plats från den aktuella gränser gruppen.

  En klient som redan har en program uppdaterings plats börjar använda den här nya gräns grupps beteendet endast när klienten inte har nått sin aktuella program uppdaterings plats och påbörjar återställningen.
  Den här fördröjningen vid växling till det nya beteendet är avsiktlig. Detta beror på att en ändring av program uppdaterings platsen kan resultera i en stor användning av nätverks bandbredden när klienten synkroniserar data med den nya program uppdaterings platsen. Fördröjningen i över gången kan hjälpa till att undvika nätverket överbelastas nätverket om alla klienter växlar till nya program uppdaterings platser på samma gång.

- **Konfigurationer för återställnings tid:** Konfigurationer för när klienter startar reserv för att söka efter en ny program uppdaterings plats stöds inte i den här tekniska för hands versionen. Detta inkluderar konfigurationer för **återställnings tider (i minuter)** och **aldrig återställnings**tid, som du kan konfigurera för olika gränser för grupp relationer.

  Klienterna behåller i stället sitt nuvarande beteende där en klient försöker ansluta till den aktuella program uppdaterings platsen i två timmar innan den påbörjar återställningen för att hitta en ny program uppdaterings plats som den kan använda.

  När en klient använder reserv använder den gränser grupp konfigurationerna för återställning för att skapa en pool med tillgängliga program uppdaterings platser. Den här poolen innehåller alla program uppdaterings platser från klientens *aktuella gränser grupp*, *intilliggande gränser grupper*och klient *platsens standard gränser grupp*.

- **Konfigurera standard platsens gränser grupp:**  
  Överväg att lägga till en program uppdaterings plats till *platsen för standardsite-gränser-grupp &lt;>*. Detta säkerställer att klienter som inte är medlemmar i en annan avgränsnings grupp kan återgå till att hitta en program uppdaterings plats.


Om du vill hantera program uppdaterings platser för gränser grupper kan du använda [procedurerna i Current Branch dokumentationen](../servers/deploy/configure/boundary-group-procedures.md), men kom ihåg att återställnings tider som du kan konfigurera inte används för program uppdaterings platser än.


## <a name="hardware-inventory-collects-uefi-information"></a>Maskin varu inventering samlar in UEFI-information
En ny maskin varu inventerings klass (**SMS_Firmware**) och egenskap (**UEFI**) är tillgängliga för att hjälpa dig att avgöra om en dator startar i UEFI-läge. När en dator startas i UEFI-läge anges egenskapen **UEFI** till **True**. Detta är aktiverat i maskin varu inventeringen som standard. Mer information om maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="improvements-to-operating-system-deployment"></a>Förbättringar av operativ Systems distribution
Vi har gjort följande förbättringar av distributionen av operativ systemet, många av dem var resultatet av din röst feedback från användaren.
- [**Stöd för fler program för steget installera program**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): vi har ökat det maximala antalet program som du kan installera till 99 i steget **installera program** . Det tidigare maximala antalet var 9 program.
- [**Välj flera appar i steget installera app i**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step)aktivitetssekvensen: när du lägger till program i steget installera program i aktivitetssekvensen kan du nu välja flera program i fönstret **Välj program att installera** .
- [**Fristående media som upphör att gälla**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): när du skapar fristående medier finns det nya alternativ för att ange valfria start-och förfallo datum för mediet. De här inställningarna är inaktiverade som standard. Datumen jämförs med system klockan på datorn innan det fristående mediet körs. När system tiden infaller före start tiden eller senare än förfallo tiden startar inte det fristående mediet. Dessa alternativ är också tillgängliga med hjälp av PowerShell-cmdleten New-CMStandaloneMedia.
- [**Stöd för ytterligare innehåll i fristående media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): ytterligare innehåll stöds nu i fristående media. Du kan välja ytterligare paket, driv rutins paket och program som ska mellanlagras på mediet tillsammans med det andra innehåll som refereras i aktivitetssekvensen. Tidigare mellanlagrades endast innehåll som refereras i aktivitetssekvensen på fristående media.
- [**Konfigurerbar tids gräns för automatiskt tillämpade driv rutins steg**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout)i aktivitetssekvensen: nya variabler för aktivitetssekvens är nu tillgängliga för att konfigurera timeout-värdet på steget Använd automatisk driv rutins aktivitet vid http-katalog-begär Anden. Följande variabler och standardvärden (i sekunder) är tillgängliga:
   - SMSTSDriverRequestResolveTimeOut standard: 60
   - SMSTSDriverRequestConnectTimeOut standard: 60
   - SMSTSDriverRequestSendTimeOut standard: 60
   - SMSTSDriverRequestReceiveTimeOut standard: 480
- [**Paket-ID visas nu i**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste)aktivitetssekvenser: Alla aktivitetssekvenser som refererar till ett paket, driv rutins paket, en operativ system avbildning, en start avbildning eller ett uppgraderings paket för operativ system kommer nu att visa paket-ID: t för det refererade objektet. När ett steg i en aktivitetssekvens refererar till ett program visas objekt-ID.
- **Windows 10 ADK som spåras av build-version**: Windows 10 ADK spåras nu av build-versionen för att säkerställa en mer upplevelse vid anpassning av start avbildningar i Windows 10. Om webbplatsen till exempel använder Windows ADK för Windows 10, version 1607, kan endast start avbildningar med version 10.0.14393 anpassas i-konsolen. Mer information om hur du anpassar WinPE-versioner finns i [Anpassa Start avbildningar](../../osd/get-started/customize-boot-images.md).
- **Käll Sök vägen för standard start avbildningen kan inte längre ändras**: standard start avbildningarna hanteras av Configuration Manager och standard Sök vägen för start avbildningen kan inte längre ändras i Configuration Manager-konsolen eller med hjälp av Configuration Manager SDK. Du kan fortsätta att konfigurera en anpassad käll Sök väg för anpassade Start avbildningar.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Vara värd för program uppdateringar på molnbaserade distributions platser
Från och med den här för hands versionen kan du använda en molnbaserad distributions plats som värd för ett program uppdaterings paket. Men eftersom du kan konfigurera klienter för att hämta program uppdateringar direkt från Microsoft Update bör du ta hänsyn till ytterligare kostnader som distribuerar ett program uppdaterings paket till en molnbaserad distributions plats.

Information om hur du använder molnbaserade distributions platser finns i [använda en molnbaserad distributions plats](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) i innehållet för Current Branch av Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Verifiera data för hälsoattestering för enhet via hanterings platser

Från och med den här för hands versionen kan du konfigurera hanterings platser för att validera rapporterings data för hälsoattestering för moln tjänster eller lokala hälsoattesterings tjänster. På fliken nya **Avancerade alternativ** i dialog **rutan Egenskaper för hanterings plats komponent** kan du **lägga till**, **Redigera**eller **ta bort** den **lokala webb adressen för tjänsten hälsoattestering för enhet**. Du kan också ange **anpassade enhets inställningar** för klient agenten för att **använda tjänsten för lokal hälsoattestering**.  Om du anger **Ja** för den här inställningen aktive ras rapportering till den lokala hanterings platsen i stället för den molnbaserade tjänsten.

### <a name="try-it-out"></a>Prova

- **Aktivera lokal hälsoattestering för enhet på en hanterings plats**<br>  I Configuration Manager-konsolen navigerar du till hanterings platsen och öppnar **Egenskaper för hanterings plats komponent** och klickar sedan på fliken **Avancerade alternativ** . Klicka på **Lägg till** och ange den lokala URL: en (till exempel https://10.10.10.10) för **URL: er för tjänsten hälsoattestering för den lokala enheten**.
- **Aktivera rapportering av hälso deklaration för lokal hanterings plats för klient agenten**<br>I Configuration Manager-konsolen väljer du **Administration**  >  **klient inställningar** och dubbelklickar på eller skapar en ny **anpassad enhets inställning**. Välj **dator agent** och konfigurera **tjänsten för lokal hälsoattestering** till **Ja**. Om **Aktivera kommunikation med Hälsoattestering för enhet tjänsten** är inställt på **Ja** och **Använd lokal hälsoattestering** är inställt på **Nej**, använder hanterings platsen den molnbaserade tjänsten hälsoattestering för enhet.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Använd OMS-anslutningen för Microsoft Azure Government Cloud
Med den här tekniska för hands versionen kan du nu använda Microsoft Operations Management Suite (OMS) Connector för att ansluta till en OMS-arbetsyta som finns på Microsoft Azure Government molnet.  

Det gör du genom att ändra en konfigurations fil så att den pekar på det offentliga molnet och sedan installera OMS-anslutaren.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Konfigurera en OMS-anslutning till Microsoft Azure Government Cloud
1. På alla datorer där Configuration Manager-konsolen är installerad redigerar du följande konfigurations fil så att den pekar på det offentliga molnet: *** &lt; cm installations Sök väg # C0\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Redigeringar**

   Ändra värdet för inställnings namnet *FairFaxArmResourceID* till "<https://management.usgovcloudapi.net/">

   - **Original:** &lt; inställnings namn = "FairFaxArmResourceId" serializeAs = "String" >   
     &lt;värde>&lt; /value>   
     &lt;/Setting>

   - **Ändra**     
     &lt;inställnings namn = "FairFaxArmResourceId" serializeAs = "sträng" > &lt; värde &gt; https://management.usgovcloudapi.net/&lt ;/Value&gt;  
     &lt;/Setting>

   Ändra värdet för inställnings namnet *FairFaxAuthorityResource* till " <https://login.microsoftonline.com/> "

   - **Original:** &lt; inställnings namn = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;värde>&lt; /value>

   - **Redige rad:** &lt; inställnings namn = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;värde &gt; [https://login.microsoftonline.com](https://login.microsoftonline.com) &lt; /Value&gt;

2. När du har sparat filen med de två ändringarna startar du om Configuration Manager-konsolen på samma dator och använder sedan konsolen för att installera OMS-anslutaren. Om du vill installera anslutningen använder du informationen i [synkronisera data från Configuration Manager till Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)och väljer sedan **Operations Management Suite-arbetsytan** som finns i Microsoft Azure Government molnet.

3. När OMS-anslutningen har installerats är anslutningen till det offentliga molnet tillgängligt när du använder en-konsol som ansluts till platsen.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android-och iOS-versioner är inte längre riktade i skapande guider för Hybrid MDM

Från och med den här tekniska för hands versionen av hantering av mobila enheter (MDM) behöver du inte längre ange specifika versioner av Android och iOS när du skapar nya principer och profiler för Intune-hanterade enheter. I stället väljer du någon av följande enhets typer:

- Android
- Samsung KNOX Standard 4,0 och högre
- iPhone
- iPad

Den här ändringen påverkar guiderna för att skapa följande objekt:

- Konfigurationsobjekt
- Efterlevnadsprinciper
- Certifikatprofiler
- E-postprofiler
- VPN-profiler
- Wi-Fi-profiler

Med den här ändringen kan hybrid distributioner ge stöd snabbare för nya Android-och iOS-versioner utan att det krävs någon ny Configuration Manager-version eller-tillägg. När en ny version stöds i Intune fristående kommer användarna att kunna uppgradera sina mobila enheter till den versionen.

För att förhindra problem vid uppgradering från tidigare versioner av Configuration Manager är mobila operativ system versioner fortfarande tillgängliga på egenskaps sidorna för dessa objekt. Om du fortfarande behöver ange en viss version som mål, kan du skapa det nya objektet och sedan ange mål versionen på egenskaps sidan för det nya objektet.
