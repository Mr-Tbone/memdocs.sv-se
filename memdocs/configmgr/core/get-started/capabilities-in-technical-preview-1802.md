---
title: Teknisk för hands version 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1802 för Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94208da3eda33cba69f04bbbf42edd08b585c1c4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428197"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Funktioner i Technical Preview 1802 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1802. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. 

Granska [teknisk för hands version för Configuration Manager](technical-preview.md) innan du installerar den här versionen av Technical Preview. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Kända problem i den här tekniska för hands versionen
- **Uppdatering till en ny för hands version Miss lyckas när du har en plats server i passivt läge**. Om du har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)måste du avinstallera plats servern för passivt läge innan du uppdaterar till den nya för hands versionen. Du kan installera om den passiva läges plats servern efter att platsen har slutfört uppdateringen.

  Så här avinstallerar du plats servern för passivt läge:
  1. I Configuration Manager-konsolen går du till **Administration**  >  **Översikt**  >  **plats konfigurations**  >  **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.
  <!--sms 489412-->


</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Över gång Endpoint Protection arbets belastning till Intune med hjälp av samhantering    
<!-- 1357365 -->
I den här versionen kan du nu överföra Endpoint Protection arbets belastningen från Configuration Manager till Intune efter att du aktiverat samhantering. Om du vill överföra Endpoint Protection arbets belastningen går du till sidan Egenskaper för samhantering och flyttar skjutreglaget från Configuration Manager till **pilot** eller **alla**. Mer information finns i [Co-Management för Windows 10-enheter](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurera Windows leverans optimering att använda Configuration Manager gränser grupper
<!-- 1324696 -->
Du använder Configuration Manager gränser grupper för att definiera och reglera innehålls distribution i företags nätverket och på fjärranslutna kontor. [Windows-leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) är en molnbaserad, peer-to-peer-teknik för att dela innehåll mellan Windows 10-enheter. Från och med den här versionen konfigurerar du leverans optimeringen så att du kan använda dina gränser när du delar innehåll mellan peer-datorer. En ny klient inställning tillämpar gränserna för den begränsade gruppen som ID för leverans optimerings grupp på klienten. När klienten kommunicerar med moln tjänsten för leverans optimering används den här identifieraren för att hitta peer-datorer med det önskade innehållet. 

### <a name="prerequisites"></a>Förutsättningar
- Leverans optimering är endast tillgänglig på Windows 10-klienter

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. I Configuration Manager-konsolen, arbets ytan **Administration** , noden **klient inställningar** , skapar du en anpassad princip för klient enhets inställningar.
2. Välj den nya gruppen för **leverans optimering** .
3. Aktivera inställningen **använd Configuration Manager gränser grupper för grupp-ID för leverans optimering**.

Mer information finns i alternativet **grupp** leverans läge i alternativ för [leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Windows 10 på plats-uppgradering av aktivitetssekvensen via Cloud Management Gateway
<!-- 1357149 -->

Aktivitetssekvensen Windows 10 [på plats-uppgradering](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) stöder nu distribution till Internetbaserade klienter som hanteras via [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md). Den här möjligheten gör att fjärran vändare enklare kan uppgradera till Windows 10 utan att behöva ansluta till företags nätverket. 

Se till att allt innehåll som refereras till av aktivitetssekvensen för uppgradering på plats distribueras till en [moln distributions plats](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Annars kan inte enheterna köra aktivitetssekvensen.

När du distribuerar en aktivitetssekvens för uppgradering använder du följande inställningar:
- **Tillåt att aktivitetssekvensen körs för klient på Internet**på fliken Användar upplevelse i distributionen.
- **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**på fliken distributions platser i distributionen. Andra alternativ som **att ladda ned innehåll lokalt när det behövs av aktivitetssekvensen som körs** fungerar inte i det här scenariot. Motorn för aktivitetssekvenser kan för närvarande inte hämta innehåll från en moln distributions plats. Den Configuration Manager klienten måste ladda ned innehållet från moln distributions platsen innan aktivitetssekvensen startas.
- (*Valfritt*) **Hämta innehåll i förväg för den här aktivitetssekvensen**på fliken Allmänt i distributionen. Mer information finns i [Konfigurera förinställt innehåll för cache](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Förbättringar av aktivitetssekvens för Windows 10-uppgradering på plats
<!-- 1357425 -->
Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller nu ytterligare grupper med rekommenderade åtgärder som ska läggas till före och efter uppgraderings processen. Dessa åtgärder är gemensamma för många kunder som har lyckats uppgradera enheter till Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nya grupper under **förbereda för uppgradering**
- **Batteri kontroller**: Lägg till steg i den här gruppen för att kontrol lera om datorn använder batteri eller kabelansluten ström. Den här åtgärden kräver ett anpassat skript eller verktyg för att utföra den här kontrollen.
- **Kontroller för nätverks-/kabelanslutna anslutningar**: Lägg till steg i den här gruppen för att kontrol lera om datorn är ansluten till ett nätverk och inte använder en trådlös anslutning. Den här åtgärden kräver ett anpassat skript eller verktyg för att utföra den här kontrollen.
- **Ta bort inkompatibla program**: Lägg till steg i den här gruppen för att ta bort alla program som inte är kompatibla med den här versionen av Windows 10. Metoden för att avinstallera ett program varierar. Om programmet använder Windows Installer kopierar du kommando raden **Avinstallera program** från fliken **program** i egenskaperna för Windows Installer distributions typ för programmet. Lägg sedan till steget **Kör kommando rad** i den här gruppen med kommando raden avinstallera program. Ett exempel: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Ta bort inkompatibla driv rutiner**: Lägg till steg i den här gruppen för att ta bort driv rutiner som inte är kompatibla med den här versionen av Windows 10.
- **Ta bort/pausa säkerhet från tredje part**: Lägg till steg i den här gruppen för att ta bort eller pausa säkerhets program från tredje part, till exempel Antivirus.
   - Om du använder ett disk krypterings program från tredje part, anger du dess krypterings driv rutin för Installationsprogrammet för Windows med [kommando rads alternativet](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers** . Lägg till [variabel steget Ställ in](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) aktivitetssekvens i aktivitetssekvensen i den här gruppen. Ange variabeln för aktivitetssekvensen till **OSDSetupAdditionalUpgradeOptions**. Ange värdet **/ReflectDriver** med sökvägen till driv rutinen. Den här [Åtgärds variabeln](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) för aktivitetssekvensen lägger till installationsprogrammet för Windows kommando raden som används av aktivitetssekvensen. Kontakta program varu leverantören om du behöver ytterligare vägledning om den här processen.

### <a name="new-groups-under-post-processing"></a>Nya grupper under **efter bearbetning**
- **Använd installationsbaserade driv rutiner**: Lägg till steg i den här gruppen för att installera installationsbaserade driv rutiner (. exe) från paket.
- **Installera/Aktivera säkerhet från tredje part**: Lägg till steg i den här gruppen för att installera eller aktivera säkerhets program från tredje part, till exempel antivirus program. 
- **Ange standardappar och associationer för Windows**: Lägg till steg i den här gruppen för att ange Windows standard-appar och fil associationer. Förbered först en referens dator med önskade app-associationer. Kör sedan följande kommando rad för att exportera: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Lägg till XML-filen i ett paket. Lägg sedan till steget [Kör kommando rad](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) i den här gruppen. Ange det paket som innehåller XML-filen och ange följande kommando rad: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Mer information finns i [Exportera eller importera standard program associationer](https://docs.microsoft.com/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Tillämpa anpassningar och**anpassningar: Lägg till steg i den här gruppen för att tillämpa anpassningar av Start-menyn, till exempel ordna program grupper. Mer information finns i [Anpassa Start skärmen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Ytterligare rekommendationer
- Läs igenom Windows-dokumentationen för att [lösa Windows 10-uppgraderings fel](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Den här artikeln innehåller även detaljerad information om uppgraderings processen.
- I steget standard **kontroll beredskap** aktiverar du **minsta ledigt disk utrymme (MB)**. Ange värdet till minst **16384** (16 GB) för ett 32-bitars uppgraderings paket för operativ system, eller **20480** (20 GB) för 64-bitars. 
- Använd den **SMSTSDownloadRetryCount** [inbyggda variabeln](../../osd/understand/task-sequence-variables.md) SMSTSDownloadRetryCount för att försöka hämta principen igen. Som standard försöker klienten igen två gånger; den här variabeln anges till två (2). Om klienterna inte är på en kabelansluten företags nätverks anslutning, kommer ytterligare försök att hjälpa klienten att hämta principer. Om den här variabeln används får ingen negativ sido effekt, förutom fördröjt fel om den inte kan hämta principen.<!-- 501016 --> Öka också **SMSTSDownloadRetryDelay** -variabeln från standardvärdet på 15 sekunder.
- Utför en intern kompatibilitetskontroll. 
   - Lägg till ett andra **uppgraderings operativ system** steg tidigt i **förbereda för uppgraderings** gruppen. Bedöm namn för *uppgradering*av namn. Ange samma uppgraderings paket och aktivera sedan alternativet för att **utföra installationsprogrammet för Windows kompatibilitetskontroll utan att starta uppgraderingen**. Aktivera **Fortsätt vid fel** på fliken Alternativ. 
   - Omedelbart efter det här steget för *uppgraderings utvärdering* lägger du till steget **Kör kommando rad** . Ange följande kommando rad:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Lägg till följande villkor på fliken **alternativ** : </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Den här retur koden är den decimal som motsvarar MOSETUP_E_COMPAT_SCANONLY (0xC1900210), som är en lyckad kompatibilitetskontroll utan problem. Om steget för *uppgraderings utvärdering* lyckas och returnerar den här koden hoppas det här steget över. Annars Miss lyckas aktivitetssekvensen med retur koden från Installationsprogrammet för Windows kompatibilitetskontroll, om bedömnings steget returnerar andra retur koder.
   - Mer information finns i [Uppgradera operativ system](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Om du vill ändra enheten från BIOS till UEFI under den här aktivitetssekvensen, se [konvertera från BIOS till UEFI under en uppgradering på plats](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

Skicka **feedback** från fliken **Start** i menyfliksområdet om du har ytterligare rekommendationer eller förslag.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Förbättringar av PXE-aktiverade distributions platser
<!-- 1357580 -->
För att klargöra beteendet för [nya PXE-funktioner](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) som introducerades i Technical Preview version 1706 har vi bytt namn till **IPv6-** alternativet för stöd. På fliken **PXE** i egenskaperna för distributions platsen markerar du **Aktivera en PXE-svarare utan Windows Deployment-tjänst**. 

Med det här alternativet aktive ras en PXE-svarare på distributions platsen, vilket inte kräver Windows Deployment Services (WDS). Om du aktiverar det här nya alternativet på en distributions plats som redan är PXE-aktiverad, pausar Configuration Manager WDS-tjänsten. Om du inaktiverar det här nya alternativet men fortfarande **aktiverar PXE-stöd för klienter**, aktiverar distributions platsen WDS igen.

Eftersom WDS inte krävs kan den PXE-aktiverade distributions platsen vara en klient eller ett serveroperativ system, inklusive Windows Server Core. Den här nya PXE responder-tjänsten fortsätter att stödja IPv6, och förbättrar även flexibiliteten i PXE-aktiverade distributions platser på fjärranslutna kontor.

> [!NOTE]
> Den här tjänsten använder samma grundläggande teknik som den [klientbaserade PXE responder-tjänsten](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) i teknisk för hands version 1712. Funktionen kräver inte distributions plats rollens omkostnader.

### <a name="multicast"></a>Multicast
Om du vill aktivera och konfigurera multicast på fliken **multicast** i egenskaperna för distributions platsen, måste distributions platsen använda WDS. 
- Om du **aktiverar PXE-stöd för klienter** och **gör det möjligt för multicast att samtidigt skicka data till flera klienter**kan du inte **Aktivera en PXE-svarare utan Windows Deployment-tjänst**.
- Om du **aktiverar PXE-stöd för klienter** och **aktiverar en PXE-svarare utan Windows Deployment service**, kan du inte **Aktivera multicast för att samtidigt skicka data till flera klienter**



## <a name="deployment-templates-for-task-sequences"></a>Distributionsmall för aktivitetssekvenser
<!-- 1357391 -->
I distributions guiden för aktivitetssekvenser kan du nu skapa en distributionsmall. Distributions mal len kan sparas och tillämpas på en befintlig eller ny aktivitetssekvens för att skapa en distribution. 

### <a name="try-it-out"></a>prova!  
Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade. 

 **Skapa en Distributionsmall för en ny aktivitetssekvensdistribution** <br/> 
1. I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer **aktivitetssekvenser**.
2. Högerklicka på en aktivitetssekvens och välj **distribuera**. 
3. På fliken **Allmänt** noterar du nu ett alternativ för att **välja distributions mal len**. 
4. Fortsätt med **guiden distribuera program vara** och välj distributions inställningarna för aktivitetssekvensen. 
5. När du kommer till fliken **Sammanfattning** i **guiden distribuera program vara**klickar du på **Spara som mall**.
6. Ge mallen ett namn och välj de inställningar som ska sparas i mallen. 
7. Klicka på **Spara**. Mallen är nu tillgänglig för användning från alternativet **Välj distributions mal len** .



## <a name="product-lifecycle-dashboard"></a>Instrument panel för produkt livs cykel
<!--1319632-->
Den nya [instrument panelen för produktens livs cykel](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) visar statusen för Microsofts produkt livs cykel princip för Microsoft-produkter som är installerade på enheter som hanteras med Configuration Manager. På instrument panelen får du information om Microsoft-produkter i din miljö, support tillstånd och slutdatum för support. Du kan använda instrument panelen för att förstå tillgängligheten för varje produkt. 

Öppna instrument panelen för livs cykeln genom att gå till **till gångar och efterlevnad**  > **tillgångsinformation**  > **produktens livs cykel** i Configuration Manager-konsolen



## <a name="improvements-to-reporting"></a>Förbättringar av rapportering
<!--1357653-->
Till följd av [din feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) har vi lagt till en ny rapport, **service information för Windows 10 för en speciell samling**. Den här rapporten innehåller resurs-ID, NetBIOS-namn, OS-namn, namn på operativ system version, build, OS-gren och service nivå för Windows 10-enheter. Om du vill ha åtkomst till rapporten går du till **övervakning**  > **rapporterings**  > **rapporter**  > **operativ system**  > **Windows 10 service information för en speciell samling**.



## <a name="improvements-to-software-center"></a>Förbättringar av Software Center
<!--1357592-->
Resultatet av [dina feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) -installerade program kan nu döljas i Software Center. Program som redan är installerade visas inte längre på fliken program när det här alternativet är aktiverat. 

### <a name="try-it-out"></a>prova!
Aktivera inställningen **Dölj installerade program i Software Center** i klient inställningarna för Software Center. Observera beteendet i Software Center när slutanvändaren installerar ett program.



## <a name="improvements-to-run-scripts"></a>Förbättringar för att köra skript
<!--1236459-->
Funktionen [Kör skript](../../apps/deploy-use/create-deploy-scripts.md) returnerar nu skript utmatningen med JSON-formatering. Det här formatet returnerar konsekvent utdata för skript. Skript som inte kan köras kan inte returnera utdata. 



## <a name="boundary-group-fallback-for-management-points"></a>Återställning av gränser grupper för hanterings platser
<!-- 1324594 -->
Från och med den här versionen kan du konfigurera återställnings relationer för hanterings platser mellan [gränser grupper](../servers/deploy/configure/boundary-groups.md). Det här beteendet ger större kontroll för de hanterings platser som klienterna använder. På fliken **relationer** i egenskaperna för gränser-gruppen finns det en ny kolumn för hanterings platsen. När du lägger till en ny återställnings gräns grupp är återställnings tiden för hanterings platsen för närvarande alltid noll (0). Det här beteendet är detsamma för **standard beteendet** på platsens standard gränser grupp.

Tidigare inträffar ett vanligt problem när du har en skyddad hanterings plats i ett säkert nätverk. Klienter i huvud företags nätverket tar emot en princip som inkluderar den här skyddade hanterings platsen, även om de inte kan kommunicera med den via en brand vägg. Du löser problemet genom att använda alternativet Återställ **aldrig återställnings** alternativ för att säkerställa att klienter endast återställnings punkter till hanterings platser som de kan kommunicera med.

När du uppgraderar platsen till den här versionen lägger Configuration Manager till alla hanterings platser som inte är baserade på Internet i standard plats för webbplatsen. Det här uppgraderings beteendet säkerställer att äldre klient versioner fortsätter att kommunicera med hanterings platser. För att dra full nytta av den här funktionen, flytta hanterings platserna till önskade gränser grupper.

Återställningen av hanterings platsens gränser påverkar inte beteendet under klient installationen (CCMSetup). Om kommando raden inte anger den första hanterings platsen med hjälp av parametern/MP får den nya klienten fullständig lista över tillgängliga hanterings platser. Vid den första start processen använder klienten den första hanterings plats som den kan komma åt. När klienten registrerar sig på platsen får den hanterings plats listan korrekt sorterad med det nya beteendet. 

### <a name="prerequisites"></a>Förutsättningar
- Aktivera [prioriterade hanterings platser](../servers/deploy/configure/boundary-groups.md#bkmk_preferred). Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration** och välj **platser**. Klicka på **Inställningar för hierarki** i menyfliksområdet. På fliken **Allmänt** väljer du aktivera **klienter vill använda hanterings platser som anges i gränser grupper**. 

### <a name="known-issues"></a>Kända problem
- Processerna för operativ Systems distribution är inte medvetna om gränser grupper.

### <a name="troubleshooting"></a>Felsökning
Nya poster visas i **filen LocationServices. log**. Attributet för **lokalitet** identifierar något av följande tillstånd:
- 0: okänd
- 1: den angivna hanterings platsen finns bara i platsens standard gränser grupp för återställning
- 2: den angivna hanterings platsen finns i en fjärran sluten plats eller i en intilliggande gränser grupp. Om hanterings platsen finns i både en granne och platsens standard gränser, är den lokala platsen 2.
- 3: den angivna hanterings platsen finns i den lokala eller aktuella gränser gruppen. Om hanterings platsen finns i den aktuella gränser-gruppen samt antingen en granne eller platsens standard gränser grupp är platsen 3. Om du inte aktiverar inställningen för önskade hanterings platser i hierarkiska inställningar är den lokala platsen alltid 3 oavsett vilken begränsande grupp hanterings platsen finns i.

Klienterna använder lokala hanterings platser först (lokal 3), fjärran sluten sekund (plats 2) och sedan reserv (plats 1). 

När en klient tar emot fem fel på tio minuter och inte kommunicerar med en hanterings plats i den aktuella gräns gruppen, försöker den kontakta en hanterings plats i en granne eller platsens standard gräns grupp. Om hanterings platsen i den aktuella anspråks gruppen senare kommer tillbaka online återgår klienten till den lokala hanterings platsen vid nästa uppdaterings cykel. Uppdaterings cykeln är 24 timmar eller när den Configuration Manager Agent tjänsten startas om.



## <a name="improved-support-for-cng-certificates"></a>Förbättrat stöd för CNG-certifikat
<!-- 1357314 -->
Configuration Manager (aktuell gren) version 1710 stöder [kryptografi: CNG-certifikat (Next Generation)](../plan-design/network/cng-certificates-overview.md). Version 1710 begränsar stödet till klient certifikat i flera scenarier. 

Från och med den här tekniska för hands versionen använder du CNG-certifikat för följande HTTPS-aktiverade Server roller:
- Hanteringsplats
- Distributionsplats
- Programuppdateringsplats

Listan över [scenarier som inte stöds](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) är oförändrade.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Stöd för Cloud Management Gateway för Azure Resource Manager
<!-- 1324735 -->
När du skapar en instans av CMG ( [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) ) ger guiden nu möjlighet att skapa en **Azure Resource Manager distribution**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en [resurs grupp](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). När du distribuerar CMG med Azure Resource Manager använder platsen Azure Active Directory (Azure AD) för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure.  

Guiden CMG ger fortfarande möjlighet att använda en **klassisk tjänst distribution** med ett hanterings certifikat för Azure. För att förenkla distributionen och hanteringen av resurser rekommenderar vi att du använder Azure Resource Manager distributions modell för alla nya CMG-instanser. Distribuera om möjligt Befintliga CMG-instanser via Resource Manager.

Configuration Manager migrerar inte befintliga klassiska CMG-instanser till Azure Resource Manager distributions modell. Skapa nya CMG-instanser med Azure Resource Manager-distributioner och ta sedan bort klassiska CMG-instanser. 

> [!IMPORTANT]
> Den här funktionen aktiverar inte stöd för Azure Cloud Service-leverantörer (CSP). CMG-distributionen med Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av KRYPTOGRAFIPROVIDERn. Mer information finns i [tillgängliga Azure-tjänster i Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Förutsättningar
- Integrering med [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Identifiering av Azure AD-användare krävs inte.
- Samma [krav för Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), förutom för Azures hanterings certifikat.

### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. I Configuration Manager-konsolen, arbets ytan **Administration** , expandera **Cloud Services**och välj **Cloud Management Gateway**. Klicka på **skapa Cloud Management Gateway** i menyfliksområdet. 
2. På sidan **Allmänt** väljer du **Azure Resource Manager distribution**. Klicka på **Logga** in för att autentisera med ett administratörs konto för Azure-prenumeration. Guiden fyller automatiskt i de återstående fälten från den Azure AD-prenumerations information som lagras under integrations kravet. Om du äger flera prenumerationer väljer du den prenumeration som du vill använda. Klicka på **Nästa**.  
3. På sidan **Inställningar** anger du serverns PKI-certifikatfil som vanligt. Det här certifikatet definierar CMG-tjänstens namn i Azure. Välj **region**och välj sedan ett resurs grupps alternativ för att antingen **skapa nya** eller **använda befintliga**. Ange namnet på den nya resurs gruppen eller Välj en befintlig resurs grupp i list rutan. 
4. Slutför guiden.

> [!NOTE] 
> För den valda Azure AD server-appen tilldelar Azure prenumerations **deltagar** behörigheten. 

Övervaka förlopps distributionen för tjänsten med **CloudMgr. log** på tjänst anslutnings punkten.



## <a name="approve-application-requests-for-users-per-device"></a>Godkänn program begär Anden för användare per enhet
<!-- 1357015 -->
Från och med den här versionen, när en användare begär ett program som kräver godkännande, är det specifika enhets namnet nu en del av begäran. Om administratören godkänner begäran kan användaren bara installera programmet på den enheten. Användaren måste skicka en annan begäran om att installera programmet på en annan enhet. 

> [!NOTE]
> Den här funktionen är valfri. När du uppdaterar till den här versionen aktiverar du den här funktionen i uppdaterings guiden. Du kan också aktivera funktionen i-konsolen senare. Mer information finns i avsnittet [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Förutsättningar
- Uppgradera Configuration Manager-klienten till den senaste versionen
- Aktivera klient inställningen **Använd nya Software Center** i [dator agent](../clients/deploy/about-client-settings.md#computer-agent) gruppen

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. Distribuera ett program som tillgängligt för en användar samling.
2. På sidan **distributions inställningar** aktiverar du alternativet: **en administratör måste godkänna en begäran för det här programmet på enheten**.
3. Som mål användare använder Software Center för att skicka en begäran om programmet. 
4. Visa **begäran om godkännande** under **program hantering** i arbets ytan **program varu bibliotek** i Configuration Manager-konsolen. Det finns nu en **enhets** kolumn i listan för varje begäran. När du vidtar åtgärder på begäran innehåller dialog rutan programbegäran även enhets namnet som användaren skickade begäran från.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Använd Software Center för att söka efter och installera användar tillgängliga program på Azure AD-anslutna enheter
<!-- 1322613 -->
Om du distribuerar program som tillgängliga för användare kan de nu bläddra och installera dem via Software Center på Azure Active Directory (Azure AD)-enheter.  

### <a name="prerequisites"></a>Förutsättningar
- Aktivera HTTPS på hanterings platsen
- Integrera webbplatsen med [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Distribuera ett program som tillgängligt för en användar samling
- Distribuera alla program innehåll till en [moln distributions plats](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Aktivera klient inställningen **Använd nya Software Center** i [dator agent](../clients/deploy/about-client-settings.md#computer-agent) gruppen
- Klienten måste vara: 
   - Windows 10
   - Azure AD-ansluten, även känd som molnbaserad domänanslutna
- För att stödja Internetbaserade klienter:
    - [Gateway för molnhantering](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Aktivera klient inställningen: **Aktivera användar princip begär Anden från Internet klienter** i [klient princip](../clients/deploy/about-client-settings.md#client-policy) gruppen
- För att stödja klienter i företags nätverket:
    - Lägg till moln distributions platsen i en begränsande grupp som används av klienterna
    - Klienterna måste kunna matcha det fullständigt kvalificerade domän namnet (FQDN) för den HTTPS-aktiverade hanterings platsen



## <a name="report-on-windows-autopilot-device-information"></a>Rapport om Windows autopilot-enhets information
<!-- 1351442 -->
Windows autopilot är en lösning för att onboarding och konfigurera nya Windows 10-enheter på ett modernt sätt. Mer information finns i [Översikt över Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). En metod för att registrera befintliga enheter med Windows autopilot är att överföra enhets information till Microsoft Store för företag och utbildning. Den här informationen omfattar enhetens serie nummer, Windows produkt identifierare och en maskin varu identifierare. Använd Configuration Manager för att samla in och rapportera den här enhets informationen. 

### <a name="prerequisites"></a>Förutsättningar
- Den här enhets informationen gäller endast för klienter i Windows 10, version 1703 och senare

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. I Configuration Manager-konsolen, **övervaknings** arbets ytan, expanderar du noden **rapportering** , expanderar **rapporter**och väljer **maskin vara-allmänt-** noden.
2. Kör den nya rapporten, **enhets information för Windows autopilot** och visa resultatet. 
3. I rapport visnings programmet klickar du på **export** ikonen och väljer **CSV (kommaavgränsad)** .
4. När du har sparat filen laddar du upp data till Microsoft Store för företag och utbildning. Mer information finns i [lägga till enheter i Microsoft Store för företag och utbildning](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Förbättringar av Configuration Manager principer för Windows Defender sårbarhet Guard
<!-- 1356220 -->
Ytterligare princip inställningar för komponenten för minskning av attack ytan och reglerad mappåtkomst har lagts till i Configuration Manager för [Windows Defender sårbarhet Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).

**Nya inställningar för reglerad mappåtkomst**<br/>
Det finns två ytterligare alternativ när du konfigurerar reglerad mappåtkomst: **Blockera endast disk sektorer** och **Granska endast disk sektorer**. De här två inställningarna tillåter regler för kontrollerad mappåtkomst att endast aktive ras för start sektorer och aktiverar inte skydd av vissa mappar eller de skyddade standardmapparna. 

**Nya inställningar för minskning av attack ytan**
- Använd avancerat skydd mot utpressnings troprodukter.
- Blockera autentiseringsuppgifter som stjälas från Windows-undersystemet för lokal säkerhets auktoritet. 
- Blockera körbara filer från att köras om de inte uppfyller ett villkor för användningsmönster, ålder eller betrodd lista. 
- Blockera obetrodda och osignerade processer som körs via USB.



## <a name="microsoft-edge-browser-policies"></a>Principer för Microsoft Edge-webbläsare
<!-- 1357310 -->
För kunder som använder [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) -webbläsaren på Windows 10-klienter kan du nu skapa en princip för Configuration Manager kompatibilitetsinställningar för att konfigurera flera Microsoft Edge-inställningar. Den här principen innehåller för närvarande följande inställningar:
- **Ange Microsoft Edge-webbläsare som standard**: konfigurerar Windows 10-standardappens inställning för webbläsare till Microsoft Edge
- **Tillåt listruta för adress fält**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för AllowAddressBarDropdown-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Tillåt synkronisering av favoriter mellan Microsoft-webbläsare**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för SyncFavoritesBetweenIEAndMicrosoftEdge-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Tillåt rensning av webb data vid avslut**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för ClearBrowsingDataOnExit-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Tillåt Not Track-huvuden**: Mer information finns i [AllowDoNotTrack Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Tillåt Autofyll**: Mer information finns i [AllowAutofill Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Tillåt cookies**: Mer information finns i [AllowCookies Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Tillåt blockering av popup-fönster**: Mer information finns i [AllowPopups Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Tillåt Sök förslag i adress fältet**: Mer information finns i [AllowSearchSuggestionsinAddressBar Browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Tillåt sändning av intranäts trafik till Internet Explorer**: Mer information finns i [SendIntranetTraffictoInternetExplorer Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Tillåt lösen ords hanteraren**: Mer information finns i [AllowPasswordManager Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Tillåt utvecklarverktyg**: Mer information finns i [princip för AllowDeveloperTools-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Tillåt tillägg**: Mer information finns i [AllowExtensions Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Förutsättningar
- Windows 10-klient som är Azure Active Directory ansluten. 

### <a name="known-issues"></a>Kända problem
- Lokala domänanslutna enheter kan inte tillämpa den här principen i den här versionen. Det här problemet gäller även för Hybrid domänanslutna enheter.

### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

**Skapa principen**
1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar** och välj den nya noden **Microsoft Edge-webbläsar profiler** . Klicka på alternativet menyfliksområde för att **skapa en policy för Microsoft Edge-webbläsaren**.
2. Ange ett **namn** för principen, ange en **Beskrivning**(valfritt) och klicka på **Nästa**.
3. På sidan **Inställningar** ändrar du värdet till **konfigurerat** för inställningarna som ska tas med i den här principen och klickar på **Nästa**.
4. På sidan **plattformar som stöds** väljer du de operativ system versioner och arkitekturer som den här principen gäller för och klickar på **Nästa**. 
5. Slutför guiden.

**Distribuera principen**
1. Välj din princip och klicka på alternativet för menyfliksområdet som ska **distribueras**.
2. Klicka på **Bläddra** och välj den användar-eller enhets samling som du vill distribuera principen till. 
3. Välj ytterligare alternativ vid behov. Generera aviseringar när principen inte är kompatibel. Ange det schema enligt vilket klienten utvärderar enhetens kompatibilitet med den här principen.
4. Klicka på **OK** för att skapa distributionen.

Precis som alla inställningar för efterlevnadsprinciper åtgärdar klienten inställningarna enligt det schema du anger. [Övervaka och rapportera om enhetens efterlevnad](../../compliance/deploy-use/monitor-compliance-settings.md) i Configuration Manager-konsolen.



## <a name="report-for-default-browser-counts"></a>Rapport för antal standard webbläsare
<!-- 1357830 -->
Nu finns det en ny rapport för att visa antalet klienter med en speciell webbläsare som Windows standard. 

### <a name="known-issues"></a>Kända problem
- Första gången du öppnar rapporten visar den bara antalet och inte BrowserProgID. Undvik det här problemet genom att redigera frågan för rapporten till följande syntax:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.
1. I **Configuration Manager** -konsolen, **övervaknings** arbets yta, expandera **rapportering**, expandera **rapporter**, Välj **program vara-företag och produkter**.
2. Kör **standard rapporten antal webbläsare** .

Använd följande referens för vanliga BrowserProgIDs:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE. HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera program vara
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Stöd för Windows 10 ARM64-enheter
<!-- 1353704 -->
Från och med den här versionen stöds Configuration Manager-klienten på Windows 10 ARM64-enheter. Befintliga klient hanterings funktioner bör fungera med de här nya enheterna. Till exempel maskin-och program varu inventering, program uppdateringar och program hantering. Distribution av operativ system stöds inte för närvarande. 

## <a name="changes-to-phased-deployments"></a>Ändringar i stegvisa distributioner
<!-- 1357405 -->
Stegvisa distributioner automatiserar en samordnad, sekvenserad distribution av program vara i flera samlingar. I den här tekniska för hands versionen kan guiden stegvis distribution utföras för aktivitetssekvenser i administratörs konsolen och distributioner skapas. Den andra fasen startar dock inte automatiskt efter att du uppfyller villkoren i den första fasen. Den andra fasen kan startas manuellt med ett SQL-uttryck.   

### <a name="try-it-out"></a>prova!  
  Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.
 
**Skapa en stegvis distribution för en aktivitetssekvens** </br>
1. I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer **aktivitetssekvenser**.
2. Högerklicka på en befintlig aktivitetssekvens och välj **skapa stegvis distribution**. 
3. På fliken **Allmänt** anger du den stegvisa distributionen ett namn, en beskrivning (valfritt) och väljer **Skapa automatiskt en standard distribution av två faser**. 
4. Fyll i fälten **första samling** och **andra samling** . Välj **Nästa**.
5. På fliken **Inställningar** väljer du ett alternativ för var och en av schemaläggnings inställningarna och väljer **Nästa** när du är klar. 
6. På fliken **faser** redigerar du någon av stegen om det behövs och klickar sedan på **Nästa**.
7. Bekräfta dina val på fliken **Sammanfattning** och klicka sedan på **Nästa** för att fortsätta.
8. När de slutförda villkoren för den första fasen har nåtts följer du anvisningarna för att starta den andra fasen med en SQL-sats.
 
**Starta den andra fasen med ett SQL-uttryck**
1. Identifiera PhasedDeploymentID för den distribution som du skapade med följande SQL-fr åga:<br/> `Select * from PhasedDeployment`
2. Kör följande instruktion för att starta produktions fasen:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
