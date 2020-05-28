---
title: Moln distributions plats
titleSuffix: Configuration Manager
description: Planera och utforma för att distribuera program varu innehåll via Microsoft Azure med moln distributions platser i Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52c2b70d2b094d5a89d80aafa61f1db67a53816f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987708"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Använd en moln distributions plats i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Implementeringen av delning av innehåll från Azure har ändrats. Använd en innehålls aktive rad Cloud Management Gateway genom att aktivera alternativet för att **tillåta att CMG fungerar som en moln distributions plats och hanterar innehåll från Azure Storage**. Mer information finns i [ändra en CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Du kommer inte att kunna skapa en traditionell moln distributions plats i framtiden. Mer information finns i [borttagna och föråldrade funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

En moln distributions plats är en Configuration Manager-distributions plats som är värd för PaaS (Platform-as-a-Service) i Microsoft Azure. Den här tjänsten har stöd för följande scenarier:  

- Tillhandahålla program varu innehåll till Internetbaserade klienter utan ytterligare lokal infrastruktur  

- Moln – aktivera innehålls distributions systemet  

- Minska behovet av traditionella distributions platser  

Den här artikeln hjälper dig att lära dig om moln distributions platsen, planera för användning och hur du utformar din implementering. Den innehåller följande avsnitt:

- [Funktioner och fördelar](#bkmk_features)
- [Topologins design](#bkmk_topology)
- [Krav](#bkmk_requirements)
- [Specifikationer](#bkmk_spec)
- [Kostnad](#bkmk_cost)
- [Prestanda och skalning](#bkmk_perf)
- [Portar och data flöde](#bkmk_dataflow)
- [Certifikat](#bkmk_certs)
- [Vanliga frågor och svar (FAQ)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a>Funktioner och fördelar

### <a name="features"></a>Funktioner

Moln distributions platsen har stöd för flera funktioner som också erbjuds av lokala distributions platser:  

- Hantera moln distributions platser individuellt eller som medlemmar i distributions plats grupper  

- Använd en moln distributions plats som en återställnings innehålls plats  

- Stöder både intranät-och Internetbaserade klienter  

### <a name="benefits"></a>Fördelar

Moln distributions platsen ger följande ytterligare fördelar:  

- Platsen krypterar innehållet innan det skickas till moln distributions platsen i Azure.  

- Skala moln tjänsten manuellt i Azure för att möta förändrade krav för innehålls begär Anden från klienter. Den här åtgärden kräver inte att du installerar och etablerar ytterligare distributions platser i Configuration Manager.  

- Stöder nedladdning av innehåll från klienter som kon figurer ATS för andra innehålls tekniker, till exempel Windows BranchCache och alternativa innehålls leverantörer.  

- Från och med version 1806 använder du moln distributions platser som käll platser för mottagar distributions platser.  


## <a name="topology-design"></a><a name="bkmk_topology"></a>Topologins design

Distribution och drift av moln distributions platsen innehåller följande komponenter:  

- En **moln tjänst** i Azure. Platsen distribuerar innehåll till den här tjänsten, som lagrar den i Azure Cloud Storage. Hanterings platsen ger klienterna den här innehålls platsen i listan över tillgängliga källor efter behov.  

- En plats system roll för **hanterings** plats tjänster som klient begär per normal.  

    - Lokala klienter använder vanligt vis en lokal hanterings plats.  

    - Internetbaserade klienter använder antingen en [Gateway för moln hantering](../../clients/manage/cmg/plan-cloud-management-gateway.md)eller en [Internetbaserad hanterings plats](../../clients/manage/plan-internet-based-client-management.md).  

- Moln distributions platsen använder en **CERTIFIKATBASERAD https** -webbtjänst för att skydda nätverkskommunikation med klienter. Klienterna måste ha förtroende för det här certifikatet.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Från och med version 1806 skapar du en moln distributions plats med hjälp av en **Azure Resource Manager distribution**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en [resurs grupp](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). När du distribuerar en moln distributions plats med Azure Resource Manager använder platsen Azure Active Directory (Azure AD) för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure.  

> [!Note]  
> Den här funktionen aktiverar inte stöd för Azure Cloud Service-leverantörer (CSP). Distributions platsen för moln distribution med Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av CSP: n. Mer information finns i [tillgängliga Azure-tjänster i Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av moln distributions platsen. Befintliga distributioner fortsätter att fungera.<!-- 3605704 -->

I Configuration Manager version 1810 och tidigare tillhandahåller guiden moln distributions plats fortfarande alternativet för en **klassisk tjänst distribution** med ett hanterings certifikat för Azure. Använd Azure Resource Manager distributions modell för alla nya moln distributions platser för att förenkla distributionen och hanteringen av resurser. Distribuera om möjligt Befintliga moln distributions platser via Resource Manager.

> [!Important]  
> Från och med version 1810 är den klassiska tjänst distributionen i Azure inaktuell för användning i Configuration Manager. Den här versionen är den sista som stöd för att skapa dessa Azure-distributioner. Den här funktionen kommer att tas bort i en framtida Configuration Manager version.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager migrerar inte befintliga klassiska moln distributions platser till Azure Resource Manager distributions modell. Skapa nya moln distributions platser med hjälp av Azure Resource Manager distributioner och ta sedan bort de klassiska moln distributions platserna.

### <a name="hierarchy-design"></a>Hierarkins design

Var du skapar en moln distributions plats beror på vilka klienter som behöver ha åtkomst till innehållet. Från och med version 1806 finns det tre typer av moln distributions platser:  

- Azure Resource Manager distribution: skapa den här typen på en primär plats eller på den centrala administrations webbplatsen.  

- Klassisk tjänst distribution: skapa endast den här typen på en primär plats.  

- Cloud Management Gateway kan också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. Mer information finns i [Planera för Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Tänk på följande om du vill ta reda på om du ska lägga till moln distributions platser i gränser grupper:  

- Internetbaserade klienter förlitar sig inte på gränser grupper. De använder endast Internet-riktade distributions platser eller moln distributions platser. Om du bara använder moln distributions platser för att betjäna dessa typer av klienter, behöver du inte ta med dem i gränser grupper.  

- Om du vill att klienter i det interna nätverket ska använda en moln distributions plats måste den finnas i samma gränser grupp som-klienterna. Klienter prioriterar moln distributions platser sist i listan med innehålls källor, eftersom det finns en kostnad för att ladda ned innehåll från Azure. En moln distributions plats används vanligt vis som en återställnings källa för intranätbaserade klienter. Om du vill ha en moln-och första design kan du utforma dina begränsnings grupper så att de uppfyller affärs kraven. Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md).  

Även om du installerar moln distributions platser i vissa regioner i Azure är inte klienter medvetna om Azure-regionerna. De väljer slumpmässigt en moln distributions plats. Om du installerar moln distributions platser i flera regioner och en klient tar emot mer än en i innehålls plats listan, kanske klienten inte använder en moln distributions plats från samma Azure-region.  

### <a name="backup-and-recovery"></a>Säkerhetskopiering och återställning  

När du använder en moln distributions plats i-hierarkin använder du följande information som hjälp för att planera för säkerhets kopiering och återställning:  

- När du använder underhålls uppgiften **plats Server för säkerhets kopiering** , innehåller Configuration Manager automatiskt konfigurationerna för moln distributions platsen.  

- Säkerhetskopiera och spara en kopia av certifikatet för serverautentisering. Om du använder den klassiska tjänst distributionen i Azure bör du även säkerhetskopiera och spara en kopia av hanterings certifikatet för Azure. När du återställer Configuration Manager primära platsen till en annan server måste du importera certifikaten på nytt.  


## <a name="requirements"></a><a name="bkmk_requirements"></a>Signaturkrav

- Du behöver en **Azure-prenumeration** som värd för tjänsten.  

    - En **Azure-administratör** behöver delta i den första skapandet av vissa komponenter, beroende på din design. Den här personen behöver inte behörigheter i Configuration Manager.  

- Plats servern kräver **Internet åtkomst** för att distribuera och hantera moln tjänsten.  

- När du använder **Azure Resource Manager** distributions metod integrerar du Configuration Manager med [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) för **moln hantering**. Identifiering av Azure AD- *användare* krävs inte.  

- Ett **certifikat för serverautentisering**. Mer information finns i avsnittet [certifikat](#bkmk_certs) nedan.  

    - Om du vill minska komplexiteten använder du en offentlig certifikat leverantör för certifikatet för serverautentisering. När du gör det behöver du också ett **DNS CNAME-alias** för att klienter ska kunna matcha namnet på moln tjänsten.  

- Om du använder den klassiska distributions metoden i Azure i Configuration Manager version 1810 eller tidigare behöver du ett **hanterings certifikat för Azure**. Mer information finns i avsnittet [certifikat](#bkmk_certs) nedan.  

    > [!TIP]  
    > Från och med Configuration Manager version 1806 använder du **Azure Resource Manager** distributions modell. Det kräver inte detta hanterings certifikat.  
    >
    > Den klassiska distributions metoden är inaktuell från och med version 1810.  

- Ange klient inställningen, **Tillåt åtkomst till moln distributions platser**, till **Ja** i **Cloud Servicess** gruppen. Det här värdet är inställt på **Nej**som standard.  

- Klient enheter kräver **Internet anslutning**och måste använda **IPv4**.  


## <a name="specifications"></a><a name="bkmk_spec"></a>Krav

- Moln distributions platsen har stöd för alla Windows-versioner som visas i [operativ system som stöds för klienter och enheter](../configs/supported-operating-systems-for-clients-and-devices.md).  

- En administratör distribuerar följande typer av program varu innehåll som stöds:  
  - Program
  - Paket
  - Uppgraderings paket för operativ system
  - Programuppdateringar från tredje part  

    > [!Important]  
    > - Medan Configuration Manager-konsolen inte blockerar distributionen av Microsoft-programuppdateringar till en moln distributions plats, betalar du Azure-kostnader för att lagra innehåll som klienterna inte använder. Internetbaserade klienter får alltid Microsoft-program uppdaterings innehåll från moln tjänsten Microsoft Update. Distribuera inte program uppdateringar från Microsoft till en moln distributions plats.
    > - När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** [klienten](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) är aktive rad. <!--6598587--> 

- Från och med version 1806 konfigurerar du en mottagar distributions plats att använda en moln distributions plats som källa. Mer information finns i [om käll distributions platser](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Distributionsinställningar

- **Hämta innehåll lokalt vid behov genom att köra aktivitetssekvensen**. Från och med version 1910 kan aktivitetssekvensen Ladda ned paket på begäran från en innehålls aktive rad CMG eller en moln distributions plats. Den här ändringen ger ytterligare flexibilitet för distributioner av Windows 10 på plats till Internet-baserade enheter.

- **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**. I Configuration Manager version 1906 och tidigare fungerar andra alternativ som **Hämta innehåll lokalt när det behövs av aktivitetssekvensen som körs** inte i det här scenariot. Motorn för aktivitetssekvenser kan inte ladda ned innehåll från en moln källa. Den Configuration Manager klienten måste ladda ned innehållet från moln källan innan aktivitetssekvensen startas. Du kan fortfarande använda det här alternativet i version 1910 om det behövs för att uppfylla dina krav.

- En moln distributions plats har inte stöd för paket distributioner med alternativet att **köra program från distributions platsen**. Använd distributions alternativet för att **Ladda ned innehåll från distributions platsen och kör lokalt**.  

### <a name="limitations"></a>Begränsningar  

- Du kan inte använda en moln distributions plats för PXE-eller multicast-aktiverade distributioner.  

- En moln distributions plats har inte stöd för App-V streaming-program.  

- Det går inte att [Förinstallera innehåll](manage-network-bandwidth.md#BKMK_PrestagingContent) på en moln distributions plats. Distributions hanteraren för den primära plats som hanterar moln distributions platsen överför allt innehåll.  

- Du kan inte konfigurera en moln distributions plats som en mottagar distributions plats.  


## <a name="cost"></a><a name="bkmk_cost"></a>Kostnader

<!--501018-->
> [!IMPORTANT]  
> Följande kostnads information är endast avsedd för uppskattnings syfte. Din miljö kan ha andra variabler som påverkar den totala kostnaden för att använda en moln distributions plats.  

Configuration Manager innehåller följande alternativ för att kontrol lera kostnader och övervaka data åtkomst:  

- Kontrol lera och övervaka mängden innehåll som du lagrar i en moln tjänst. Mer information finns i [övervaka moln distributions platser](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Konfigurera Configuration Manager som varnar dig när tröskelvärden för klient hämtningar uppfyller eller överskrider månads gränserna. Mer information finns i [varningar om tröskelvärden för data överföring](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- För att minska antalet data överföringar från moln distributions platser av klienter kan du använda någon av följande tekniker för peer-cachelagring:  
  - Configuration Manager peer-cache
  - Windows BranchCache
  - Leverans optimering för Windows 10  

    Mer information finns i [grundläggande begrepp för innehålls hantering](fundamental-concepts-for-content-management.md).  

### <a name="components"></a>Komponenter

En moln distributions plats använder följande Azure-komponenter, som debiteras för Azure-prenumerations kontot:  

> [!Tip]  
> Från och med version 1806 kan Cloud Management Gateway också hantera innehåll till klienter. Den här funktionen minskar kostnaden genom att konsolidera de virtuella Azure-datorerna. Mer information finns i [kostnad för Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Virtuell dator

- Moln distributions platsen använder Azure Cloud Services som plattform som en tjänst (PaaS). Den här tjänsten använder virtuella datorer (VM) som ådrar sig beräknings kostnader.  

- Varje punkt tjänst för moln distribution använder två virtuella standard a0-datorer.  

- Se [pris Kalkylatorn för Azure](https://azure.microsoft.com/pricing/calculator/) för att hjälpa till att fastställa potentiella kostnader.

    > [!NOTE]  
    > Kostnaderna för virtuella datorer varierar beroende på region.

#### <a name="outbound-data-transfer"></a>Utgående data överföring

- Alla data flöden i Azure är kostnads fria (ingångs-eller uppladdning). Distribution av innehåll från platsen till moln distributions platsen laddas upp till Azure.  

- Avgifterna baseras på data som flödar ut från Azure (utgående eller hämtning). Moln distributions platsen data flöden utanför Azure består av det program varu innehåll som klienterna laddar ned.  

- Mer information finns i [övervaka moln distributions platser](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Se [pris informationen för Azure bandbredd](https://azure.microsoft.com/pricing/details/bandwidth/) för att hjälpa till att fastställa potentiella kostnader. Prissättningen för data överföring är på nivå. Desto mer du använder, desto mindre du betalar per Gigabyte.  

#### <a name="content-storage"></a>Innehålls lagring

- Internetbaserade klienter får Microsoft program uppdaterings innehåll från Microsoft Update moln tjänsten utan kostnad. Distribuera inte distributions paket för program uppdatering med Microsoft-programuppdateringar till en moln distributions plats. Annars debiteras du data lagrings kostnader för innehåll som klienterna aldrig använder.  

- Moln distributions platser använder följande standard-blob-lagring beroende på distributions modellen:  

    - En Azure Resource Manager distribution använder Azure lokalt redundant lagring (LRS). Den här ändringen minskar kostnaden för lagrings kontot. Den klassiska distributionen använde inte ytterligare funktioner i GRS. Mer information finns i [Lokalt Redundant lagring](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - En klassisk distribution med Configuration Manager version 1810 eller tidigare använder Azure Geo-redundant lagring (GRS). Mer information finns i [Geo-redundant lagring](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Andra kostnader

- Varje moln tjänst har en dynamisk IP-adress. Varje distinkt distributions plats i molnet använder en ny dynamisk IP-adress. Att lägga till ytterligare virtuella datorer per moln tjänst ökar inte dessa adresser.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a>Portar och data flöde

Det finns två primära data flöden för moln distributions platsen:  

- Plats servern ansluter till Azure för att konfigurera punkt tjänsten för moln distribution  

- En klient ansluter till moln distributions platsen för att ladda ned innehåll  

### <a name="site-server-to-azure"></a>Plats Server till Azure

Du behöver inte öppna några inkommande portar till ditt lokala nätverk. Plats servern initierar all kommunikation med Azure och moln distributions platsen för att distribuera, uppdatera och hantera moln tjänsten. Plats servern måste skapa utgående anslutningar till Microsoft-molnet. Den här åtgärden motsvarar att installera distributionsplatsens platssystemroll på en viss plats.  

### <a name="client-to-cloud-distribution-point"></a>Distributions plats för klient till moln

Du behöver inte öppna några inkommande portar till ditt lokala nätverk. Internetbaserade klienter kommunicerar direkt med Azure-tjänsten. Klienter i det interna nätverket som använder en moln distributions plats måste ansluta till Microsoft-molnet.

Mer information om prioritet för innehålls platser och om intranätbaserade klienter använder en moln distributions plats finns i [innehålls källans prioritet](fundamental-concepts-for-content-management.md#content-source-priority).

När en klient använder en moln distributions plats som en innehålls plats:  

1. Hanterings platsen ger klienten en åtkomsttoken tillsammans med listan över innehålls källor. Denna token är giltig i 24 timmar och ger klienten åtkomst till moln distributions platsen.  

2. Hanterings platsen svarar på klientens plats förfrågan med **tjänstens FQDN** för moln distributions platsen. Den här egenskapen är samma som nätverks namnet för certifikatet för serverautentisering.  

    Om du använder ditt domän namn, till exempel WallaceFalls.contoso.com, försöker klienten först matcha detta fullständiga domän namn. Du behöver ett CNAME-alias i din domäns Internet-riktade DNS för att klienter ska kunna matcha namnet på Azure-tjänsten, till exempel: WallaceFalls.cloudapp.net.  

3. Klienten löser nästa Azure-tjänst namn, till exempel WallaceFalls.cloudapp.net, till en giltig IP-adress. Detta svar bör hanteras av Azures DNS.  

4. Klienten ansluter till moln distributions platsen. Azure load balanserar anslutningen till en av de virtuella dator instanserna. Klienten autentiserar sig själv med hjälp av åtkomsttoken.  

5. Moln distributions platsen autentiserar klientens åtkomsttoken och ger sedan klienten den exakta innehålls platsen i Azure Storage.  

6. Om klienten litar på moln distributions platsens certifikat för serverautentisering ansluter den till Azure Storage för att hämta innehållet.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a>Prestanda och skalning

<!--494872-->

Tänk på följande faktorer när du använder en distributions plats design:  

- Antal samtidiga klient anslutningar
- Storleken på det innehåll som klienterna laddar ned
- Den tids längd som tillåts för att uppfylla dina affärs behov

Beroende på din [topologis design](#bkmk_topology), om klienterna har möjlighet att använda fler än en moln distributions plats för ett angivet innehåll, så slumpar de naturligt mellan dessa moln tjänster. Om du bara distribuerar en viss typ av innehåll till en enda moln distributions plats och ett stort antal klienter försöker att ladda ned det här innehållet på samma gång, placerar den här aktiviteten en högre belastning på den enskilda moln distributions platsen. Att lägga till ytterligare en moln distributions plats innehåller också en separat Azure Storage-tjänst. Mer information om hur klienten kommunicerar med moln distributions platsens komponenter och laddar ned innehåll finns i [portar och data flöde](#bkmk_dataflow).  

Moln distributions platsen använder två virtuella Azure-datorer som klient delen i Azure Storage. Den här standard distributionen uppfyller de flesta kundernas behov. I vissa extrema fall, med ett stort antal samtidiga klient anslutningar (t. ex. 150 000-klienter), kan bearbetnings kapaciteten för de virtuella Azure-datorerna inte hålla sig på klient begär Anden. Du kan inte ändra storlek på de virtuella Azure-datorer som används för moln distributions platsen. Du kan inte konfigurera antalet virtuella dator instanser för moln distributions platsen i Configuration Manager, om det behövs, konfigurera om moln tjänsten i Azure Portal. Lägg antingen till fler VM-instanser manuellt eller konfigurera tjänsten för automatisk skalning.

> [!Important]  
> När du uppdaterar Configuration Manager distribuerar webbplatsen om moln tjänsten. Om du konfigurerar om moln tjänsten manuellt i Azure Portal återställs antalet instanser till standardvärdet för två.  

Azure Storage-tjänsten stöder 500-begäranden per sekund för en enskild fil. Prestandatest av en distributions plats med en enda distributions plats som stöds av en enskild 100-MB-fil till 50 000-klienter på 24 timmar.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a>Intyg  

Beroende på moln distributions platsens design behöver du ett eller flera digitala certifikat.  

### <a name="general-information"></a>Allmän information

<!--SCCMDocs issue #779-->
Certifikat för moln distributions platser har stöd för följande konfigurationer:  

- 4096-bitars nyckel längd

- Version 3-certifikat. Mer information finns i [Översikt över CNG-certifikat](../network/cng-certificates-overview.md).  

- Från och med version 1802 när du konfigurerar Windows med följande princip: **system kryptografi: Använd FIPS-kompatibla algoritmer för kryptering, hashing och signering**  

- Från och med version 1802, stöd för TLS 1,2. Mer information finns i [teknisk referens för kryptografiska kontroller](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Certifikat för serverautentisering

*Detta certifikat krävs för alla distributioner av distributions platser i molnet.*

Mer information finns i [certifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)för serverautentisering och följande underavsnitt om det behövs:  

- CMG betrodda rot certifikat till klienter
- Certifikat för serverautentisering som utfärdats av en offentlig Provider
- Certifikat för serverautentisering som utfärdats från företags-PKI

Moln distributions platsen använder den här typen av certifikat på samma sätt som Cloud Management Gateway. Klienterna måste också ha förtroende för det här certifikatet. För att minska komplexiteten rekommenderar Microsoft att du använder ett certifikat som utfärdats av en offentlig leverantör.

Om du inte använder ett jokertecken kan du inte återanvända samma certifikat. Varje instans av moln distributions platsen och Cloud Management Gateway kräver ett unikt certifikat för serverautentisering.

Mer information om hur du skapar det här certifikatet från en PKI finns i [distribuera tjänst certifikatet för moln distributions platser](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Hanterings certifikat för Azure

*Detta certifikat krävs för klassiska tjänst distributioner. Det krävs inte för Azure Resource Manager-distributioner.*

> [!Important]  
> Från och med Configuration Manager version 1806 använder du **Azure Resource Manager** distributions modell. Det kräver inte detta hanterings certifikat.  
>
> Den klassiska distributions metoden är inaktuell från och med version 1810.  
>
> Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av moln distributions platsen. Detta certifikat krävs inte i Configuration Manager version 1902 eller senare.<!-- 3605704 -->

Om du använder den klassiska Azure-distributions metoden med Configuration Manager version 1810 eller tidigare, behöver du ett **hanterings certifikat för Azure**. Mer information finns i avsnittet certifikat för [Azure Management-certifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) i artikeln Cloud Management Gateway certificates. Den Configuration Manager plats servern använder det här certifikatet för att autentisera med Azure för att skapa och hantera den klassiska distributionen.  

Om du vill minska komplexiteten använder du samma Azure-hanterings certifikat för alla klassiska distributioner av moln distributions platser och moln hanterings-gatewayer, över alla Azure-prenumerationer och alla Configuration Manager-platser.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Vanliga frågor och svar

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Behöver en klient ett certifikat för att ladda ned innehåll från en distributions plats i molnet?

Det krävs inget certifikat för klientautentisering. Klienten måste lita på certifikatet för serverautentisering som används av moln distributions platsen. Om certifikatet har utfärdats av en offentlig certifikat leverantör, innehåller de flesta Windows-enheter redan betrodda rot certifikat för dessa leverantörer. Om du utfärdade ett certifikat för serverautentisering från din organisations PKI måste dina klienter lita på utfärdande certifikat i hela kedjan. Den här kedjan innehåller rot certifikat utfärdaren och alla mellanliggande certifikat utfärdare. Beroende på din PKI-design kan det här certifikatet medföra ytterligare komplexitet för distributionen av moln distributions platsen. För att undvika denna komplexitet rekommenderar Microsoft att du använder en offentlig certifikat leverantör som dina klienter redan litar på.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Kan mina lokala klienter använda en moln distributions plats?

Ja. Om du vill att klienter i det interna nätverket ska använda en moln distributions plats måste den finnas i samma gränser grupp som-klienterna. Klienter prioriterar moln distributions platser sist i listan med innehålls källor, eftersom det finns en kostnad för att ladda ned innehåll från Azure. Därför används en moln distributions plats vanligt vis som en återställnings källa för intranätbaserade klienter. Om du vill ha en moln-och första design, kan du utforma dina gränser grupper därefter. Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>Behöver jag Azure ExpressRoute?

Med [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) kan du utöka ditt lokala nätverk till Microsoft-molnet. ExpressRoute eller andra sådana virtuella nätverks anslutningar krävs inte för den Configuration Manager moln distributions platsen.  

Om din organisation använder ExpressRoute isolerar du Azure-prenumerationen för moln distributions platsen från prenumerationen som använder ExpressRoute. Den här konfigurationen säkerställer att moln distributions platsen inte har anslutits av misstag på det här sättet.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Behöver jag underhålla Azure Virtual Machines?

Inget underhåll krävs. Designen av moln distributions platsen använder Azure Platform as a Service (PaaS). Med den prenumeration du anger skapar Configuration Manager nödvändiga virtuella datorer, lagring och nätverk. Azure säkrar och uppdaterar de virtuella datorerna. De här virtuella datorerna är inte en del av din lokala miljö, som är fallet med IaaS (Infrastructure as a Service). Moln distributions platsen är en PaaS som utökar din Configuration Manager miljö till molnet. Mer information finns i [säkerhets fördelarna med en PaaS Cloud Service-modell](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Använder moln distributions platsen Azure CDN?

Azure Content Delivery Network (CDN) är en global lösning för att snabbt leverera innehåll med hög bandbredd genom att cachelagra innehållet på strategiskt placerade fysiska noder över hela världen. Mer information finns i [Vad är Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview).

Den Configuration Manager moln distributions platsen stöder för närvarande inte Azure CDN.


## <a name="next-steps"></a>Nästa steg

[Installera moln distributions platser](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
