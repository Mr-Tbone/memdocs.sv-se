---
title: Planera för SMS-providern
titleSuffix: Configuration Manager
description: Läs mer om plats system rollen för SMS-providern i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01ea9b089da3cfcfc3e8d23e7ad25d27ab2fec7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712556"
---
# <a name="plan-for-the-sms-provider"></a>Planera för SMS-providern

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill hantera Configuration Manager använder du en Configuration Manager-konsol som ansluter till en instans av **SMS-providern**. Som standard installeras en SMS-provider på plats servern när du installerar en central administrations plats eller en primär plats.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Om SMS-providern  

SMS-providern är en Windows Management Instrumentation-Provider (WMI) som tilldelar **Läs** -och **skriv** åtkomst till Configuration Manager-databasen på en plats.  

- Du måste ha minst en SMS-provider på varje central administrationswebbplats och primär plats. Du kan installera ytterligare providers vid behov.  

- Säkerhets gruppen **SMS-administratörer** ger åtkomst till SMS-providern. Configuration Manager skapar automatiskt den här gruppen på plats servern och på varje dator där du installerar en instans av SMS-providern. Mer information finns i [SMS-administratörer](accounts.md#sms-admins).  

- Sekundära platser har inte stöd för SMS-providerns roll.  

Configuration Manager administrativa användare använder en SMS-provider för att komma åt information som lagras i-databasen. Administratörer kan göra detta genom att använda Configuration Manager-konsolen, Resursläsaren, verktyg och anpassade skript. SMS-providern interagerar inte med Configuration Manager klienter. När en Configuration Manager-konsol ansluter till en plats, frågar den WMI på plats servern för att hitta en instans av SMS-providern som ska användas.  

SMS-providern hjälper till att upprätthålla Configuration Manager säkerhet. Den returnerar bara den information som konsol användaren har behörighet att visa.  

SMS-providern ger också åtkomst till API-samverkan över HTTPS, som kallas **administrations tjänsten**. Den här REST API kan användas i stället för en anpassad webb tjänst för att komma åt information från webbplatsen. Mer information finns i [Vad är administrations tjänsten?](../../../develop/adminservice/overview.md).

> [!IMPORTANT]  
> När varje instans av SMS-providern för en plats är offline kan Configuration Manager-konsoler inte ansluta till platsen.  

Mer information om hur du hanterar SMS-providern finns i [Hantera SMS-providern](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Installationskrav  

För att stödja SMS-providern måste mål servern uppfylla följande krav:  

- I samma domän som plats servern och plats systemen för plats databasen  

- Kan inte ha en plats system roll från en annan plats  

- Det går inte att redan ha en SMS-provider från någon plats  

- Kör en OS-version som stöds  

- Minst 650 MB ledigt disk utrymme för att stödja Windows ADK-komponenterna. Mer information om Windows ADK och SMS-providern finns i [krav för operativ Systems distribution](#BKMK_WAIKforSMSProv).  

- För [administrations tjänsten](../../../develop/adminservice/overview.md) REST API:

  - .NET 4,5 eller senare

  - Aktivera webb server för Windows Server **-roll (IIS)**

    > [!Note]  
    > Varje SMS-provider försöker installera administrations tjänsten, som kräver ett certifikat. Den här tjänsten har ett beroende på IIS för att binda certifikatet till HTTPS-port 443. Om du aktiverar [utökat http](enhanced-http.md)binder platsen det certifikatet med IIS-API: er. Om din webbplats använder PKI måste du manuellt binda ett PKI-certifikat i IIS på SMS-providern. Från och med version 2002 använder platsen automatiskt platsens självsignerade certifikat.

## <a name="locations"></a><a name="bkmk_location"></a>Platser  

När du installerar en-plats installerar du automatiskt den första SMS-providern för platsen. Du kan ange någon av följande platser som stöds för SMS-providern:  

- Plats servern  

- Plats databas servern  

- En annan server som uppfyller [installations kraven](#installation-prerequisites)  

Så här visar du platserna för varje SMS-provider för en plats:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj önskad plats i listan och välj sedan **Egenskaper** i menyfliksområdet.  

3. På fliken **Allmänt** i plats **egenskaperna**visar du fältet plats för **SMS-provider** .  

Varje SMS-provider stöder samtidiga anslutningar från flera begäranden. De enda begränsningarna för dessa anslutningar är antalet Server anslutningar som är tillgängliga för Windows och de tillgängliga resurserna på servern för att betjäna anslutnings begär Anden.  

När du har installerat en-plats kan du köra Configuration Manager-installationen på plats servern igen. Använd installations programmet för att ändra platsen för en befintlig SMS-provider eller för att installera ytterligare SMS-providers på platsen. Installera endast en SMS-provider på en dator. En dator kan inte vara värd för en SMS-provider från fler än en plats.  

### <a name="choosing-a-location"></a>Välja en plats

I följande avsnitt beskrivs fördelarna och nack delarna med att installera en SMS-provider på varje plats som stöds:  

#### <a name="configuration-manager-site-server"></a>Configuration Manager plats Server

- **Fördelar**  

  - SMS-providern använder inte system resurserna för plats databasens dator.  

  - Den här platsen kan ge bättre prestanda än en SMS-provider som finns på en annan dator än platsservern eller platsdatabasens dator.  

- **Nack delarna**  

  - SMS-providern använder system- och nätverksresurser som kan dedikeras till platsserveråtgärder.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server som är värd för plats databasen

- **Fördelar**  

  - SMS-providern använder inte system resurser på plats servern.  

  - Den här platsen kan erbjuda den bästa prestandan av tre platser, om det finns tillräckligt med serverresurser tillgängliga.  

- **Nack delarna**  

  - SMS-providern använder system- och nätverksresurser som kan dedikeras till platsdatabasåtgärder.  

  - När plats databasen finns på en klustrad instans av SQL Server kan du inte använda den här platsen.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>En annan dator än plats servern eller plats databas servern

- **Fördelar**  

  - SMS-providern använder inte plats servern eller plats databasens system resurser.  

  - Med den här typen av plats kan du distribuera ytterligare SMS-providers för att erbjuda hög tillgänglighet för anslutningar.  

- **Nack delarna**  

  - Prestandan för SMS-providern kan vara lägre. Detta beror på den ytterligare nätverks aktivitet som krävs för att koordinera med plats servern och plats databasens dator.  

  - Den här servern måste alltid vara tillgänglig för plats databas servern och till alla datorer där Configuration Manager-konsolen är installerad.  

  - Den här platsen kan använda systemresurser som annars skulle dedikeras till andra tjänster.  

## <a name="authentication"></a><a name="bkmk_auth"></a>Anspråksautentisering

<!--1357013-->
Från och med version 1810 kan du ange den lägsta autentiseringsnivån som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. Den gäller för alla komponenter som har åtkomst till SMS-providern. Till exempel Configuration Manager-konsolen, SDK-metoder och Windows PowerShell-cmdletar.

### <a name="configure-authentication"></a>Konfigurera autentisering

Om du vill konfigurera den här inställningen loggar du först in på Windows med avsedd autentiseringsnivå.

> [!Important]  
> Den här konfigurationen är en inställning för hela hierarkin. Innan du ändrar den här inställningen ser du till att alla Configuration Manager administratörer kan logga in i Windows med den autentiseringsnivå som krävs.

Använd följande steg för att konfigurera den här inställningen:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj **Inställningar för hierarki** i menyfliksområdet.  

3. Växla till fliken **autentisering** . Välj önskad [Autentiseringsnivå](#authentication-levels)och välj sedan **OK**.  

    - Om det behövs väljer du **Lägg till** för att undanta vissa användare eller grupper. Mer information finns i [undantag](#exclusions).  

### <a name="authentication-levels"></a>Autentiseringsnivåer

Följande nivåer är tillgängliga:

- **Windows-autentisering**: Kräv autentisering med Active Directory domänautentiseringsuppgifter. Den här inställningen är föregående beteende och den aktuella standardinställningen. När du uppdaterar platsen sker ingen ändring av autentiseringsnivån.  

- **Certifikatautentisering**: Kräv autentisering med ett giltigt certifikat som har utfärdats av en betrodd PKI-certifikatutfärdare. Du konfigurerar inte det här certifikatet i Configuration Manager. Configuration Manager kräver att administratören är inloggad i Windows med PKI.  

- **Windows Hello för företag-autentisering**: Kräv autentisering med stark tvåfaktorautentisering som är knutet till en enhet och använder biometrik eller en PIN-kod. Mer information finns i [Windows Hello för företag](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Undantag

På fliken **autentisering** i inställningar för hierarki kan du även utesluta vissa användare eller grupper. Använd det här alternativet sparsamt. Till exempel när vissa användare behöver åtkomst till Configuration Manager-konsolen, men inte kan autentisera till Windows på den nivå som krävs. Det kan också vara nödvändigt för Automation eller tjänster som körs under ett system kontos kontext.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a>Om SMS-providerns språk  

SMS-providern fungerar oberoende av visnings språket för den server där du installerar den.  

När en administrativ användare eller Configuration Manager bearbetar data med hjälp av SMS-providern, försöker den returnera dessa data i ett format som matchar operativ system språket för den begär ande datorn.

Hur det försöker matcha språket är indirekt. SMS-providern översätter inte information från ett språk till ett annat. När data returneras för visning i Configuration Manager-konsolen beror visnings språket för data på källan till objektet och typen av lagring.  

När Configuration Manager lagrar data för ett objekt i databasen beror de tillgängliga språken på följande faktorer:  

- Configuration Manager lagrar objekt som skapas med hjälp av stöd för flera språk. Objektet lagras i plats databasen med hjälp av de språk som du konfigurerar för platsen när du kör installations programmet. Configuration Manager-konsolen visar dessa objekt på visnings språket för den begär ande datorn när det språket är tillgängligt för objektet. Om konsolen inte kan visa objektet på visnings språket för den begär ande datorn visas objektet på standard språket, vilket är engelska.  

- Configuration Manager lagrar objekt som en administrativ användare skapar med hjälp av det språk som användes för att skapa objektet. Dessa objekt visas i Configuration Manager-konsolen på samma språk. SMS-providern kan inte översätta dem och de har inte flera språk alternativ.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a>Använd flera SMS-providers  

När installationen har slutförts för en plats kan du installera ytterligare SMS-providers för platsen. Om du vill installera ytterligare SMS-providers kör Configuration Manager-installationen på plats servern.

Överväg att installera ytterligare SMS-providers när något av följande stämmer:  

- Många administrativa användare behöver använda Configuration Manager-konsolen och ansluta till en plats på samma tid.  

- Du använder Configuration Manager SDK eller andra produkter som kan leda till vanliga anrop till SMS-providern.  

- Du har ett affärs krav för att få hög tillgänglighet för SMS-providern.  

När du installerar flera SMS-providrar på en plats och en anslutningsbegäran görs tilldelar webbplatsen slumpmässigt varje ny anslutningsbegäran för att använda en installerad SMS-provider. Du kan inte ange vilken SMS-provider som ska användas med en speciell session.  

> [!NOTE]  
> Ta hänsyn till fördelarna och nack delarna med varje plats för SMS-provider. Mer information finns i [platser](#bkmk_location). Balansera dessa överväganden med den information som du inte kan kontrol lera vilken SMS-provider som används för varje ny anslutning.  

När du först ansluter en Configuration Manager-konsol till en plats, frågar anslutningen WMI på plats servern. Den här frågan identifierar en instans av SMS-providern som konsolen använder. Den här speciella instansen av SMS-providern är fortfarande använda av-konsolen tills sessionen avslutas. Om sessionen avslutas eftersom SMS-providern inte är tillgänglig i nätverket, upprepas den första frågan när du återansluter-konsolen till platsen. Det är möjligt att platsen tilldelar samma instans av SMS-providern som inte är tillgänglig. Om det här problemet inträffar försöker du att återansluta-konsolen tills platsen returnerar en tillgänglig SMS-provider.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a>Om SMS-Providerns namn område  

Configuration Manager WMI-schemat definierar strukturen för SMS-providern. Schema namn rymder beskriver platsen för Configuration Manager data i SMS-providerns schema. Följande tabell innehåller några av de vanliga namn rymder som SMS-providern använder:  

|Namnområde|Beskrivning|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|SMS-providern, som i stor utsträckning används av Configuration Manager-konsolen, Resursläsaren, Configuration Manager verktyg och skript.|  
|`Root\SMS\SMS_ProviderLocation`|Platsen för SMS-providerns datorer för en plats.|  
|`Root\CIMv2`|Platsen som inventerats för WMI-namnområdes information under maskin-och program varu inventering.|  
|`Root\CCM`|Configuration Manager klient konfigurations principer och klient data.|  
|`Root\CIMv2\SMS`|Platsen för de inventerings rapporterings klasser som inventerings klient agenten samlar in. Klienterna kompilerar de här inställningarna under utvärderingen av dator principer. De här inställningarna baseras på klient inställnings konfigurationen för datorn.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a>Krav för operativ Systems distribution

Datorn där du installerar en instans av SMS-providern kräver en version av Windows ADK som stöds.  

Mer information om det här kravet finns i [infrastruktur krav för operativ Systems distribution](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) och [stöd för Windows 10](../configs/support-for-windows-10.md).  

När du hanterar operativ system distributioner kan SMS-providern utföra olika uppgifter i Windows ADK, till exempel:  

- Visa WIM-filinformation  

- Lägga till drivrutinsfiler i befintliga startavbildningar  

- Skapa ISO-filer för start  

Installationen av Windows ADK kan kräva upp till 650 MB ledigt diskutrymme på varje dator där SMS-providern installeras. Kravet på högt disk utrymme krävs för att Configuration Manager ska kunna installera Windows PE-startavbildningarna.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a>Administrations tjänst

<!--3607711, fka 1321523-->

SMS-providern ger API-interoperabilitet via en HTTPS OData-anslutning, som kallas **administrations tjänsten**. Den här REST API kan användas i stället för en anpassad webb tjänst för att komma åt information från webbplatsen.

Mer information finns i [Vad är administrations tjänsten?](../../../develop/adminservice/overview.md)
