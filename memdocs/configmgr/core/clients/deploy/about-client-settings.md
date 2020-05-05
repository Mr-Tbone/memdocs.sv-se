---
title: Klientinställningar
titleSuffix: Configuration Manager
description: Lär dig mer om standard-och anpassade inställningar för att styra klient beteenden
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1435c1ab6be8c80178566ae9d354084fddebb22a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771356"
---
# <a name="about-client-settings-in-configuration-manager"></a>Om klient inställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Hantera alla klient inställningar i Configuration Manager-konsolen från noden **klient inställningar** på arbets ytan **Administration** . Configuration Manager innehåller en uppsättning standardinställningar. När du ändrar standard klient inställningarna tillämpas de här inställningarna på alla klienter i hierarkin. Du kan också konfigurera anpassade klient inställningar som åsidosätter standard klient inställningarna när du tilldelar dem till samlingar. Mer information finns i [så här konfigurerar du klient inställningar](configure-client-settings.md).

I följande avsnitt beskrivs inställningar och alternativ i detalj.  


## <a name="background-intelligent-transfer-service-bits"></a>Background Intelligent Transfer Service (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Begränsa den maximala nätverksbandbredden för BITS-bakgrundsöverföring

När det här alternativet är **Ja**använder klienterna bandbredds begränsning i BITS. Om du vill konfigurera de andra inställningarna i den här gruppen måste du aktivera den här inställningen.

### <a name="throttling-window-start-time"></a>Starttid för begränsningsfönstret

Ange den lokala Start tiden för BITS-begränsnings fönstret.  

### <a name="throttling-window-end-time"></a>Sluttid för begränsningsfönstret

Ange den lokala slut tiden för BITS-begränsnings fönstret. Om slut tiden är lika med **Start tiden för begränsnings fönstret**är BITS-begränsning alltid aktiverat.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Maximal överföringshastighet under begränsningsfönstret (kbit/s)

Ange den maximala överföringshastigheten som klienter kan använda under fönstret.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Tillåt BITS-hämtningar utanför begränsningsfönstret

Tillåt klienter att använda separata BITS-inställningar utanför det angivna fönstret.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Maximal överföringshastighet utanför begränsningsfönstret (kbit/s)

Ange den maximala överföringshastigheten som klienter kan använda utanför BITS-begränsnings fönstret.  



## <a name="client-cache-settings"></a>Inställningar för klient-cache

### <a name="configure-branchcache"></a>Konfigurera BranchCache

Konfigurera klient datorn för [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). Om du vill tillåta BranchCache-cachelagring på klienten anger du **Aktivera BranchCache** till **Ja**.

- **Aktivera BranchCache**: aktiverar BranchCache på klient datorer.

- **Maximal cachestorlek för BranchCache (procent andel av disken)**: den procent andel av disken som du tillåter BranchCache att använda.

> [!TIP]
> Om du ställer in **Konfigurera BranchCache** på **Nej**konfigurerar Configuration Manager inte några BranchCache-inställningar.
>
> Om du vill inaktivera BranchCache ställer du in **BranchCache** på **Ja**och anger sedan **Aktivera BranchCache** till **Nej**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Konfigurera cache-storlek för klienter

Configuration Manager-klientcachen på Windows-datorer lagrar temporära filer som används för att installera program och program. Om det här alternativet är inställt på **Nej**är standard storleken 5 120 MB.

Om du väljer **Ja**anger du:

- **Maximal cachestorlek (MB)**
- **Maximal cachestorlek (procent andel av disken)**: klientens cachestorlek expanderar till den maximala storleken i megabyte (MB) eller procent andelen av disken, beroende på vilket som är mindre.

### <a name="enable-as-peer-cache-source"></a>Aktivera som peer-cache-källa

> [!Note]  
> I version 1902 och tidigare kallades den här inställningen **aktivera Configuration Manager klienten i fullständigt operativ system för att dela innehåll**. Beteendet för inställningen ändrades inte.

Aktiverar [peer-cache](../../plan-design/hierarchy/client-peer-cache.md) för Configuration Manager klienter. Välj **Ja**och ange sedan den port som klienten kommunicerar med peer-datorn.

- **Port för första nätverks sändning** (standard UDP 8004): Configuration Manager använder den här porten i Windows PE eller det fullständiga Windows OS. Motorn för aktivitetssekvenser i Windows PE skickar sändningen för att hämta innehålls platser innan aktivitetssekvensen startas.<!--SCCMDocs issue 910-->

- **Port för nedladdning av innehåll från peer** (standard TCP 8003): Configuration Manager konfigurerar automatiskt regler för Windows-brandväggen för att tillåta den här trafiken. Om du använder en annan brand vägg måste du manuellt konfigurera regler för att tillåta den här trafiken.  

    Mer information finns i [portar som används för anslutningar](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Minsta varaktighet innan cachelagrat innehåll kan tas bort (minuter)

<!--4485509-->
Från och med version 1906 anger du den minsta tiden som den Configuration Manager klienten ska behålla cachelagrat innehåll. Den här klient inställningen definierar den minsta tids period Configuration Manager agenten ska vänta innan den kan ta bort innehåll från cachen om mer utrymme behövs.

Som standard är det här värdet 1 440 minuter (24 timmar).
Det maximala värdet för den här inställningen är 10 080 minuter (1 vecka).

Den här inställningen ger dig större kontroll över klientens cacheminne på olika typer av enheter. Du kan minska värdet på klienter som har små hård diskar och inte behöver behålla befintligt innehåll innan en annan distribution körs.


## <a name="client-policy"></a>Klient princip  

### <a name="client-policy-polling-interval-minutes"></a>Avsökningsintervall för klientprincip (minuter)

Anger hur ofta följande Configuration Manager klienter hämtar klient princip:

- Windows-datorer (till exempel skrivbordsdatorer, servrar, bärbara datorer)  
- Mobila enheter som Configuration Manager registrerar  
- Mac-datorer  
- Datorer som kör Linux eller UNIX  

Det här värdet är 60 minuter som standard. Genom att minska det här värdet kan klienterna söka på platsen oftare. Med flera klienter kan det här beteendet ha en negativ inverkan på platsens prestanda. [Rikt linjerna för storlek och skala](../../plan-design/configs/size-and-scale-numbers.md) baseras på standardvärdet. Om du ökar det här värdet går det snabbare att söka efter platsen. Eventuella ändringar i klient principerna, inklusive nya distributioner, tar längre tid för klienter att ladda ned och bearbeta.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Aktivera användar princip på klienter

När du ställer in det här alternativet på **Ja**och använder [användar identifiering](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), får klienterna program och program som är riktade till den inloggade användaren.  

Om den här inställningen är **Nej**får användarna inte de nödvändiga program som du distribuerar till användare. Användarna får inte heller några andra hanterings uppgifter i användar principer.  

Den här inställningen gäller för användare när deras dator är antingen i intranätet eller på Internet. Det måste vara **Ja** om du också vill aktivera användar principer på Internet.  

> [!Note]  
> Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte installera nya program katalog roller.
>
> Om du fortfarande använder program katalogen får du en lista över tillgänglig program vara för användare från plats servern. Därför behöver den här inställningen inte vara **Ja** för att användarna ska kunna se och begära program från program katalogen. Om den här inställningen är **Nej**kan användarna inte installera de program som de ser i program katalogen.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Aktivera användar princip begär Anden från Internet klienter

Ställ in det här alternativet på **Ja** för att användarna ska kunna ta emot användar principen på Internet-baserade datorer. Följande krav gäller också:  

- Klienten och platsen är konfigurerade för [Internetbaserad klient hantering](../manage/plan-internet-based-client-management.md) eller en [Gateway för moln hantering](../manage/cmg/plan-cloud-management-gateway.md).  

- Inställningen **Aktivera användar princip på klienter** är **Ja**.  

- Den Internetbaserad hanterings platsen autentiserar användaren med hjälp av Windows-autentisering (Kerberos eller NTLM). Mer information finns i [överväganden för klient kommunikation från Internet](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Cloud Management Gateway har autentiserat användaren med hjälp av Azure Active Directory. Mer information finns i [distribuera användar tillgängliga program på Azure AD-anslutna enheter](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Om du ställer in det här alternativet på **Nej**, eller om något av de tidigare kraven inte uppfylls, så tar en dator på Internet bara emot dator principer. I det här scenariot kan användarna fortfarande se, begära och installera program från en Internetbaserad program katalog. Om den här inställningen är **Nej**men **Aktivera användar princip på klienter** är **Ja**, får användarna inga användar principer förrän datorn är ansluten till intranätet.  

> [!NOTE]  
> För internetbaserad klient hantering behöver begäran om program godkännande från användare inte användar principer eller användarautentisering. Cloud Management Gateway stöder inte begär Anden om program godkännande.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Aktivera användar princip för flera användarsessioner

<!--4737447-->

*Gäller för version 1910*

Som standard är denna inställning inaktiverad. Även om du aktiverar användar principer och startar i version 1906 inaktive ras de som standard på alla enheter som tillåter flera samtidiga aktiva användarsessioner. Till exempel Terminal-servrar eller Windows 10 Enterprise multi-session i [det virtuella Windows-skrivbordet](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

Klienten inaktiverar bara användar principen när den identifierar den här typen av enhet under en ny installation. För en befintlig klient av den här typen som du uppdaterar till version 1906 eller senare, kvarstår det tidigare beteendet. På en befintlig enhet konfigurerar den användar princip inställningen även om den upptäcker att enheten tillåter flera användarsessioner.

Aktivera den här klient inställningen om du behöver en användar princip i det här scenariot och godkänner eventuell prestanda påverkan.


## <a name="cloud-services"></a>Molntjänster

### <a name="allow-access-to-cloud-distribution-point"></a>Tillåt åtkomst till moln distributions platsen

Ställ in det här alternativet på **Ja** för att klienter ska kunna hämta innehåll från en moln distributions plats. Den här inställningen kräver inte att enheten är Internet-baserad.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registrera automatiskt nya Windows 10-domänanslutna enheter med Azure Active Directory

När du konfigurerar Azure Active Directory att stödja hybrid anslutning, Configuration Manager konfigurerar Windows 10-enheter för den här funktionen. Mer information finns i [så här konfigurerar du hybrid Azure Active Directory anslutna enheter](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Gör det möjligt för klienter att använda en Cloud Management Gateway

Som standard använder alla Internet-centrala klienter alla tillgängliga [moln hanterings-gatewayer](../manage/cmg/plan-cloud-management-gateway.md). Ett exempel på när du ska konfigurera den här inställningen på **Nej** är att omfattnings användningen av tjänsten, till exempel under ett pilot projekt eller att spara kostnader.



## <a name="compliance-settings"></a>Kompatibilitetsinställningar  

### <a name="enable-compliance-evaluation-on-clients"></a>Aktivera kompatibilitetsutvärdering på klienter

Ställ in det här alternativet på **Ja** för att konfigurera de andra inställningarna i den här gruppen.

### <a name="schedule-compliance-evaluation"></a>Schemalägg kompatibilitetsutvärdering

Välj **schema** för att skapa standardschemat för distributioner av konfigurations bas linjer. Det här värdet kan konfigureras för varje bas linje i dialog rutan **distribuera konfigurations bas linje** .  

### <a name="enable-user-data-and-profiles"></a>Aktivera användardata och profiler

Välj **Ja** om du vill distribuera konfigurations objekt för [användar data och profiler](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) .



## <a name="computer-agent"></a>Dator agent  

### <a name="user-notifications-for-required-deployments"></a>Användar meddelanden för nödvändiga distributioner

Mer information om följande tre inställningar finns i [användar meddelanden för nödvändiga distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **Distributions tids gräns större än 24 timmar, Påminn användaren var (timmar)**
- **Distributions tids gräns mindre än 24 timmar, Påminn användaren var (timmar)**
- **Distributions tids gräns mindre än en timme, Påminn användaren var (minuter)**

### <a name="default-application-catalog-website-point"></a>Standardwebbplats för programkatalog

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager använder den här inställningen för att ansluta användare till program katalogen från Software Center. Välj **Ange webbplats** för att ange en server som är värd för program katalogens webbplats punkt. Ange dess NetBIOS-namn eller FQDN, ange automatisk identifiering eller ange en webb adress för anpassade distributioner. I de flesta fall är automatisk identifiering det bästa alternativet.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Lägg till standardwebbplatsen för programkatalogen i Internet Explorers zon för betrodda webbplatser

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Om det här alternativet är **Ja**lägger klienten automatiskt till den aktuella standard webbplats webb adressen för program katalogen i zonen Tillförlitliga platser i Internet Explorer.  

Den här inställningen garanterar att Internet Explorer-inställningen för skyddat läge inte är aktive rad. Om skyddat läge är aktiverat kanske Configuration Manager-klienten inte kan installera program från program katalogen. Zonen Tillförlitliga platser har som standard också stöd för användar inloggning för program katalogen, som kräver Windows-autentisering.  

Om du låter det här alternativet vara **Nej**kanske Configuration Manager-klienter inte kan installera program från program katalogen. En alternativ metod är att konfigurera Internet Explorer-inställningar i en annan zon för den program katalog webb adress som klienterna använder.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Tillåt att Silverlight-program körs med förhöjt förtroende

> [!Important]  
> Klienten installerar inte Silverlight automatiskt.
>
> Från och med version 1806 stöds inte längre **Silverlight-användar upplevelsen** för program katalog webbplatsen. Användarna bör använda det nya Software Center. Mer information finns i [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Den här inställningen måste vara **Ja** för att användarna ska kunna använda program katalogen.  

Om du ändrar den här inställningen börjar den gälla nästa gång användarna läser in webbläsaren eller uppdaterar webbläsarfönstret som är öppna för tillfället.  

Mer information om den här inställningen finns i [certifikat för Microsoft Silverlight 5 och förhöjt förtroende krävs för program katalogen](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Organisationsnamn som visas i Software Center

Skriv det namn som användarna ser i Software Center. Den här informationen hjälper användarna att identifiera programmet som en pålitlig källa. Mer information om prioriteten för den här inställningen finns i [Software Center](../../../apps/plan-design/plan-for-software-center.md#branding-software-center).  

### <a name="use-new-software-center"></a>Använd nya Software Center

Standardinställningen är **Ja**.

När du ställer in det här alternativet på **Ja**använder alla klient datorer Software Center. Software Center visar program vara, program uppdateringar och aktivitetssekvenser som du distribuerar till användare eller enheter.

### <a name="enable-communication-with-health-attestation-service"></a>Aktivera kommunikation med tjänsten hälsoattestering

Ställ in det här alternativet på **Ja** för att Windows 10-enheter ska använda [hälsoattestering](../../servers/manage/health-attestation.md). När du aktiverar den här inställningen är följande inställning också tillgänglig för konfiguration.

### <a name="use-on-premises-health-attestation-service"></a>Använd tjänsten för lokal hälsoattestering

Ställ in det här alternativet på **Ja** för att enheter ska använda en lokal tjänst. Ange till **Nej** för enheter för att använda den Microsoft-molnbaserade tjänsten.  

### <a name="install-permissions"></a>Installationsbehörigheter

Konfigurera hur användare kan installera program vara, program uppdateringar och aktivitetssekvenser:  

- **Alla användare**: användare med valfri behörighet förutom gäst.  

- **Endast administratörer**: användare måste vara medlemmar i den lokala administratörs gruppen.  

- **Endast administratörer och primära användare**: användare måste vara medlemmar i den lokala gruppen Administratörer eller en primär användare av datorn.  

- **Inga användare**: inga användare som är inloggade på en klient dator kan installera program vara, program uppdateringar och aktivitetssekvenser. Nödvändiga distributioner för datorn installeras alltid vid tids gränsen. Användare kan inte installera program vara från Software Center.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Inaktivera PIN-koden för BitLocker vid omstart

Om datorerna kräver PIN-kod för BitLocker, åsidosätter det här alternativet kravet på att ange en PIN-kod när datorn startas om efter en program varu installation.  

- **Always**: Configuration Manager tillfälligt avbryter BitLocker efter att det har installerat program vara som kräver en omstart och har påbörjat en omstart av datorn. Den här inställningen gäller endast för omstart av datorn som initierats av Configuration Manager. Den här inställningen inaktiverar inte kravet att ange BitLocker-PIN-koden när användaren startar om datorn. Kravet på PIN-koden för BitLocker återupptas när Windows har startats.

- **Aldrig**: Configuration Manager pausar inte BitLocker efter att ha installerat program vara som kräver en omstart. I det här scenariot kan program varu installationen inte slutföras förrän användaren anger PIN-koden för att slutföra standard start processen och läsa in Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Ytterligare programvara hanterar distributionen av program och programvaruuppdateringar

Aktivera endast det här alternativet om något av följande villkor gäller:  

- Du använder en leverantörslösning som kräver att den här inställningen är aktiverad.  

- Du använder Configuration Manager Software Development Kit (SDK) för att hantera klient agent meddelanden och installationen av program och program uppdateringar.  

> [!WARNING]  
> - Om du väljer det här alternativet när inget av dessa villkor gäller, installerar inte klienten program uppdateringar och nödvändiga program. Den här inställningen hindrar inte användare från att installera tillgänglig program vara från Software Center, inklusive program, paket och aktivitetssekvenser.  
> -  När du aktiverar den här inställningen inträffar inte popup-meddelanden för ny program vara eller nödvändig program vara på klienter. <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell-körningsprincip

Konfigurera hur Configuration Manager-klienter kan köra Windows PowerShell-skript. Du kan använda dessa skript för identifiering i konfigurations objekt för kompatibilitetsinställningar. Du kan också skicka skripten i en distribution som ett standard skript.  

- **Kringgå**: den Configuration Manager klienten kringgår Windows PowerShell-konfigurationen på klient datorn så att osignerade skript kan köras.  

- **Begränsad**: den Configuration Manager klienten använder den aktuella PowerShell-konfigurationen på klient datorn. Den här konfigurationen bestämmer om osignerade skript kan köras.  

- **Alla signerade**: Configuration Manager klienten kör endast skript om en betrodd utgivare har signerat dem. Den här begränsningen gäller oberoende av den aktuella PowerShell-konfigurationen på klient datorn.  

Det här alternativet kräver minst Windows PowerShell version 2,0. Standardvärdet är **signerat**.  

> [!TIP]  
> Om osignerade skript inte kan köras på grund av den här klient inställningen, rapporterar Configuration Manager det här felet på följande sätt:  
>
> - Arbets ytan **övervakning** i-konsolen visar distributions status fel-ID **0x87D00327**. Det visar också hur **skriptet är signerat**.  
> - Rapporter visar fel typens **identifierings fel**. Rapporter visar sedan antingen felkoden **0x87D00327** och beskrivnings **skriptet är inte signerat**, eller felkoden **0x87D00320** och beskrivningen **som skript värden inte har installerats ännu**. En exempel rapport är: **information om fel i konfigurations objekt i en konfigurations bas linje för en till gång**.  
> - **DcmWmiProvider. log** -filen visar att meddelande **skriptet inte har signerats (fel: 87D00327; Källa: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Visa meddelanden om nya distributioner

Välj **Ja** om du vill visa ett meddelande om distributioner som är tillgängliga i mindre än en vecka. Det här meddelandet visas varje gången klient agenten startar.

### <a name="disable-deadline-randomization"></a>Inaktivera slumpmässig tidsgräns

Efter distributionens tids gräns avgör den här inställningen om klienten använder en aktiverings fördröjning på upp till två timmar för att installera nödvändiga program uppdateringar. Som standard är aktiveringsfördröjningen inaktiverad.  

För VDI-scenarier (Virtual Desktop Infrastructure) kan den här fördröjningen distribuera CPU-bearbetning och data överföring för en värddator med flera virtuella datorer. Även om du inte använder VDI kan många klienter som installerar samma uppdateringar samtidigt minska processor användningen på plats servern negativt. Det här beteendet kan även sakta ned distributions platser och minska den tillgängliga nätverks bandbredden avsevärt.  

Om klienterna måste installera nödvändiga program uppdateringar vid distributionens tids gräns utan fördröjning konfigurerar du den här inställningen till **Ja**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Respitperiod för tillämpning efter distributionens tids gräns (timmar)

Om du vill ge användare mer tid för att installera nödvändiga program eller program uppdaterings distributioner utöver tids gränsen, ställer du in det här alternativet på **Ja**. Den här Grace-perioden är för en dator avstängd under en längre tid och användaren måste installera många program eller uppdaterings distributioner. Den här inställningen är till exempel användbar om en användare returnerar semestern och måste vänta en stund medan klienten installerar förfallna program distributioner.

Ange en respitperiod på 1 till 120 timmar. Använd den här inställningen tillsammans med distributions egenskapen **fördröjd tillämpning av distributionen enligt användar inställningar**. Mer information finns i [distribuera program](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).


## <a name="computer-restart"></a>Omstart av dator

Följande inställningar måste vara kortare i varaktighet än det kortaste underhålls fönstret som tillämpas på datorn:

- **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller omstart av datorn (minuter)**
- **Visa en dialog ruta som användaren inte kan stänga, som visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**


Mer information om underhålls perioder finns i [använda underhålls](../manage/collections/use-maintenance-windows.md)perioder.

- **Ange varaktighet för vilo läge för omstart av datorn (minuter) för omstart** (från och med version 1906)<!--3976435-->
  - Standardvärdet är 240 minuter.
  - Varaktighet svärdet för vilo läge ska vara mindre än det tillfälliga meddelande svärdet minus värdet för meddelandet som användaren inte kan stänga.
  - Mer information finns i [meddelanden om omstart av enhet](device-restart-notifications.md).

**När en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande**<!--3555947-->: Från och med version 1902 kan du konfigurera den här inställningen till **Ja** för att ändra användar upplevelsen till mer påträngande. Den här inställningen gäller för alla distributioner av program, aktivitetssekvenser och program uppdateringar. Mer information finns i [Planera för Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> I Configuration Manager 1902, under vissa omständigheter, ersätter dialog rutan inte popup-meddelanden. Lös problemet genom att installera Samlad [uppdatering för Configuration Manager version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->


## <a name="delivery-optimization"></a>Leveransoptimering 

<!-- 1324696 -->
Du använder Configuration Manager gränser grupper för att definiera och reglera innehålls distribution i företags nätverket och på fjärranslutna kontor. [Windows-leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) är en molnbaserad, peer-to-peer-teknik för att dela innehåll mellan Windows 10-enheter. Konfigurera leverans optimeringen så att den använder dina gränser när du delar innehåll mellan peer-datorer.

> [!Note]
> - Leverans optimering är endast tillgänglig på Windows 10-klienter.
> - Internet åtkomst till moln tjänsten för leverans optimering är ett krav för att använda peer-to-peer-funktioner. Information om vilka Internet-slutpunkter som behövs finns i [vanliga frågor och svar om leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** [klienten](#allow-clients-to-download-delta-content-when-available) är aktive rad. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Använd Configuration Manager gränser grupper för grupp-ID för leverans optimering

Välj **Ja** om du vill använda gränserna för den begränsade gruppen som ID för leverans optimerings grupp på klienten. När klienten kommunicerar med moln tjänsten för leverans optimering används den här identifieraren för att hitta peer-datorer med det önskade innehållet.

> [!Note]
> Microsoft rekommenderar att klienten konfigurerar den här inställningen via lokal princip i stället för grup princip. Detta gör att gränserna för grupp identifieraren kan anges som leverans optimerings grupp identifierare på klienten. Mer information finns i avsnittet om [leverans optimering](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Aktivera enheter som hanteras av Configuration Manager att använda Microsoft-anslutna cache-servrar för innehålls hämtning

<!--3555764-->
Välj **Ja** om du vill tillåta att klienter laddar ned innehåll från en lokal distributions plats som du aktiverar som en Microsoft-ansluten cache-server. Mer information finns [i Microsoft Connected cache i Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Slutpunktsskydd

> [!Tip]
> Förutom följande information hittar du information om hur du använder Endpoint Protection klient inställningar i [exempel scenariot: använda Endpoint Protection för att skydda datorer mot skadlig kod](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Hantera Endpoint Protection-klient på klient datorer

Välj **Ja** om du vill hantera befintliga Endpoint Protection-och Windows Defender-klienter på datorer i hierarkin.  

Välj det här alternativet om du redan har installerat Endpoint Protection-klienten och vill hantera den med Configuration Manager. Den här separata installationen innehåller en skript process som använder ett Configuration Manager-program eller paket och program. Windows 10-enheter behöver inte ha Endpoint Protection-agenten installerad. Dessa enheter behöver dock fortfarande **hantera Endpoint Protection-klient på klient datorer** som är aktiverade. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Installera Endpoint Protection-klient på klientdatorer

Välj **Ja** om du vill installera och Aktivera Endpoint Protection-klienten på klient datorer som inte redan kör-klienten. Windows 10-klienter behöver inte ha Endpoint Protection-agenten installerad.  

> [!NOTE]  
> Om Endpoint Protection-klienten redan är installerad väljer du **Nej** för att inte avinstallera Endpoint Protection klienten. Om du vill avinstallera Endpoint Protection-klienten ställer du in klient inställningen **hantera Endpoint Protection klient på klient datorer** på **Nej**. Distribuera sedan ett paket och program för att avinstallera Endpoint Protection-klienten.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Tillåt Endpoint Protection klient installation och startar om utanför underhålls fönster. Underhålls perioder måste vara minst 30 minuter långt för klient installation

Ställ in det här alternativet på **Ja** om du vill åsidosätta vanliga installations beteenden med underhålls fönster. Den här inställningen uppfyller affärs kraven för system underhåll av säkerhets synpunkt.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>För Windows Embedded-enheter med Skriv filter genomför du Endpoint Protection klient installation (kräver omstart)

Välj **Ja** om du vill inaktivera Skriv filtret på Windows Embedded-enheten och starta om enheten. Den här åtgärden utför installationen på enheten.  

Om du väljer **Nej**installeras klienten på ett tillfälligt överlägg som rensas när enheten startas om. I det här scenariot installeras Endpoint Protection-klienten inte fullständigt förrän en annan installation genomför ändringar på enheten. Den här konfigurationen är standard.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Ignorera eventuella nödvändiga omstarter av datorn efter att Endpoint Protection-klienten har installerats

Välj **Ja** om du vill förhindra att datorn startas om när den Endpoint Protection klienten har installerats.  

> [!IMPORTANT]  
> Om den Endpoint Protection klienten kräver en omstart av datorn och den här inställningen är **Nej**startas datorn om oavsett eventuella konfigurerade underhålls fönster.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Tids period som användare kan skjuta upp en begärd omstart för att slutföra Endpoint Protection installationen (timmar)

Om en omstart krävs efter att den Endpoint Protection klienten har installerats, anger den här inställningen antalet timmar som användarna kan skjuta upp den begärda omstarten. Den här inställningen kräver att inställningen för **ignorera eventuella nödvändiga omstarter av datorn efter att Endpoint Protection-klienten har installerats** **.**  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Inaktivera alternativa källor (till exempel Microsoft Windows Update, Microsoft Windows Server Update Services eller UNC-resurser) för den inledande definitions uppdateringen på klient datorer

Välj **Ja** om du vill att Configuration Manager endast ska installera den första definitions uppdateringen på klient datorer. Den här inställningen kan vara till hjälp för att undvika onödiga nätverks anslutningar och minska nätverks bandbredden under den inledande installationen av definitions uppdateringen.  



## <a name="enrollment"></a>Registrering

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Avsöknings intervall för äldre mobila enhets klienter

Välj **ange intervall** för att ange hur lång tid i minuter eller timmar som äldre mobila enheter avsöker för principen. Dessa enheter innehåller plattformar som Windows CE, Mac OS X och UNIX eller Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Avsöknings intervall för moderna enheter (minuter)

Ange antalet minuter som moderna enheter söker efter princip. Den här inställningen gäller för Windows 10-enheter som hanteras via lokal hantering av mobila enheter.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Tillåt att användare registrerar mobila enheter och Mac-datorer

Om du vill aktivera användarbaserad registrering av äldre enheter ställer du in det här alternativet på **Ja**och konfigurerar sedan följande inställning:

- **Registrerings profil**: Välj **Ange profil** för att skapa eller välja en registrerings profil. Mer information finns i [Konfigurera klient inställningar för registrering](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Tillåt att användare registrerar moderna enheter

Om du vill aktivera användarbaserad registrering av moderna enheter ställer du in det här alternativet på **Ja**och konfigurerar sedan följande inställning:

- **Registrerings profil för modern enhet**: Välj **Ange profil** för att skapa eller välja en registrerings profil. Mer information finns i [skapa en registrerings profil som gör det möjligt för användare att registrera moderna enheter](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Maskinvaruinventering  

### <a name="enable-hardware-inventory-on-clients"></a>Aktivera maskin varu inventering på klienter

Som standard är den här inställningen **Ja**. Mer information finns i [Introduktion till maskin varu inventering](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Schema för maskin varu inventering

Välj **schema** för att justera hur ofta klienterna kör maskin varu inventerings cykeln. Som standard sker den här cykeln var sjunde dag.

### <a name="maximum-random-delay-minutes"></a>Maximal slumpmässig fördröjning (minuter)

Ange det maximala antalet minuter som den Configuration Manager klienten ska Slumpa maskin varu inventerings cykeln från det definierade schemat. Den här slumpmässigheten för alla klienter hjälper till att belastningsutjämna lager bearbetning på plats servern. Du kan ange ett värde mellan 0 och 480 minuter. Som standard är det här värdet inställt på 240 minuter (4 timmar).

### <a name="maximum-custom-mif-file-size-kb"></a>Maximal storlek på anpassad MIF-fil (kB)

Ange den maximala storlek, i kilobyte (KB), som tillåts för varje MIF-fil (Management information format) som klienten samlar in under en maskin varu inventerings cykel. Configuration Manager maskin varu inventerings agenten bearbetar inte några anpassade MIF-filer som överskrider den här storleken. Du kan ange en storlek på 1 KB till 5 120 KB. Som standard är det här värdet inställt på 250 kB. Den här inställningen påverkar inte storleken på den vanliga data filen för maskin varu inventering.  

> [!NOTE]  
> Den här inställningen är endast tillgänglig i standard klient inställningarna.  

### <a name="hardware-inventory-classes"></a>Maskinvarulagerklasser

Välj **Ange klasser** om du vill utöka den maskin varu information som du samlar in från klienter utan att redigera filen sms_def. MOF manuellt. Mer information finns i [så här konfigurerar du maskin varu inventering](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Samla in MIF-filer

Använd den här inställningen för att ange om du vill samla in MIF-filer från Configuration Manager klienter under maskin varu inventeringen.  

För att en MIF-fil ska kunna samlas in av maskin varu inventeringen måste den finnas på rätt plats på klient datorn. Som standard finns filerna i följande sökvägar:  

- **IDMIF-filer** ska finnas i mappen Windows\System32\CCM\Inventory\Idmif.

- **NOIDMIF-filer** ska finnas i mappen windows\system32\ccm\inventory\noidmif.

> [!NOTE]  
> Den här inställningen är endast tillgänglig i standard klient inställningarna.



## <a name="metered-internet-connections"></a>Avgiftsbelagda Internet anslutningar  

Hantera hur Windows 8-datorer och senare datorer använder avgiftsbelagda Internet anslutningar för att kommunicera med Configuration Manager. Internet leverantörer debiteras ibland av den mängd data som du skickar och tar emot när du använder en avgiftsbelagd Internet-anslutning.  

> [!NOTE]  
> Den konfigurerade klient inställningen tillämpas inte i följande scenarier:  
>
> - Om datorn är på en central data anslutning utför Configuration Manager-klienten inga aktiviteter som kräver att data överförs till Configuration Manager platser.  
> - Om nätverks anslutnings egenskaperna för Windows har kon figurer ATS som icke-avgiftsbelagda fungerar Configuration Manager-klienten som om anslutningen inte är avgiftsbelagd och överför sedan data till platsen.  

### <a name="client-communication-on-metered-internet-connections"></a>Klient kommunikation i Internet anslutningar med datapriser

Välj något av följande alternativ för den här inställningen:  

- **Tillåt**: all klient kommunikation tillåts via den avgiftsbelagda Internet anslutningen, om inte klient enheten använder en data anslutning med nätverks växling.  

- **Gräns**: endast följande klient kommunikation tillåts via den avgiftsbelagda Internet anslutningen:  

    - Återställning av klientprincip  

    - Klienttillståndsmeddelanden som ska skickas till platsen  

    - Program varu installations förfrågningar från Software Center  

    - Nödvändiga distributioner (om tidsgränsen för installationen uppnås)  

    > [!IMPORTANT]  
    > Klienten tillåter alltid programinstallationer från Software Center, oavsett inställningarna för avgiftsbelagd Internet anslutning.  

    Om klienten når data överförings gränsen för den avgiftsbelagda Internet anslutningen försöker klienten inte längre kommunicera med Configuration Manager-platser.  

- **Blockera**: Configuration Manager klienten försöker inte kommunicera med Configuration Manager platser när den är på en avgiftsbelagd Internet-anslutning. Det här alternativet är standardinställningen.  



## <a name="power-management"></a>Energisparfunktioner  

### <a name="allow-power-management-of-devices"></a>Tillåt energispar funktioner för enheter

Ställ in det här alternativet på **Ja** för att aktivera energispar funktioner på klienter. Mer information finns i [Introduktion till energispar funktioner](../manage/power/introduction-to-power-management.md).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Tillåt att användare undantar sina enheter från energisparfunktioner

Välj **Ja** om du vill låta användare av Software Center undanta sina datorer från eventuella konfigurerade inställningar för energispar funktioner.  

### <a name="allow-network-wake-up"></a>Tillåt nätverks aktivering

Tillagt i 1810. När inställningen är **aktive**rad konfigurerar energi inställningarna på nätverkskortet så att nätverkskortet kan aktivera enheten. När inställningen är **inaktive**rad konfigureras energi inställningarna på nätverkskortet så att det inte tillåter att nätverkskortet aktiverar enheten.

### <a name="enable-wake-up-proxy"></a>Aktivera aktiveringsproxy

Ange **Ja** för att komplettera platsens Wake on LAN inställning när den har kon figurer ATS för unicast-paket.  

Mer information om Wake-up proxy finns i [Planera aktivering av klienter](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Aktivera inte Wake-up-proxy i ett produktions nätverk utan att först förstå hur det fungerar och utvärdera det i en test miljö.  

Konfigurera sedan följande ytterligare inställningar efter behov:

- **Port nummer för Väcknings port (UDP)**: det port nummer som klienter använder för att skicka aktiverings paket till datorer i vilo läge. Behåll standard porten 25536 eller ändra värdet till önskat värde.  

- **Wake on LAN port nummer (UDP)**: Behåll standardvärdet 9, om du inte har ändrat port numret för Wake on LAN (UDP) på fliken **portar** i plats **egenskaperna**.  

    > [!IMPORTANT]  
    > Numret måste stämma med numret i **Egenskaper**för platsen. Om du ändrar det här numret på en plats uppdateras det inte automatiskt på den andra platsen.  

- **Undantag i Windows Defender-brandväggen för Wake-up-proxy**: Configuration Manager klienten konfigurerar automatiskt port numret för Wake-up-proxy på enheter som kör Windows Defender-brandväggen. Välj **Konfigurera** för att ange önskade brand Väggs profiler.  

    Om klienterna kör en annan brand vägg konfigurerar du den manuellt för att tillåta **port numret för Wake-up-proxy (UDP)**.  

- **IPv6-prefix om det krävs för DirectAccess eller andra mellanliggande nätverks enheter. Använd ett kommatecken om du vill ange flera poster**: ange nödvändiga IPv6-prefix för aktivering av proxy för att fungera i nätverket.



## <a name="remote-tools"></a>Fjärrverktyg  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Aktivera fjärr styrning på klienter och undantags profiler för brand väggen

Välj **Konfigurera** om du vill aktivera funktionen Configuration Manager fjärr styrning. Du kan också konfigurera brand Väggs inställningar för att tillåta fjärr styrning att fungera på klient datorer.  

Som standard är fjärrstyrning inaktiverad.  

> [!IMPORTANT]  
> Om du inte konfigurerar brand Väggs inställningar kanske fjärr styrning inte fungerar korrekt.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Användare kan ändra princip- eller meddelandeinställningar i Software Center

Välj om användarna ska kunna ändra alternativ för fjärr styrning inifrån Software Center.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Tillåt fjärrstyrning av en obevakad dator

Välj om en administratör ska kunna använda fjärr styrning för att komma åt en klient dator som är utloggad eller låst. Endast en inloggad och olåst dator kan fjärrstyras när den här inställningen är inaktive rad.  

### <a name="prompt-user-for-remote-control-permission"></a>Fråga användaren om Fjärrstyrning-behörighet

Välj om klient datorn ska visa ett meddelande som ber om användarens behörighet innan en fjärrstyrningssession tillåts.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Uppmana användaren att ange behörighet för att överföra innehåll från delat Urklipp

Innan du överför innehåll från det delade Urklippet i en fjärrstyrningssession kan användarna tillåta att de godkänner eller nekar fil överföringar. Användare behöver bara bevilja behörighet en gång per session. Visnings programmet kan inte ge sig själva behörighet att överföra filen.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Bevilja fjärrstyrningsbehörigheten till lokal administratörsgrupp

Välj om lokala administratörer på den server som initierar fjärr styrnings anslutningen ska kunna upprätta fjärr styrnings anslutningar till klient datorer.  

### <a name="access-level-allowed"></a>Tillåten åtkomstnivå

Ange nivån för fjärr styrnings åtkomst som ska tillåtas. Välj bland följande inställningar:  

- **Ingen åtkomst**
- **Visa endast**
- **Fullständig behörighet**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Tillåtna visnings program för fjärr styrning och Fjärrhjälp

Välj **Ange visnings program** för att ange namnen på de Windows-användare som kan upprätta fjärr styrnings-sessioner till klient datorer.  

### <a name="show-session-notification-icon-on-taskbar"></a>Visa sessionsmeddelandeikonen i Aktivitetsfältet

Konfigurera den här inställningen på **Ja** om du vill visa en ikon på klientens aktivitets fält i Windows för att ange en aktiv fjärrstyrningssession.  

### <a name="show-session-connection-bar"></a>Visa sessionsanslutningsfältet

Ställ in det här alternativet på **Ja** för att Visa anslutnings fältet med hög synbarhet på klienter för att ange en aktiv fjärrstyrningssession.  

### <a name="play-a-sound-on-client"></a>Spela upp ett ljud på klienten

Ange det här alternativet om du vill använda ljud för att indikera när en fjärrstyrningssession är aktiv på en klient dator. Välj något av följande alternativ:

- **Inget ljud**
- **Början och slutet av sessionen** (standard)
- **Upprepade gånger under sessionen**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Hantera oönskade Fjärrhjälp-inställningar

Konfigurera den här inställningen till **Ja** för att låta Configuration Manager hantera oönskade Fjärrhjälp-sessioner.  

I en oönskad fjärrhjälpsession begärdes inte användaren på klient datorn att hjälpa till att initiera sessionen.  

### <a name="manage-solicited-remote-assistance-settings"></a>Hantera önskade Fjärrhjälp-inställningar

Ställ in det här alternativet på **Ja** för att låta Configuration Manager hantera efterfrågade Fjärrhjälp-sessioner.  

I en efterfrågad fjärrhjälpssession skickade användaren på klient datorn en begäran till administratören om Fjärrhjälp.  

### <a name="level-of-access-for-remote-assistance"></a>Åtkomstnivå för Fjärrhjälp

Välj den åtkomst nivå som ska tilldelas till Fjärrhjälp-sessioner som initieras i Configuration Manager-konsolen. Välj något av följande alternativ:

- **Ingen** (standardvärde)
- **Fjärrvisning**
- **Fullständig behörighet**

> [!NOTE]  
> Användaren vid fjärrdatorn måste alltid ge tillåtelse för att en Fjärrhjälp-session ska kunna genomföras.  

### <a name="manage-remote-desktop-settings"></a>Hantera Fjärrskrivbord-inställningar

Ställ in det här alternativet på **Ja** för att låta Configuration Manager Hantera fjärrskrivbord-sessioner för datorer.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Tillåt betrodda visningsprogram att ansluta via Anslutning till fjärrskrivbord

Ställ in det här alternativet på **Ja** om du vill lägga till användare som anges i listan över tillåtna visnings program i den lokala användar gruppen fjärr skrivbord på klienter.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Begär autentisering på nätverksnivå för datorer som kör Windows Vista eller senare versioner

Ställ in det här alternativet på **Ja** om du vill använda autentisering på nätverks nivå (NLA) för att upprätta fjärr skrivbords anslutningar till klient datorer. NLA kräver initialt färre resurser på fjärrdatorn, eftersom användarautentisering slutförs innan en fjärr skrivbords anslutning upprättas. Att använda NLA är en säkrare konfiguration. NLA skyddar datorn från skadliga användare eller program vara och minskar risken från DOS-attacker (Denial-of-Service).  



## <a name="software-center"></a>Software Center

### <a name="select-these-new-settings-to-specify-company-information"></a>Välj de här nya inställningarna för att ange företags information

Ställ in det här alternativet på **Ja**och ange sedan följande inställningar för att anpassa Software Center för din organisation:

- **Företags namn**: Ange det organisations namn som användarna ser i Software Center.  

- **Färg schema för Software Center**: Klicka på **Välj färg** för att definiera den primära färg som används av Software Center.  

- **Välj en logo typ för Software Center**: Klicka på **Bläddra** och välj en bild som ska visas i Software Center. Logo typen måste vara en JPEG, PNG eller BMP med 400 x 100 pixlar, med en maximal storlek på 750 KB. Logo typ filens namn får inte innehålla blank steg.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a>Dölj ej godkända program i Software Center

När du aktiverar det här alternativet döljs användar tillgängliga program som kräver godkännande i Software Center.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a>Dölj installerade program i Software Center

När du aktiverar det här alternativet visas inte längre program som redan är installerade på fliken program. Det här alternativet anges som standard när du installerar eller uppgraderar till Configuration Manager 1802. Installerade program är fortfarande tillgängliga för granskning på fliken installations status. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a>Dölj Programkatalog länk i Software Center

Ange synlighet för länken till program katalogens webbplats i Software Center. När det här alternativet är inställt kan användarna inte se länken till program katalogens webbplats i noden installations status i Software Center. <!--1358214-->

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  

### <a name="software-center-tab-visibility"></a>Fliken synlighet i Software Center

#### <a name="starting-in-version-1906"></a>Från och med version 1906
<!--4063773-->

Välj vilka flikar som ska visas i Software Center. Använd knappen **Lägg** till för att flytta en flik till **synliga flikar**. Använd knappen **ta bort** för att flytta den till listan med **dolda flikar** . Ordna flikarna med knapparna **Flytta upp** eller **Flytta ned** . 

Tillgängliga flikar:
- **Program**
- **Uppdateringar**
- **Operativ system**
- **Installations status**
- **Enhetsefterlevnad**
- **Alternativ**
- Lägg till upp till fem anpassade flikar genom att klicka på knappen **Lägg till flik** .
  - Ange **flikens namn** och **innehålls-URL** för din anpassade flik.
  - Klicka på **fliken ta bort** om du vill ta bort en anpassad flik.  

  >[!Important]  
  > - Vissa webbplats funktioner kanske inte fungerar när du använder den som en anpassad flik i Software Center. Se till att testa resultaten innan du distribuerar det till klienter. <!--519659-->
  > - Ange endast betrodda eller intranäts webbplats adresser när du lägger till en anpassad flik.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Version 1902 och tidigare

Konfigurera de ytterligare inställningarna i den här gruppen till **Ja** så att följande flikar visas i Software Center:

- **Program**
- **Uppdateringar**
- **Operativ system**
- **Installations status**
- **Enhetsefterlevnad**
- **Alternativ**
- **Ange en anpassad flik för Software Center** <!--1358132-->
    - **Fliknamn**
    - **Innehålls-URL**

    >[!Important]  
    > Vissa webbplats funktioner kanske inte fungerar när du använder den som en anpassad flik i Software Center. Se till att testa resultaten innan du distribuerar det till klienter. <!--519659-->
    >
    > Ange endast betrodda eller intranäts webbplats adresser när du lägger till en anpassad flik.<!--SCCMDocs issue 1575-->

Om din organisation till exempel inte använder efterlevnadsprinciper och du vill dölja fliken för enhets efterlevnad i Software Center, anger du fliken för att **Aktivera enhets** efterlevnad på **Nej**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a>Konfigurera standardvyer i Software Center
<!--3612112-->
*(Lanseras i version 1902)*

- Konfigurera **standard program filtret** som antingen **alla** eller endast **nödvändiga** program.  

  - I Software Center används alltid standardvärdet. Användare kan ändra det här filtret, men Software Center behåller inte sina preferenser.  

- Ange **standard visningen** för vyn som antingen **panel** eller **listvy**. 

  - Om en användare ändrar den här konfigurationen, behåller Software Center användarnas preferenser i framtiden. 


## <a name="software-deployment"></a>Programvarudistribution  

### <a name="schedule-re-evaluation-for-deployments"></a>Schemalägg omvärdering för distributioner

Konfigurera ett schema för när Configuration Manager utvärderar krav reglerna för alla distributioner. Standardvärdet är var sjunde dag.  

> [!IMPORTANT]  
> Den här inställningen är mer invasiv till den lokala klienten än den är till nätverket eller plats servern. Ett mer aggressivt utvärderings schema påverkar nätverkets och klient datorernas prestanda negativt. Microsoft rekommenderar inte att du anger ett lägre värde än standardvärdet. Om du ändrar det här värdet övervakar du prestanda noga.  

Starta den här åtgärden från en klient på följande sätt: gå till fliken **åtgärder** i **Configuration Manager** kontroll panelen och välj **utvärderings cykel för program distribution**.  



## <a name="software-inventory"></a>Programvaruinventering  

### <a name="enable-software-inventory-on-clients"></a>Aktivera program varu inventering på klienter

Det här alternativet är inställt på **Ja** som standard. Mer information finns i [Introduktion till program varu inventering](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Schemalägg program varu inventering och fil insamling

Välj **schema** för att justera den frekvens som klienterna kör program varu inventeringen och fil insamlings cykler. Som standard sker den här cykeln var sjunde dag.

### <a name="inventory-reporting-detail"></a>Information om inventeringsrapportering

Ange en av följande nivåer av fil information som ska inventeras:

- **Endast fil**
- **Endast produkt**
- **Fullständig information** (standard)

### <a name="inventory-these-file-types"></a>Inventera de här filtyperna

Om du vill ange de typer av filer som ska inventeras väljer du **Ange typer**och konfigurerar sedan följande alternativ:  

> [!NOTE]  
> Om flera anpassade klient inställningar används på en dator slås inventeringen som varje inställning returnerar samman.  

- Välj **nytt** om du vill lägga till en ny filtyp i lagret. Ange följande information i dialog rutan **Egenskaper för inventerade filer** :  

    - **Namn**: Ange ett namn för den fil som du vill inventera. Använd en asterisk (`*`) som jokertecken för att representera valfri text sträng och ett frågetecken (`?`) för att representera ett enskilt tecken. Om du till exempel vill inventera alla filer med fil namns tillägget. doc anger du fil namnet `*.doc`.  

    - **Plats**: Välj **Ange** för att öppna dialog rutan **Sök vägs egenskaper** . Konfigurera program varu inventering för att söka igenom alla klient hård diskar efter den angivna filen, söka i en angiven sökväg `C:\Folder`(till exempel) eller söka efter en angiven variabel (t `%windir%`. ex.). Du kan också söka i alla undermappar under den angivna sökvägen.  

    - **Exkludera krypterade och komprimerade filer**: när du väljer det här alternativet inventeras inte komprimerade eller krypterade filer.  

    - **Undanta filer i Windows-mappen**: när du väljer det här alternativet inventeras inga filer i Windows-mappen och dess undermappar.  

    Välj **OK** för att stänga dialog rutan **Egenskaper för inventerade filer** . Lägg till alla filer som du vill inventera och välj sedan **OK** för att stänga dialog rutan **Konfigurera klient inställning** .  

### <a name="collect-files"></a>Samla in filer

Om du vill samla in filer från klient datorer väljer du **Ange filer**och konfigurerar sedan följande inställningar:  

> [!NOTE]  
> Om flera anpassade klient inställningar används på en dator slås inventeringen som varje inställning returnerar samman.  

- I dialog rutan **Konfigurera klient inställning** väljer du **ny** för att lägga till en fil som ska samlas in.  

- Ange följande information i dialogrutan **Insamlade filegenskaper** :  

    - **Namn**: Ange ett namn för den fil som du vill samla in. Använd en asterisk (`*`) som jokertecken för att representera valfri text sträng och ett frågetecken (`?`) för att representera ett enskilt tecken.  

    - **Plats**: Välj **Ange** för att öppna dialog rutan **Sök vägs egenskaper** . Konfigurera program varu inventering för att söka igenom alla klient hård diskar efter den fil som du vill samla in, söka i en angiven sökväg `C:\Folder`(till exempel) eller söka efter en angiven variabel (t `%windir%`. ex.). Du kan också söka i alla undermappar under den angivna sökvägen.  

    - **Exkludera krypterade och komprimerade filer**: när du väljer det här alternativet samlas komprimerade eller krypterade filer inte in.  

    - **Stoppa fil insamling när den totala storleken på filerna överskrider (KB)**: Ange fil storleken i KILOBYTE (KB), efter vilken klienten slutar att samla in de angivna filerna.  

    > [!NOTE]  
    > Plats servern samlar in de fem senast ändrade versionerna av insamlade filer och lagrar dem i `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` katalogen. Om en fil inte har ändrats sedan den senaste program varu inventerings cykeln samlas filen inte in igen.  
    >
    > Program varu inventering samlar inte in filer som är större än 20 MB.  
    >
    > Värdet **maximal storlek för alla insamlade filer (KB)** i dialog rutan **Konfigurera klient inställning** visar den maximala storleken för alla insamlade filer. När den här storleken uppnås stoppas fil insamlingen. Alla filer som redan samlats in behålls och skickas till platsservern.  

    > [!IMPORTANT]
    > Om du konfigurerar program varu inventering för att samla in många stora filer kan den här konfigurationen påverka nätverkets och plats serverns prestanda negativt.  

    Information om hur du visar insamlade filer finns i [så här använder Resursläsaren för att visa program varu inventering](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Välj **OK** för att stänga dialog rutan **insamlade fil egenskaper** . Lägg till alla filer som du vill samla in och välj sedan **OK** för att stänga dialog rutan **Konfigurera klient inställning** .  

### <a name="set-names"></a>Ange namn

Program varu inventerings agenten hämtar tillverkare och produkt namn från fil huvud information. Dessa namn är inte alltid standardiserade i fil huvuds informationen. När du visar program varu inventering i Resursläsaren kan olika versioner av samma tillverkare eller produkt namn visas. Om du vill standardisera dessa visnings namn väljer du **Ange namn**och konfigurerar sedan följande inställningar:  

- **Typ av namn**: program varu inventering samlar in information om både tillverkare och produkter. Välj om du vill konfigurera visnings namn för en **tillverkare** eller en **produkt**.  

- **Visnings namn**: Ange det visnings namn som du vill använda i stället för namnen i listan **inventerade namn** . Om du vill ange ett nytt visnings namn väljer du **nytt**.  

- **Inventerade namn**: Välj **nytt**om du vill lägga till ett inventerat namn. Namnet ersätts i program varu inventeringen med det namn som valts i listan **visnings namn** . Du kan lägga till flera namn som ska ersättas.  



## <a name="software-metering"></a>Avläsning av programvara

### <a name="enable-software-metering-on-clients"></a>Aktivera Avläsning av program vara på klienter

Den här inställningen är inställd på **Ja** som standard. Mer information finns i [avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Schemalägg data insamling

Välj **schema** för att justera den frekvens som klienterna kör program mätnings cykeln. Som standard sker den här cykeln var sjunde dag.



## <a name="software-updates"></a>Programuppdateringar  

### <a name="enable-software-updates-on-clients"></a>Aktivera programvaruuppdateringar på klienter

Använd den här inställningen för att aktivera program uppdateringar på Configuration Manager klienter. När du inaktiverar den här inställningen tar Configuration Manager bort befintliga distributions principer från klienter. Om du markerar den här inställningen igen laddar klienten ned den aktuella distributionsprincipen.  

> [!IMPORTANT]  
> När du inaktiverar den här inställningen kommer efterlevnadsprinciper som är beroende av program uppdateringar inte längre att fungera.  

### <a name="software-update-scan-schedule"></a>Schema för sökning efter programvaruuppdateringar

Välj **schema** för att ange hur ofta klienten ska initiera en sökning efter kompatibilitetskontroll. Den här sökningen bestämmer status för program uppdateringar på klienten (till exempel obligatorisk eller installerad). Mer information om kompatibilitetsutvärdering finns i [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Som standard använder den här genomsökningen ett enkelt schema för att initiera var sjunde dag. Du kan skapa ett anpassat schema. Du kan ange en exakt start dag och tid, använda UTC (Universal Coordinated Time) eller lokal tid och konfigurera det återkommande intervallet för en angiven veckodag.  

> [!NOTE]  
> Om du anger ett intervall på mindre än en dag, Configuration Manager automatiskt en dag som standard.  

> [!WARNING]  
> Den faktiska start tiden på klient datorerna är start tiden plus en slumpmässig mängd tid, upp till två timmar. Den här slumpmässigheten förhindrar att klient datorer initierar genomsökningen och samtidigt ansluter till den aktiva program uppdaterings platsen.  

### <a name="schedule-deployment-re-evaluation"></a>Schemalägg distributionsomvärdering

Välj **schema** för att konfigurera hur ofta klient agenten för program uppdateringar ska utvärdera program uppdateringar för installations status på Configuration Manager klient datorer. När tidigare installerade program uppdateringar inte längre hittas på klienter, men som fortfarande krävs, installerar klienten om program uppdateringarna.

Justera schemat baserat på företags princip för program uppdaterings efterlevnad och om användarna ska kunna avinstallera program uppdateringar. Varje omvärderings cykel för distribution ger nätverks-och klient dator processor aktivitet. Som standard använder den här inställningen ett enkelt schema för att initiera omprövningen av distributionen var sjunde dag.  

> [!NOTE]  
> Om du anger ett intervall på mindre än en dag, Configuration Manager automatiskt en dag som standard.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Installera alla andra program uppdaterings distributioner med tids gräns inom en angiven tids period när en tids gräns för distribution av program uppdatering har uppnåtts

Ställ in det här alternativet på **Ja** om du vill installera alla program uppdateringar från nödvändiga distributioner med tids gränser som inträffar inom en angiven tids period. När en nödvändig program uppdaterings distribution når en tids gräns initierar klienten installationen av program uppdateringarna i distributionen. Den här inställningen avgör om program uppdateringar ska installeras från andra nödvändiga distributioner som har en tids gräns inom den angivna tiden.  

Använd den här inställningen för att påskynda installationen av nödvändiga program uppdateringar. Den här inställningen har också möjlighet att öka klient säkerheten, minska meddelanden till användaren och minska omstarter av klienter. Som standard är inställningen **Nej**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Tidsperiod när alla väntande distributioner med tidsgräns under den här tiden också installeras

Använd den här inställningen för att ange tids perioden för föregående inställning. Du kan ange ett värde mellan 1 och 23 timmar och mellan 1 och 365 dagar. Som standard är den här inställningen konfigurerad i sju dagar.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Tillåt att klienter laddar ned delta innehåll när det är tillgängligt

*(Lanseras i version 1902)*

Ställ in det här alternativet på **Ja** om du vill tillåta klienter att använda delta-innehållsfiler. Med den här inställningen kan Windows Update Agent på enheten avgöra vilket innehåll som behövs och selektivt Ladda ned det. 

- Innan du aktiverar den här klient inställningen bör du se till att leverans optimeringen är korrekt konfigurerad för din miljö. Mer information finns i [Windows-leverans optimering](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) och [klient inställning för leverans optimering](#delivery-optimization).
 - Den här klient inställningen ersätter **Aktivera installation av Express-installationsfiler på klienter**. Ställ in det här alternativet på **Ja** så att klienterna kan använda installationsfiler för Express. Mer information finns i [Hantera snabb installationsfiler för Windows 10-uppdateringar](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - Från och med Configuration Manager version 1910, när det här alternativet är inställt, används delta hämtning för alla Windows Update-installationsfiler, inte bara Express-installationsfiler.
    - När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** klienten är aktive rad. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Port som klienter använder för att ta emot begär Anden om delta innehåll

*(Lanseras i version 1902)*

Den här inställningen konfigurerar den lokala porten för HTTP-lyssnaren att ladda ned delta innehåll. Den ställs in på 8005 som standard. Du behöver inte öppna den här porten i klient brand väggen. 

> [!NOTE]
>Den här klient inställningen ersätter den **port som används för att ladda ned innehåll för installationsfiler för Express installation**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Aktivera hantering av klient agenten för Office 365

När du ställer in det här alternativet på **Ja**, aktive ras konfigurationen av installations inställningar för Office 365. Du kan också hämta filer från Office Content Delivery Networks (CDN) och distribuera filerna som ett program i Configuration Manager. Mer information finns i [Hantera Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a>Aktivera installation av program uppdateringar i underhålls fönstret för alla distributioner när underhålls fönstret program uppdatering är tillgängligt

Från och med version 1810, när du ställer in det här alternativet på **Ja** och klienten har minst en definierad underhålls period för program uppdatering, kommer program uppdateringar att installeras under underhålls perioden "alla distributioner".

Som standard är inställningen **Nej**. Det här värdet använder samma beteende som innan: om båda typerna finns ignoreras fönstret. <!--2839307-->

> [!NOTE]
> Den här inställningen gäller även för de underhålls fönster som du konfigurerar för att tillämpa på **aktivitetssekvenser**.<!-- SCCMDocs-pr #4596 -->
>
> Om klienten endast har ett fönster för **alla distributioner** , installerar det fortfarande program uppdateringar eller aktivitetssekvenser i fönstret.

#### <a name="maintenance-window-example"></a>Exempel på underhålls period

Du kan till exempel konfigurera följande underhålls fönster:

- **Alla distributioner**: 02:00-04:00
- **Program uppdateringar**: 04:00-06:00

Som standard installerar klienten bara program uppdateringar i den andra underhålls perioden. Underhålls perioden ignoreras för alla distributioner i det här scenariot. När du ändrar den här inställningen till **Ja**installerar klienten program uppdateringar mellan 02:00-06:00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a>Ange tråd prioritet för funktions uppdateringar

<!--3734525-->
Från och med Configuration Manager version 1902 kan du justera prioriteten med vilken Windows 10-version 1709 eller senare klienter installerar en funktions uppdatering via [Windows 10-Underhåll](../../../osd/deploy-use/manage-windows-as-a-service.md). Den här inställningen har ingen inverkan på Windows 10 på plats-uppgradering av aktivitetssekvenser.

Den här klient inställningen ger följande alternativ:

- **Inte konfigurerad**: Configuration Manager ändrar inte inställningen. Administratörer kan i förväg mellanlagra sin egen setupconfig. ini-fil. Detta värde är standard.

- **Normal**: installationsprogrammet för Windows använder mer system resurser och uppdateringar snabbare. Det använder mer processor tid, så den totala installations tiden är kortare, men användarens avbrott är längre.  

    - Konfigurerar filen setupconfig. ini på enheten med `/Priority Normal` [kommando rads alternativet Windows-installation](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Låg**: du kan fortsätta att arbeta med enheten medan den laddas ned och uppdateras i bakgrunden. Den totala installations tiden är längre, men användarens avbrott är kortare. Du kan behöva öka uppdateringens maximala körnings tid för att undvika tids gräns när du använder det här alternativet.  

    - `/Priority` Tar bort [kommando rads alternativet för installations programmet för Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) från filen setupconfig. ini.


### <a name="enable-third-party-software-updates"></a>Aktivera program uppdateringar från tredje part

När du ställer in det här alternativet på **Ja**ställer det in principen för **Tillåt signerade uppdateringar för en Microsoft-uppdateringstjänst på intranätet** och installerar signerings certifikatet i arkivet för betrodda utgivare på klienten.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Aktivera dynamisk uppdatering för funktions uppdateringar
<!--4062619-->
Från och med Configuration Manager version 1906 kan du konfigurera [dynamisk uppdatering för Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). Dynamisk uppdatering installerar språk paket, funktioner på begäran, driv rutiner och ackumulerade uppdateringar under Windows-installationen genom att dirigera klienten för att ladda ned uppdateringarna från Internet. När den här inställningen är inställd på **Ja** eller **Nej**ändrar Configuration Manager den [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) -fil som används under installationen av funktions uppdateringen.

- **Inte konfigurerad** – standardvärdet. Inga ändringar har gjorts i setupconfig-filen.
  - Dynamisk uppdatering är aktiverat som standard i alla versioner av Windows 10 som stöds.
    - För Windows 10 version 1803 och tidigare kontrollerar dynamisk uppdatering enhetens WSUS-server för godkända dynamiska uppdateringar. I Configuration Manager miljöer godkänns dynamiska uppdateringar aldrig direkt på WSUS-servern så att enheterna inte installerar dem.
    - Från och med Windows 10 version 1809 använder dynamisk uppdatering enhetens Internet anslutning för att hämta dynamiska uppdateringar från Microsoft Update. Dessa dynamiska uppdateringar publiceras inte för WSUS-användning.
- **Ja** – aktiverar dynamisk uppdatering.
- **No** -inaktiverar dynamisk uppdatering.


## <a name="state-messaging"></a>Tillstånds meddelanden

### <a name="state-message-reporting-cycle-minutes"></a>Rapporterings cykel för tillstånds meddelande (minuter)

Anger hur ofta klienter rapporterar tillstånds meddelanden. Den här inställningen är 15 minuter som standard.



## <a name="user-and-device-affinity"></a>Mappning mellan användare och enhet  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Användningströskel för tillhörighet mellan användare och (minuter)

Ange antalet minuter innan Configuration Manager skapar mappning av mappning mellan användare och enhet. Som standard är det här värdet 2880 minuter (två dagar).

### <a name="user-device-affinity-usage-threshold-days"></a>Användningströskel för tillhörighet mellan användare och (dagar)

Ange det antal dagar under vilka klienten mäter tröskelvärdet för användnings baserad enhets tillhörighet. Som standard är det här värdet 30 dagar.

> [!NOTE]  
> Du kan till exempel ange **användnings tröskeln för tillhörighet mellan användare och enhet (minuter)** som **60** minuter och **användnings tröskeln för tillhörighet mellan användare och enhet (dagar)** som **5** dagar. Användaren måste sedan använda enheten i 60 minuter under en period på fem dagar för att skapa automatisk tillhörighet med enheten.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Konfigurera automatiskt tillhörighet mellan användare och enhet från användningsdata

Välj **Ja** för att skapa automatisk mappning mellan användare och enhet baserat på den användnings information som Configuration Manager samlar in.  

### <a name="allow-user-to-define-their-primary-devices"></a>Tillåt att användarna definierar sina primära enheter
<!--3485366-->
När den här inställningen är **Ja**kan användarna identifiera sina egna primära enheter i Software Center. Mer information finns i [användar handboken för Software Center](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> Windows Analytics-tjänsten dras tillbaka den 31 januari 2020. Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics är utvecklingen av Windows Analytics. Mer information finns i [Vad är Desktop Analytics](../../../desktop-analytics/overview.md).
