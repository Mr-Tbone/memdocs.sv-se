---
title: Planera för en molnhanteringsgateway
titleSuffix: Configuration Manager
description: Planera och utforma Cloud Management Gateway (CMG) för att förenkla hanteringen av Internetbaserade klienter.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d6165678331811f4b04e8b1f540f3dcbb7f015d
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502263"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planera för Cloud Management Gateway i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1101764-->
CMG (Cloud Management Gateway) är ett enkelt sätt att hantera Configuration Manager-klienter på Internet. Genom att distribuera CMG som en moln tjänst i Microsoft Azure kan du hantera traditionella klienter som är centrala på Internet utan ytterligare lokal infrastruktur. Du behöver inte heller exponera din lokala infrastruktur på Internet.

> [!NOTE]
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

När du har upprättat kraven, består CMG av följande tre steg i Configuration Manager-konsolen:

1. Distribuera CMG Cloud service till Azure.
2. Lägg till anslutnings punkt rollen CMG.
3. Konfigurera plats-och plats rollerna för tjänsten.
När de har distribuerats och kon figurer ATS får klienterna sömlös åtkomst till lokala plats roller oavsett om de finns på intranätet eller Internet.

Den här artikeln ger grundläggande kunskaper om CMG, hur de passar i din miljö och hur du planerar implementeringen.

## <a name="scenarios"></a>Scenarier

Det finns flera scenarier för vilka en CMG är fördelaktig. Följande scenarier är några av de vanligaste:  

- Hantera traditionella Windows-klienter med Active Directory domänanslutna identitet. Dessa klienter omfattar Windows 8,1 och Windows 10. Den använder PKI-certifikat för att skydda kommunikations kanalen. Hanterings aktiviteter är:  

  - Program uppdateringar och Endpoint Protection
  - Inventerings-och klient status
  - Kompatibilitetsinställningar
  - Program varu distribution till enheten
  - Aktivitetssekvens för uppgradering av Windows 10 på plats

- Hantera traditionella Windows 10-klienter med modern identitet, antingen hybrid eller rena molnbaserad domänanslutna med Azure Active Directory (Azure AD). Klienter använder Azure AD för att autentisera snarare än PKI-certifikat. Att använda Azure AD är enklare att konfigurera, konfigurera och underhålla än mer komplexa PKI-system. Hanterings aktiviteter är samma som det första scenariot, samt:  

  - Program varu distribution till användaren  

- Installera Configuration Manager-klienten på Windows 10-enheter via Internet. Med hjälp av Azure AD kan enheten autentisera till CMG för klient registrering och tilldelning. Du kan installera klienten manuellt eller använda en annan metod för program varu distribution, till exempel Microsoft Intune.  

- Ny enhets etablering med samhantering. När du automatiskt registrerar befintliga klienter krävs CMG inte för samhantering. Det krävs för nya enheter som inbegriper Windows autopilot, Azure AD, Microsoft Intune och Configuration Manager. Mer information finns i [sökvägar till samhantering](../../../../comanage/quickstart-paths.md).

### <a name="specific-use-cases"></a>Vissa användnings fall

I de här scenarierna kan följande angivna enhets användnings fall gälla:

- Nätverks växlings enheter, till exempel bärbara datorer  

- Fjärr-och avdelnings kontors enheter som är billigare och mer effektiva att hantera via Internet än i ett WAN-nätverk eller via en VPN-anslutning.  

- Fusioner och förvärv, där det är enkelt att ansluta enheter till Azure AD och hantera via en CMG.  

- Arbets grupps klienter. Dessa enheter kan kräva ytterligare konfiguration, t. ex. certifikat.<!-- SCCMDocs#1925 -->

    Från och med version 2002 stöder Configuration Manager token-baserad autentisering, som kan hjälpa till med hantering av fjärran sluten arbets grupps klienter. Mer information finns i [tokenbaserad autentisering för CMG](../../deploy/deploy-clients-cmg-token.md).

> [!Important]
> Som standard tar alla klienter emot en princip för en CMG och börjar använda den när de blir Internet-baserade. Beroende på vilket scenario och vilket användnings fall som gäller för din organisation, kan du behöva omfångs användningen av CMG. Mer information finns i klient inställningen [aktivera klienter för att använda en moln hanterings-Gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) .

## <a name="topology-design"></a>Topologins design

### <a name="cmg-components"></a>CMG-komponenter

Distribution och drift av CMG innehåller följande komponenter:  

- **Moln tjänsten CMG** i Azure autentiserar och vidarebefordrar Configuration Manager klient begär anden till CMG-anslutnings punkten.  

- **CMG anslutnings punktens** plats system roll möjliggör en konsekvent och hög prestanda anslutning från det lokala nätverket till CMG-tjänsten i Azure. Den publicerar också inställningar till CMG, inklusive anslutnings information och säkerhets inställningar. Anslutnings punkten för CMG vidarebefordrar klient begär Anden från CMG till lokala roller enligt URL-mappningar.

- [**Tjänst anslutnings punktens**](../../../servers/deploy/configure/about-the-service-connection-point.md) plats system roll kör Cloud Service Manager-komponenten som hanterar alla CMG-distributions uppgifter. Dessutom övervakar och rapporterar tjänstens hälsa och loggnings information från Azure AD. Kontrol lera att tjänst anslutnings punkten är i [onlineläge](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- **Hanterings** platsens plats system roll tjänster klient begär Anden per normal.

- Klient begär Anden för plats system roll tjänster för **program uppdaterings platsen** per normal.

    > [!NOTE]
    > Storleks vägledningen för hanterings platser och program uppdaterings platser påverkar inte om de fungerar lokalt eller på Internetbaserade klienter. Mer information finns i [storlek och skalnings nummer](../../../plan-design/configs/size-and-scale-numbers.md#management-point).

- **Internetbaserade klienter** ansluter till CMG för att komma åt lokala Configuration Manager-komponenter.

- CMG använder en **CERTIFIKATBASERAD https** -webbtjänst för att skydda nätverkskommunikation med klienter.  

- Internetbaserade klienter använder **PKI-certifikat eller Azure AD** för identitet och autentisering.  

- En [**distributions plats i molnet**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) ger till gång till innehåll till Internetbaserade klienter efter behov.  

  - En CMG kan också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. Mer information finns i [ändra en CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Skapa CMG med hjälp av en **Azure Resource Manager-distribution**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en [resurs grupp](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). När du distribuerar CMG med Azure Resource Manager använder platsen Azure Active Directory (Azure AD) för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure.  

> [!NOTE]
> Den här funktionen aktiverar inte stöd för Azure Cloud Service-leverantörer (CSP). CMG-distributionen med Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av KRYPTOGRAFIPROVIDERn. Mer information finns i [tillgängliga Azure-tjänster i Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).

Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av Cloud Management Gateway. Befintliga distributioner fortsätter att fungera.<!-- 3605704 -->

I Configuration Manager version 1810 och tidigare tillhandahåller guiden CMG fortfarande alternativet för en **klassisk tjänst distribution** med ett hanterings certifikat för Azure. Azure Resource Manager distributions modell rekommenderas för alla nya CMG-instanser för att förenkla distributionen och hanteringen av resurser. Distribuera om möjligt Befintliga CMG-instanser via Resource Manager. Mer information finns i [ändra en CMG](setup-cloud-management-gateway.md#modify-a-cmg).

> [!IMPORTANT]
> Den klassiska tjänst distributionen i Azure är föråldrad för användning i Configuration Manager. Version 1810 är den sista som stöd för att skapa dessa Azure-distributioner. Den här funktionen kommer att tas bort i en framtida Configuration Manager version.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Hierarkins design

Skapa CMG på platsen på den översta nivån i hierarkin. Om det är en central administrations plats skapar du CMG-kopplings punkter på underordnade primära platser. Cloud Service Manager-komponenten finns på tjänst anslutnings punkten, som också finns på den centrala administrations webbplatsen. Den här designen kan dela tjänsten på olika primära platser om det behövs.

Du kan skapa flera CMG-tjänster i Azure och du kan skapa flera CMG-anslutnings punkter. Flera CMG anslutnings punkter ger belastnings utjämning av klient trafik från CMG till lokala roller.

Från och med version 1902 kan du associera en CMG med en avgränsnings grupp. Den här konfigurationen gör det möjligt för klienter att default eller återgå till CMG för klient kommunikation baserat på [gränser grupp relationer](../../../servers/deploy/configure/boundary-groups.md). Det här beteendet är särskilt användbart i avdelnings kontor och VPN-scenarier. Du kan dirigera klient trafiken bort från dyra och långsamma WAN-länkar för att i stället använda snabbare tjänster i Microsoft Azure.<!--3640932-->

> [!NOTE]
> Internetbaserade klienter omfattas inte av någon avgränsnings grupp.
>
> I Configuration Manager version 1810 och tidigare hamnar CMG inte i någon avgränsnings grupp.

Andra faktorer, till exempel antalet klienter som ska hanteras, påverkar även din CMG-design. Mer information finns i [prestanda och skalning](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Exempel 1: fristående primär plats

Contoso har en fristående primär plats i ett lokalt Data Center på sitt huvud kontor i New York City.

- De skapar en CMG i regionen USA, östra Azure för att minska nätverks fördröjningen.
- De skapar två CMG anslutnings punkter, både länkade till den enskilda CMG-tjänsten.  

När klienter växlar till Internet, kommunicerar de med CMG i Azure-regionen USA, östra. CMG vidarebefordrar den här kommunikationen genom båda kopplings punkterna för CMG.

#### <a name="example-2-hierarchy"></a>Exempel 2: hierarki

Fourth kaffe har en central administrations plats i ett lokalt Data Center i sitt huvud kontor i Seattle. En primär plats finns i samma data Center och den andra primära platsen finns på sitt huvudsakliga Europeiska kontor i Paris.

- På den centrala administrations platsen skapar de en CMG-tjänst i regionen USA, västra Azure. De skalar antalet virtuella datorer för den förväntade belastningen av centrala klienter i hela hierarkin.
- På den Seattle-baserade primära platsen skapar de en CMG kopplings punkt som är länkad till den enskilda CMG.
- På den Paris-baserade primära platsen skapar de en CMG kopplings punkt som är kopplad till den enskilda CMG.

När klienter växlar till Internet, kommunicerar de med CMG i Azure-regionen USA, västra. CMG vidarebefordrar denna kommunikation till CMG-anslutnings punkten på klientens tilldelade primära plats.

> [!TIP]
> Du behöver inte distribuera fler än en moln hanterings-Gateway för syftet med geolokalisering. Configuration Manager-klienten påverkas i huvudsak av den små svars tiden som kan uppstå med moln tjänsten, även om den är geografiskt avlägsen.

### <a name="test-environments"></a>Test miljöer
<!-- SCCMDocs#1225 -->
Många organisationer har separata miljöer för produktion, testning, utveckling eller kvalitets säkring. När du planerar din CMG-distribution bör du tänka på följande frågor:

- Hur många Azure AD-klienter har din organisation?
  - Finns det en separat klient för testning?
  - Är användar-och enhets identiteter i samma klient organisation?

- Hur många prenumerationer finns i varje klient?
  - Finns det prenumerationer som är speciella för testning?

Configuration Manager Azure-tjänsten för **moln hantering** stöder flera klienter. Flera Configuration Manager-platser kan ansluta till samma klient organisation. En enda plats kan distribuera flera CMG-tjänster till olika prenumerationer. Flera platser kan distribuera CMG-tjänster till samma prenumeration. Configuration Manager ger flexibilitet beroende på din miljö och dina affärs behov.

Mer information finns i följande vanliga frågor och svar: [användar kontona måste finnas i samma Azure AD-klient som klienten som är kopplad till den prenumeration som är värd för CMG-moln tjänsten?](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>Krav

- En **Azure-prenumeration** som värd för CMG.

    > [!IMPORTANT]
    > CMG stöder inte prenumerationer med en Azure Cloud Service Provider (CSP).<!-- MEMDocs#320 -->

- Ditt användar konto måste vara en **fullständig administratörs** -eller **infrastruktur administratör** i Configuration Manager.<!-- SCCMDocs#2146 -->

- En **Azure-administratör** behöver delta i den första skapandet av vissa komponenter, beroende på din design. Den här personen kan vara samma som Configuration Manager administratör eller separat. Om den är separat behöver den inte behörighet i Configuration Manager.

  - Om du vill distribuera CMG behöver du en **prenumerations ägare**
  - Om du vill integrera-platsen med Azure AD för att distribuera CMG med hjälp av Azure Resource Manager behöver du en **Global administratör**

- Minst en lokal Windows Server som värd för **CMG-anslutnings punkten**. Du kan samplacera rollen med andra Configuration Manager plats system roller.  

- **Tjänst anslutnings punkten** måste vara i [onlineläge](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- Integrering med **Azure AD** för att distribuera tjänsten med Azure Resource Manager. Mer information finns i [Konfigurera Azure-tjänster](../../../servers/deploy/configure/azure-services-wizard.md).  

- Ett [**certifikat**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) för SERVERAUTENTISERING för CMG.  

- **Andra certifikat** kan krävas, beroende på KLIENTens OS-version och Authentication-modell. Mer information finns i [CMG-certifikat](certificates-for-cloud-management-gateway.md).  

    När du använder alternativet plats för att **använda Configuration Manager-genererade certifikat för HTTP-plats system**kan hanterings platsen vara http. Mer information finns i [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md).

- Om du använder den klassiska distributions metoden i Azure i Configuration Manager version 1810 eller tidigare måste du använda ett [**hanterings certifikat för Azure**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt).  

    > [!TIP]  
    > Använd **Azure Resource Manager** distributions modell. Det kräver inte detta hanterings certifikat.
    >
    > Den klassiska distributions metoden är inaktuell från och med version 1810.  

- Klienterna måste använda **IPv4**.  

## <a name="specifications"></a>Specifikationer

- Alla Windows-versioner som visas i [operativ system som stöds för klienter och enheter](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) stöds för CMG.  

- CMG stöder endast hanterings platsen och program uppdaterings platsens roller.  

- CMG stöder inte klienter som bara kommunicerar med IPv6-adresser.<!--495606-->  

- Program uppdaterings platser som använder en utjämning av nätverks belastning fungerar inte med CMG. <!--505311-->  

- CMG-distributioner som använder Azures resurs modell aktiverar inte stöd för Azure Cloud Service Providers (CSP). CMG-distributionen med Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av KRYPTOGRAFIPROVIDERn. Mer information finns i [Azure-tjänster som är tillgängliga i Azure CSP-programmet](https://docs.microsoft.com/partner-center/azure-plan-available).

### <a name="support-for-configuration-manager-features"></a>Stöd för Configuration Manager funktioner

I följande tabell visas CMG-stöd för Configuration Manager-funktioner:

|Funktion  |Support  |
|---------|---------|
| Programuppdateringar     | ![Stöds](media/green_check.png) |
| Endpoint Protection     | ![](media/green_check.png) <sup> [Anmärkning 1](#bkmk_note1) som stöds</sup> |
| Inventering av maskin- och programvara     | ![Stöds](media/green_check.png) |
| Klient status och meddelanden     | ![Stöds](media/green_check.png) |
| Kör skript     | ![Stöds](media/green_check.png) |
| CMPivot     | ![Stöds](media/green_check.png) |
| Kompatibilitetsinställningar     | ![Stöds](media/green_check.png) |
| Klient installation<br>(med [Azure AD-integrering](../../deploy/deploy-clients-cmg-azure.md)) | ![Stöds](media/green_check.png) |
| Klient installation<br>(med [token-autentisering](../../deploy/deploy-clients-cmg-token.md)) | ![Stöds](media/green_check.png) (2002) |
| Program varu distribution (enhets riktad)     | ![Stöds](media/green_check.png) |
| Program varu distribution (användar mål, krävs)<br>(med Azure AD-integrering)     | ![Stöds](media/green_check.png) |
| Program varu distribution (användar mål, tillgänglig)<br>([alla krav](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Stöds](media/green_check.png) |
| [Aktivitetssekvens för uppgradering av Windows 10 på plats](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) | ![Stöds](media/green_check.png) |
| Aktivitetssekvenser som inte använder start avbildningar och distribueras med ett alternativ: **Ladda ned allt innehåll lokalt innan aktivitetssekvensen startas** | ![Stöds](media/green_check.png) |
| Aktivitetssekvenser som inte använder start avbildningar med [antingen nedladdnings alternativet](../../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg) | ![Stöds](media/green_check.png) (1910)|
| Ett annat scenario för aktivitetssekvenser     | ![Stöds inte](media/Red_X.png) |
| Klient-push     | ![Stöds inte](media/Red_X.png) |
| Automatisk platstilldelning     | ![Stöds inte](media/Red_X.png) |
| Begär Anden om program varu godkännande     | ![Stöds inte](media/Red_X.png) |
| Configuration Manager-konsolen     | ![Stöds inte](media/Red_X.png) |
| Fjärrverktyg     | ![Stöds inte](media/Red_X.png) |
| Rapport webbplats     | ![Stöds inte](media/Red_X.png) |
| Wake on LAN     | ![Stöds inte](media/Red_X.png) |
| Mac-, Linux-och UNIX-klienter     | ![Stöds inte](media/Red_X.png) |
| Peer-cache     | ![Stöds inte](media/Red_X.png) |
| Lokal MDM     | ![Stöds inte](media/Red_X.png) |
| BitLocker-hantering     | ![Stöds inte](media/Red_X.png) |

|Nyckel|
|--|
|![Stöds](media/green_check.png) = Den här funktionen stöds med CMG av alla versioner av Configuration Manager som stöds  |
|![Stöds ](media/green_check.png) (*YYMM*) = den här funktionen stöds med CMG från och med *version YYMM* av Configuration Manager  |
|![Stöds inte](media/Red_X.png) = Den här funktionen stöds inte med CMG |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a>Anmärkning 1: stöd för Endpoint Protection
<!-- 4350561 -->
För domänanslutna enheter som använder Endpoint Protection-principen måste de ha åtkomst till domänen. Enheter med frekvent åtkomst till det interna nätverket kan uppleva fördröjningar i tillämpningen av Endpoint Protection-principer. Om du kräver att enheterna omedelbart tillämpar Endpoint Protection-principer när de får den, bör du överväga något av följande alternativ:

- Använd Co-Management och Byt [Endpoint Protection arbets belastning](../../../../comanage/workloads.md#endpoint-protection) till Intune och hantera [Microsoft Defender Antivirus](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus) från molnet.

- Använd [konfigurations objekt](../../../../compliance/deploy-use/create-configuration-items.md) i stället för de interna [principerna för program mot skadlig kod](../../../../protect/deploy-use/endpoint-antimalware-policies.md) för att tillämpa Endpoint Protection-principen.

## <a name="cost"></a>Kostnad

> [!IMPORTANT]  
> Följande kostnads information är endast avsedd för uppskattnings syfte. Din miljö kan ha andra variabler som påverkar den totala kostnaden för att använda CMG.

CMG använder följande Azure-komponenter, som debiteras för Azure-prenumerations kontot:

### <a name="virtual-machine"></a>Virtuell dator

- CMG använder Azure Cloud Services som plattform som en tjänst (PaaS). Den här tjänsten använder virtuella datorer (VM) som ådrar sig beräknings kostnader.  

- CMG använder en standard a2 v2-VM.  

- Du väljer hur många VM-instanser som stöder CMG. En är standard och 16 är Max värdet. Det här antalet anges när du skapar CMG och kan ändras efteråt för att skala tjänsten efter behov.

- Mer information om hur många virtuella datorer du behöver för att stödja dina klienter finns i [prestanda och skalning](#performance-and-scale).

- Se [pris Kalkylatorn för Azure](https://azure.microsoft.com/pricing/calculator/) för att hjälpa till att fastställa potentiella kostnader.

    > [!NOTE]  
    > Kostnaderna för virtuella datorer varierar beroende på region.

### <a name="outbound-data-transfer"></a>Utgående data överföring

- Avgifterna baseras på data som flödar ut från Azure (utgående eller hämtning). Alla data flöden i Azure är kostnads fria (ingångs-eller uppladdning). CMG data flöden från Azure inkluderar princip för klienten, klient meddelanden och klient svar som vidarebefordras av CMG till platsen. Dessa svar omfattar inventerings rapporter, status meddelanden och kompatibilitetsstatus.  

- Även om det inte finns några klienter som kommunicerar med en CMG, orsakar en viss bakgrunds kommunikation nätverks trafik mellan CMG och den lokala platsen.  

- Visa den **utgående data överföringen (GB)** i Configuration Manager-konsolen. Mer information finns i [övervaka klienter på CMG](monitor-clients-cloud-management-gateway.md).  

- Se [pris informationen för Azure bandbredd](https://azure.microsoft.com/pricing/details/bandwidth/) för att hjälpa till att fastställa potentiella kostnader. Prissättningen för data överföring är på nivå. Desto mer du använder, desto mindre du betalar per Gigabyte.  

- *I uppskattnings syfte*förväntar vi cirka 100-300 MB per klient per månad för Internetbaserade klienter. Den lägre uppskattningen är för en standard klient konfiguration. Den övre uppskattningen är för en mer aggressiv klient konfiguration. Den faktiska användningen kan variera beroende på hur du konfigurerar klient inställningar.  

    > [!NOTE]  
    > Om du utför andra åtgärder, t. ex. distribution av program uppdateringar eller program, ökar mängden utgående data överföring från Azure.

- Internetbaserade klienter får Microsoft program uppdaterings innehåll från Windows Update utan kostnad. Distribuera inte uppdaterings paket med Microsoft Update-innehåll till en moln distributions plats, annars kan du debiteras kostnader för lagring och data utgång.  

- Felaktig konfiguration av CMG-alternativet för att **Verifiera återkallning av klient certifikat** kan orsaka ytterligare trafik från klienter till CMG. Den ytterligare trafiken kan öka de utgående Azure-data, vilket kan öka dina Azure-kostnader.<!-- SCCMDocs#1434 --> Mer information finns i [publicera listan över återkallade certifikat](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>Innehålls lagring

- Internetbaserade klienter får Microsoft program uppdaterings innehåll från Windows Update utan kostnad. Distribuera inte uppdaterings paket med Microsoft Update-innehåll till en moln distributions plats, annars kan du debiteras kostnader för lagring och data utgång.  

- För alla andra nödvändiga innehåll, till exempel program eller program uppdateringar från tredje part, måste du distribuera till en moln distributions plats. För närvarande stöder CMG endast moln distributions platsen för att skicka innehåll till klienter.
   - När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** [klienten](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) är aktive rad. <!--6598587--> 

- Mer information finns i kostnaden för att använda [moln distributions platser](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).  

- En CMG kan också vara en moln distributions plats för att betjäna innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. Mer information finns i [ändra en CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

- CMG använder Azure lokalt redundant lagring (LRS). Mer information finns i [Lokalt Redundant lagring](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

### <a name="other-costs"></a>Andra kostnader

- Varje moln tjänst har en dynamisk IP-adress. Varje distinkt CMG använder en ny dynamisk IP-adress. Om du lägger till ytterligare virtuella datorer per CMG ökas inte dessa adresser.  

## <a name="performance-and-scale"></a>Prestanda och skalning

Mer information om CMG skalning finns i [storlek och skalnings nummer](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg).

Följande rekommendationer kan hjälpa dig att förbättra prestanda för CMG:

- Anslutningen mellan Configuration Manager-klienten och CMG är inte regions medveten. Klient kommunikation påverkas i stor utsträckning av latens/geografisk åtskillnad. Det är inte nödvändigt att distribuera flera CMG i syfte att geo-närhet. Distribuera CMG på platsen på den översta nivån i hierarkin och Lägg till instanser för att öka skalningen.

- För hög tillgänglighet för tjänsten skapar du en CMG med minst två CMG-instanser och två CMG anslutnings punkter per plats.  

- Skala CMG till att stödja fler klienter genom att lägga till fler VM-instanser. Azure Load Balancer styr klient anslutningar till tjänsten.  

- Skapa fler CMG anslutnings punkter för att distribuera belastningen mellan dem. CMG distribuerar trafiken till dess anslutande CMG-anslutnings punkter i en resursallokering.  

- När CMG är under hög belastning med mer än det antal klienter som stöds, hanterar den fortfarande begär Anden, men det kan uppstå en fördröjning.  

> [!NOTE]
> Även om Configuration Manager inte har någon hård gräns för antalet klienter för en CMG anslutnings punkt har Windows Server standard port intervallet 16 384 för TCP. Om en Configuration Manager plats hanterar fler än 16 384 klienter med en enda CMG anslutnings punkt måste du öka gränsen för Windows Server. Alla klienter underhåller en kanal för klient meddelanden, som innehåller en port öppen på CMG-anslutnings punkten. Mer information om hur du använder kommandot netsh för att öka den här gränsen finns [Microsoft Support artikel 929851](https://support.microsoft.com/help/929851).

## <a name="ports-and-data-flow"></a>Portar och data flöde

Du behöver inte öppna några inkommande portar till ditt lokala nätverk. Tjänst anslutnings punkten och CMG anslutnings punkten initierar all kommunikation med Azure och CMG. Dessa två plats system roller måste skapa utgående anslutningar till Microsoft-molnet. Tjänst anslutnings punkten distribuerar och övervakar tjänsten i Azure, och måste därför vara online-läge. Anslutnings punkten CMG ansluter till CMG för att hantera kommunikationen mellan CMG och lokala plats system roller.

Följande diagram är ett grundläggande, konceptuellt data flöde för CMG:

[![CMG data flöde](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. Tjänst anslutnings punkten ansluter till Azure via HTTPS-port 443. Den autentiserar med hjälp av Azure AD eller Azures hanterings certifikat. Tjänst anslutnings punkten distribuerar CMG i Azure. CMG skapar HTTPS-molnet med hjälp av certifikatet för serverautentisering.  

2. Anslutnings punkten CMG ansluter till CMG i Azure över TCP-TLS eller HTTPS. Den håller anslutningen öppen och skapar kanalen för framtida kommunikation på två sätt.  

3. Klienten ansluter till CMG via HTTPS-port 443. Den autentiserar med hjälp av Azure AD eller certifikatet för klientautentisering.  

    > [!NOTE]
    > Om du aktiverar CMG för att hantera innehåll eller använder en moln distributions plats ansluter klienten direkt till Azure Blob Storage via HTTPS-port 443. Mer information finns i [använda en molnbaserad distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).<!-- SCCMDocs#2332 -->

4. CMG vidarebefordrar klient kommunikationen över den befintliga anslutningen till anslutnings punkten för den lokala CMG. Du behöver inte öppna några inkommande brand Väggs portar.  

5. Anslutnings punkten för CMG vidarebefordrar klient kommunikationen till den lokala hanterings platsen och program uppdaterings platsen.  

Mer information när du är värd för innehåll i Azure finns i [använda en molnbaserad distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="required-ports"></a>Portar som krävs

I den här tabellen listas de nätverks portar och protokoll som krävs. *Klienten* är enheten som initierar anslutningen, vilket kräver en utgående port. *Servern* är den enhet som accepterar anslutningen, vilket kräver en inkommande port.

| Klient | Protokoll | Port | Server | Description |
|--------|----------|------|--------|-------------|
| Tjänstanslutningspunkt | HTTPS | 443 | Azure | CMG-distribution |
| CMG kopplings punkt | TCP-TLS | 10140-10155 | CMG-tjänst | Önskat protokoll för att bygga CMG-kanal <sup> [anteckning 1](#bkmk_port-note1)</sup> |
| CMG kopplings punkt | HTTPS | 443 | CMG-tjänst | Återställnings protokoll för att bygga CMG-kanalen till endast en instans av virtuell dator instans <sup> [2](#bkmk_port-note2)</sup> |
| CMG kopplings punkt | HTTPS | 10124-10139 | CMG-tjänst | Reserv protokoll för att bygga CMG-kanalen till två eller flera VM-instanser <sup> [Anmärkning 3](#bkmk_port-note3)</sup> |
| Klient | HTTPS | 443 | CMG | Allmän klient kommunikation |
| Klient | HTTPS | 443 | Blob Storage | Hämta molnbaserad innehåll |
| CMG kopplings punkt | HTTPS eller HTTP | 443 eller 80 | Hanteringsplats | Lokal trafik, Port beror på hanterings platsens konfiguration |
| CMG kopplings punkt | HTTPS eller HTTP | 443 eller 80 | Programuppdateringsplats | Lokal trafik är beroende av konfigurationen av program uppdaterings platsen |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a>Anmärkning 1: CMG TCP-TLS ports för anslutnings punkt

CMG anslutnings punkt försöker först upprätta en TCP-TLS-anslutning med lång livs längd med varje CMG VM-instans. Den ansluter till den första virtuella dator instansen på port 10140. Den andra virtuella dator instansen använder port 10141, upp till 16 på port 10155. En TCP-TLS-anslutning fungerar bäst, men stöder inte Internet-proxy. Om anslutnings punkten för CMG inte kan ansluta via TCP-TLS går den tillbaka till HTTPS-<sup>[anteckning 2](#bkmk_port-note2)</sup>.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a>Anmärkning 2: HTTPS-portar för CMG-anslutning för en virtuell dator

Om anslutnings punkten för CMG inte kan ansluta till CMG via TCP-TLS<sup>[Anmärkning 1](#bkmk_port-note1)</sup>ansluter den till Azure Network Load Balancer via https 443 bara för en VM-instans.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a>Anmärkning 3: CMG HTTPS-portar för två eller flera virtuella datorer

Om det finns två eller flera virtuella dator instanser använder CMG-anslutnings punkten HTTPS 10124 för den första virtuella dator instansen, inte HTTPS 443. Den ansluter till den andra virtuella dator instansen på HTTPS 10125, upp till sextonde HTTPS-port 10139.

### <a name="internet-access-requirements"></a>Krav för Internet-åtkomst

Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, måste du tillåta CMG anslutnings punkt och tjänst anslutnings punkt för att få åtkomst till Internet-slutpunkter.

Mer information finns i [krav för Internet åtkomst](../../../plan-design/network/internet-endpoints.md#bkmk_cloud).

## <a name="next-steps"></a>Nästa steg

- [Certifikat för molnhanteringsgateway](certificates-for-cloud-management-gateway.md)
- [Säkerhet och sekretess för molnhanteringsgateway](security-and-privacy-for-cloud-management-gateway.md)
- [Storlek och skalnings nummer för Cloud Management Gateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Vanliga frågor och svar om Cloud Management Gateway](cloud-management-gateway-faq.md)
- [Konfigurera en molnhanteringsgateway](setup-cloud-management-gateway.md)
