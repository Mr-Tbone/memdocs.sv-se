---
title: Krav för distribution av Windows-klient
titleSuffix: Configuration Manager
description: Läs om kraven för att distribuera Configuration Manager-klienten till Windows-datorer.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713977"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Krav för distribution av klienter till Windows-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Distribution av Configuration Manager klienter i miljön har följande externa beroenden och beroenden inom produkten. Dessutom har varje klientdistributionsmetod sina egna beroenden som måste vara uppfyllda om klientinstallationerna ska lyckas.  

Mer information om minimi kraven för maskin vara och operativ system för Configuration Manager-klienten finns i [konfigurationer som stöds](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> De versionsnummer för programvaran som anges är endast de lägsta versionerna som krävs.  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Krav för Windows-klienter  

Använd följande information för att fastställa kraven för när du installerar Configuration Manager-klienten på Windows-enheter.  

### <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager  

|Komponent|Beskrivning|  
|---|---|  
|Windows Installer version 3.1.4000.2435|Krävs för att det ska gå att använder Windows Installers uppdateringsfiler (.msp) för paket och programvaruuppdateringar.|  
|Microsoft Background Intelligent Transfer Service (BITS) version 2.5|Krävs för att tillåta begränsad data överföring mellan klient datorn och Configuration Manager plats system. BITS laddas inte ned automatiskt under klient installationen. När BITS installeras på datorerna kräver det vanligt vis en omstart för att slutföra installationen.<br /><br /> De flesta operativ system innehåller BITS. Om de inte gör det installerar du BITS innan du installerar Configuration Manager-klienten.|  
|Microsoft Task Scheduler|Aktivera den här tjänsten på klienten för att slutföra klient installationen.|  
|Stöd för SHA-2-kod signering|Från och med version 1906 kräver klienterna stöd för SHA-2-algoritmen för kod signering. Mer information finns i [stöd för SHA-2-kod signering](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>Stöd för SHA-2-kod signering

<!--SCCMDocs-pr#3404-->
På grund av svagheter i SHA-1-algoritmen och för att anpassa sig till bransch standarder, signerar Microsoft nu bara Configuration Manager binärfiler med hjälp av säkrare SHA-2-algoritmen. Äldre Windows OS-versioner kräver en uppdatering av stöd för SHA-2-kod signering. Mer information finns i [support kravet för 2019 SHA-2-kod signering för Windows och WSUS](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Om du inte uppdaterar dessa versioner av operativ systemet kan du inte installera Configuration Manager-klient version 1906. Det här beteendet gäller för antingen en ny klient installation eller uppdatering från en tidigare version.

Om du behöver hantera en klient på en version av Windows som inte har uppdaterats, eller äldre än de versioner som anges ovan, använder du Configuration Manager Extended driftskompatibilitet client (EIC) version 1902. Mer information finns i [Extended driftskompatibilitet client](../../understand/interoperability-client.md).

> [!Tip]  
> Om du inte använder [Automatisk klient uppdatering](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)och uppdaterar klienter med en annan mekanism, måste du uppdatera versionen av CCMSetup. En äldre version av CCMSetup kanske inte korrekt validerar det nya SHA-2 kod signerings certifikatet på klientens binärfiler för version 1906. Om du till exempel kopierar CCMSetup. exe till en fil resurs eller använder CCMSetup. msi med grup princip.<!-- 4963362 -->
>
> Följande klient uppdaterings metoder bör inte påverkas:
>
> - Push-installation av klient: den använder klient paketet från platsen
> - Installation baserad på program uppdatering: plats uppdateringen publiceras om till WSUS
> - Intune MDM-hanterade Windows-enheter: den version som stöds för den här mekanismen har redan stöd för SHA-2 kod signering, men det är fortfarande viktigt att använda den senaste CCMSetup. msi

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Externa beroenden till Configuration Manager och hämtas automatiskt under installationen  

Den Configuration Manager klienten har externa beroenden. Dessa beroenden beror på operativ systemets version och installerad program vara på klient datorn.  

Om klienten kräver dessa beroenden för att slutföra installationen installeras de automatiskt.  

|Komponent|Beskrivning|  
|---|---|  
|Windows Update Agent version 7.0.6000.363|Krävs av Windows för stöd av identifiering och distribution av uppdateringar.|  
|Microsoft Core XML Services (MSXML) version 6.20.5002 eller senare|Krävs för bearbetning av XML-dokument i Windows.|  
|Microsoft Remote Differential Compression (RDC)|Krävs för optimering av dataöverföringar i nätverket|  
|Microsoft Visual C++ 2013 Redistributable version 12.0.21005.1|Krävs för stöd av klientåtgärder. När du installerar den här uppdateringen på klient datorer kan det krävas en omstart för att slutföra installationen.|  
|Microsoft Visual C++ 2005 Redistributable version 8.0.50727.42|För version 1606 och tidigare krävs stöd för Microsoft SQL Server Compact åtgärder.|  
|Windows Imaging APIs 6.0.6001.18000|Krävs för att tillåta Configuration Manager att hantera Windows-avbildningsfiler (. wim).|  
|Microsoft Policy Platform 1.2.3514.0|Krävs för att klienter ska kunna utvärdera efterlevnadsinställningar.|  
|Microsoft .NET Framework version 4.5.2|Krävs för stöd av klientåtgärder. Installeras automatiskt på klient datorn om den inte har Microsoft .NET Framework version 4,5 eller senare installerad. Mer information finns i [Mer information om Microsoft .NET Framework version 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 4,0 SP1-komponenter|Krävs för att lagra information som rör klientåtgärder.|  

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Om du fortfarande använder användar upplevelsen för webbplatsen för program katalogen kräver klienten Microsoft Silverlight 5.1.41212.0. Klienten installerar inte Silverlight automatiskt. De viktigaste funktionerna i program katalogen ingår nu i Software Center.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>Mer information om Microsoft .NET Framework version 4.5.2  

> [!NOTE]  
> .NET 4,0, 4,5 och 4.5.1 stöds inte längre. Mer information Microsoft .NET finns i avsnittet [vanliga frågor och svar om livs cykel policy för support](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework version 4.5.2 kan kräva en omstart för att slutföra installationen. Användaren ser ett meddelande som **krävs för omstart** i system fältet. Följande vanliga scenarier kräver att klient datorer startas om:  

- .NET-program eller -tjänster som körs på datorn.  

- Det saknas en eller flera programuppdateringar som krävs för installation av .NET.  

- Datorn väntar på att startas om från föregående installation av programuppdateringar för .NET Framework.  

När .NET Framework 4.5.2 har installerats kan det krävas ytterligare uppdateringar. Dessa senare uppdateringar kan kräva ytterligare omstarter av datorn.  

### <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager  

Mer information finns i [bestämma plats system roller för-klienter](plan/determine-the-site-system-roles-for-clients.md).  

|Komponent|Beskrivning|  
|---|---|  
|Hanteringsplats|Om du vill distribuera Configuration Manager-klienten behöver du inte någon hanterings plats. Klienter kräver en hanterings plats för att överföra information till platsen. Utan hanterings plats kan du inte hantera klient datorer.|  
|Distributionsplats|Distributions platsen är en valfri men Rekommenderad plats Systems roll för klient distribution och hantering. Alla distributions platser är värdar för klientens källfiler. Klienter hittar den närmaste distributions plats från vilken du vill ladda ned källfilerna under klient distributionen eller uppdateringen. Om platsen inte har en distributions plats laddar datorer ned klientens källfiler från hanterings platsen.|  
|Status för återställningsplats|Återställningsstatusplatsen är en valfri men rekommenderad platssystemsroll för klientdistribution. Återställnings status platsen spårar klient distribution och gör att datorer på den Configuration Manager platsen kan skicka tillstånds meddelanden när de inte kan kommunicera med en hanterings plats.|  
|Rapporteringstjänstpunkt|Repor ting Services-platsen är en valfri men Rekommenderad plats Systems roll. Den visar rapporter som rör klient distribution och hantering. Mer information finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).|  

### <a name="installation-method-dependencies"></a>Installations metodens beroenden  

Följande förutsättningar är specifika för de olika klientinstallationsmetoderna.  

#### <a name="client-push-installation"></a>Push-installation av klient  

- -Platsen använder konton för push-installation av klienter för att ansluta till datorer för att installera-klienten. Ange dessa konton på fliken **konton** i egenskaperna för push-installation av klienter. Kontot måste vara medlem av den lokala administratörsgruppen på måldatorn.  

    Om du inte anger ett konto för push-installation av klienter använder plats servern sitt dator konto.  

- Platsen måste identifiera den dator där du installerar klienten. Minst en Configuration Manager identifierings metod krävs.  

- Datorn har en resurs som heter ADMIN$.  

- Om du vill push-överföra Configuration Manager-klienten automatiskt till identifierade resurser väljer du alternativet för att **Aktivera push-installation av klienter till tilldelade resurser** i egenskaperna för push-installation av klienten.  

- Klient datorn måste kommunicera med en distributions plats eller en hanterings plats för att kunna hämta källfilerna.  

- När du kräver ömsesidig Kerberos-autentisering måste klienterna finnas i en betrodd Active Directory skog. Kerberos i Windows förlitar sig på Active Directory för ömsesidig autentisering.<!--1358204-->  

Om du vill använda push-teknik för klienter behöver du följande säkerhets behörigheter:  

- Konfigurera kontot för push-installation av klienter: behörigheten **ändra** och **Läs** för objektet **plats** .  

- Om du vill använda push-installation av klienten för att installera klienten på samlingar, enheter och frågor: **Ändra resurs** -och **Läs** behörighet för objektet **samling** .  

Standard säkerhets rollen **infrastruktur administratör** innehåller de behörigheter som krävs för att hantera push-installationer av klienter.  

#### <a name="software-update-point-based-installation"></a>Platsbaserad klientinstallation av programuppdateringar  

- Om du inte har utökat Active Directory-schemat, eller om du installerar klienter från en annan skog, använder du grup princip för att etablera installations parametrar för CCMSetup. exe. Mer information finns i [så här etablerar du klient installations egenskaper](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Publicera Configuration Manager-klienten på program uppdaterings platsen.  

- För att kunna hämta källfilerna måste klient datorn kommunicera med en distributions plats eller en hanterings plats.  

De säkerhets behörigheter som krävs för att hantera Configuration Manager program uppdateringar finns i [krav för program uppdateringar](../../../sum/plan-design/prerequisites-for-software-updates.md).  

#### <a name="group-policy-based-installation"></a>Principbaserad installation  

- Om du inte har utökat Active Directory-schemat, eller om du installerar klienter från en annan skog, använder du grup princip för att etablera installations parametrar för CCMSetup. exe. Mer information finns i [så här etablerar du klient installations egenskaper](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- För att kunna hämta källfilerna måste klient datorn kommunicera med en distributions plats eller en hanterings plats.  

#### <a name="logon-script-based-installation"></a>Inloggningsskriptsbaserad installation  

För att kunna hämta källfilerna måste klient datorn kommunicera med en distributions plats eller en hanterings plats. Om du inte har angett CCMSetup. exe med följande kommando rads parameter:`ccmsetup /source`  

#### <a name="manual-installation"></a>Manuell installation  

För att kunna hämta källfilerna måste klient datorn kommunicera med en distributions plats eller en hanterings plats. Om du inte har angett CCMSetup. exe med följande kommando rads parameter:`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM-installation

- Kräver en Microsoft Intune-prenumeration och lämpliga licenser.  

- Kräver att enheten har Internet åtkomst, även om den inte är Internet-baserad.  

- Beroende på användnings fallet kan du också behöva en eller båda av följande tekniker:  

    - Azure Active Directory  

    - Gateway för molnhantering  

#### <a name="workgroup-computer-installation"></a>Installation av arbetsgruppsdatorer  

För att få åtkomst till resurser i Configuration Manager plats serverns domän, konfigurerar du ett konto för nätverks åtkomst för platsen.  

Mer information om hur du konfigurerar kontot för nätverks åtkomst finns i [grundläggande begrepp för innehålls hantering](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Programdistributionsbaserad installation (endast för uppgraderingar)  

- Om du inte har utökat Active Directory-schemat, eller om du installerar klienter från en annan skog, använder du grup princip för att etablera installations parametrar för CCMSetup. exe. Mer information finns i [så här etablerar du klient installations egenskaper](deploy-clients-to-windows-computers.md#BKMK_Provision).

- För att kunna hämta källfilerna måste klient datorn kommunicera med en distributions plats eller en hanterings plats.  

De säkerhets behörigheter som krävs för att uppgradera Configuration Manager-klienten med hjälp av program hantering finns i [säkerhet och sekretess för program hantering](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

#### <a name="automatic-client-upgrades"></a>Automatiska klientuppgraderingar  

Du måste ha säkerhetsrollen **Fullständig administratör** om du ska kunna konfigurera automatiska klientuppgraderingar.  

### <a name="firewall-requirements"></a>Brandväggsförutsättningar  

Om det finns en brand vägg mellan plats system servrarna och datorerna där du vill installera Configuration Manager-klienten, se Windows- [brandväggen och port inställningar för klienter](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>Krav för mobila enhets klienter  

När du installerar Configuration Manager-klienten på mobila enheter och registrerar dem ska du använda den här informationen för att fastställa kraven.  

### <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager

- En Microsoft-utfärdare av företagscertifikat med certifikatmallar för att distribuera och hantera de certifikat som krävs för mobila enheter.  

    Certifikatutfärdaren måste godkänna certifikatbegäranden från användare av mobila enheter automatiskt under registreringen.  

    Mer information om certifikat kraven finns i [säkerhet och sekretess för certifikat profiler](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- En säkerhetsgrupp som innehåller användarna som kan registrera sina mobila enheter.  

    Denna säkerhetsgrupp används för att konfigurera certifikatsmallen som används vid registreringen av mobila enheter.  

- Valfritt men rekommenderat: ett DNS-alias (CNAME-post) med namnet **configmgrenroll**. Konfigurera det här aliaset för Server namnet för proxyn för registrerings platsen.  

    Detta DNS-alias krävs för att stödja automatisk identifiering för registrerings tjänsten. Om du inte konfigurerar den här DNS-posten måste användare manuellt ange namnet på proxyn för registrerings platsen som en del av registrerings processen.  

- Beroenden för plats system rollen för de datorer som kör registrerings platsen och plats system rollerna för registrerings platsen.  

    Mer information finns i [operativ system som stöds för plats system servrar](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager

Mer information finns i [bestämma plats system roller för-klienter](plan/determine-the-site-system-roles-for-clients.md).  

- Hanterings plats som är konfigurerad för HTTPS-klientanslutningar och aktive rad för mobila enheter  

    En hanterings plats krävs alltid för att installera Configuration Manager-klienten på mobila enheter. Förutom konfigurations kraven för HTTPS och aktive rad för mobila enheter måste hanterings platsen konfigureras med ett fullständigt domän namn för Internet och acceptera klient anslutningar från Internet.  

- Registreringsplats och registreringsproxyplats  

    En registreringsproxyplats hanterar registreringsbegäranden från mobila enheter, och registreringsplatsen slutför registreringen. Registreringsplatsen måste finnas i samma Active Directory-skog som platsservern, men registreringsproxyplatsen kan befinna sig i en annan skog.  

- Klientinställningar för registrering av mobila enheter  

    Konfigurera klientinställningarna så att användarna kan registrera mobila enheter och konfigurera minst en registreringsprofil.  

- Rapporteringstjänstpunkt  

    Rapporteringstjänstplatsen är en valfri men rekommenderad platssystemsroll som kan visa rapporter som rör registrering av mobila enheter och klienthantering.  

    Mer information finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).  

- Du måste ha följande säkerhetsbehörigheter för att kunna konfigurera registreringen för mobila enheter:  

    - Lägga till, ändra och ta bort registreringsplatssystemsroller: behörigheten **Ändra** för objektet **Plats**.  

    - Konfigurera klientinställningar för registrering: standardklientinställningar kräver behörigheten **Ändr** för objektet **Plats** och anpassade klientinställningar kräver behörigheten **Klientagent**.  

    Standard säkerhets rollen **Fullständig administratör** innehåller de behörigheter som krävs för att konfigurera registrerings plats system roller.  

- Om du vill hantera registrerade mobila enheter måste du ha följande säkerhetsbehörigheter:  

    - Rensa eller dra tillbaka en mobil enhet: **Ta bort resurs** för objektet **Samling**.  

    - Annullera ett rensnings- eller tillbakadragningskommando: **Ta bort resurs** för objektet **Samling**.  

    - Tillåta och blockera mobila enheter: **Ändra resurs** för objektet **Samling** .  

    - Fjärrlåsa eller återställa lösenordet på en mobil enhet: resursen **Ändra** för objektet **Samling**.  

    Standard säkerhets rollen **drifts administratör** innehåller de behörigheter som krävs för att hantera mobila enheter.  

    Mer information om hur du konfigurerar säkerhets behörigheter finns i [grunderna i rollbaserad administration](../../understand/fundamentals-of-role-based-administration.md) och [Konfigurera rollbaserad administration](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Brandväggsförutsättningar

Mellanliggande nätverksenheter som t.ex. routrar och brandväggar, och Windows-brandväggen i tillämpliga fall, måste tillåta den trafik som hör till registrering av mobila enheter:  

- Mellan mobila enheter och registreringsproxyplatsen: HTTPS (som standard, TCP 443)  

- Mellan registreringsproxyplatsen och registreringsplatsen: HTTPS (som standard, TCP 443)  

Om du använder en proxyserver måste den konfigureras för SSL-tunnel. SSL-bryggning stöds inte för mobila enheter.  
