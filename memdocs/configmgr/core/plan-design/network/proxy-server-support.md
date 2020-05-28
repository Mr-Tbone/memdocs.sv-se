---
title: Stöd för proxyserver
titleSuffix: Configuration Manager
description: Lär dig hur Configuration Manager plats system servrar använder proxyservrar.
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 89a2f76f394d3bdf8fd6785429ae0ae60302537a
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802097"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Stöd för proxyserver i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Vissa Configuration Manager plats system servrar kräver anslutning till Internet. Om din miljö kräver Internet trafik för att använda en proxyserver konfigurerar du dessa plats system roller för att använda proxyn.  

- En dator som är värd för en plats system Server stöder en enda konfiguration av proxyservern. Alla plats system roller på den datorn delar samma proxykonfiguration. Om du behöver separata proxyservrar för olika roller eller instanser av en roll placerar du dessa roller på separata plats system servrar.  

- När du konfigurerar nya proxyserverinställningar för en plats system server som redan har en konfiguration av proxyservern skrivs den ursprungliga konfigurationen över.  

- Som standard använder anslutningar till proxy **system** kontot för den dator som är värd för plats system rollen.  

- Om dator kontot inte kan autentiseras kan plats system servern lagra användarautentiseringsuppgifter för att ansluta till proxyservern. Dessa autentiseringsuppgifter är **Server kontot för plats systemets proxyserver**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Plats system roller som använder en proxy

Följande plats system roller ansluter till Internet och kan vid behov använda en proxyserver:  

### <a name="asset-intelligence-synchronization-point"></a>Plats för synkronisering av tillgångsinformation

Den här plats system rollen ansluter till Microsoft och använder en proxyserver-konfiguration på den dator som är värd för Tillgångsinformation-platsen för synkronisering.  

### <a name="cloud-distribution-point"></a>Moln distributions plats

Moln distributions plats rollen körs i Microsoft Azure. Du konfigurerar inte den här plats system rollen för att använda en proxy. Ange proxykonfigurationen på den primära plats servern som hanterar moln distributions platsen.  

För den här konfigurationen måste den primära platsservern:  

- Måste kunna ansluta till Microsoft Azure för att konfigurera, övervaka och distribuera innehåll till moln distributions platsen.  

- Som standard använder datorns **system** konto för att ansluta. Det kan också använda plats systemets proxyserver för proxyserver, om det behövs.  

- Använder Windows webb läsar-API: er.  

### <a name="cloud-management-gateway-connection-point"></a>Anslutning punkt för moln hanterings-Gateway

Cloud Management Gateway (CMG)-anslutnings punkten är en lokal roll som kommunicerar med CMG-tjänsten i Azure. Mer information finns i [Planera för CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="distribution-point"></a>Distributionsplats

<!-- 5856396 -->

Från och med version 2002, om du aktiverar en Configuration Manager distributions plats för Microsoft Connected cache, kan den kommunicera via en oautentiserad proxyserver för Internet åtkomst. Mer information finns i [Microsoft Connected cache](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>Exchange Server-anslutning

Den här plats system rollen ansluter till en Exchange-Server. Den använder en proxyserver-konfiguration på den dator som är värd för Exchange Server-anslutningen.  

### <a name="service-connection-point"></a>Tjänstanslutningspunkt

Den här plats system rollen ansluter till Configuration Manager moln tjänst för att hämta versions uppdateringar för Configuration Manager. Den använder en proxyserver som är konfigurerad på den dator som är värd för tjänst anslutnings punkten.  

### <a name="software-update-point"></a>Programuppdateringsplats

Den här plats system rollen använder proxyn när den ansluter till Microsoft Update för att ladda ned korrigeringar och synkronisera information om uppdateringar. Precis som varje annan plats system roll måste du först konfigurera inställningarna för plats systemets proxy. Konfigurera sedan följande alternativ för program uppdaterings platsen:  

- **Använd en proxyserver vid synkronisering av programuppdateringar**  

- **Använd en proxyserver vid nedladdning av innehåll med hjälp av automatiska distributionsregler**  

    > [!NOTE]
    > Den här inställningen används inte av program uppdaterings platser på sekundära platser när den är tillgänglig för användning.  

Inställningarna finns på fliken **Inställningar för proxy och konto** i egenskaperna för program uppdaterings platsen.  

> [!NOTE]
> Som standard används **system** kontot på plats servern för den plats där en regel för automatisk distribution skapades för att ansluta till Internet och ladda ned program uppdateringar när reglerna för automatisk distribution körs. Du kan också konfigurera och använda plats systemets Proxy Server-konto. 
>
> Om det här kontot inte kan ansluta till Internet går det inte att ladda ned program uppdateringar. Följande post loggas i **RuleEngine. log**:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a>Andra funktioner som använder proxyn för en plats system Server

*(Lanseras i version 2002)*

Från och med Configuration Manager version 2002 använder följande funktioner proxyn för det plats system som är värd för [tjänst anslutnings punkt](#service-connection-point) rollen: <!--5913817-->

- [Azure Active Directory (Azure AD) identifiering av användare](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Identifiering av Azure AD-användargrupp](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Synkroniserar samlings medlemskaps resultat till Azure Active Directory grupper](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Konfigurera proxyn för en plats system Server  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **servrar och plats system roller** .  

2. Välj den plats system server som du vill redigera. I informations fönstret högerklickar du på **plats system** rollen och väljer **Egenskaper**.  

3. I egenskaper för plats system växlar du till fliken **proxy** . Konfigurera följande proxyinställningar:  

    - **Använd en proxyserver vid synkronisering av information från Internet**: Välj det här alternativet om du vill att plats system servern ska använda en proxyserver.  

    - **Proxyserverns namn**: Ange värd namnet eller FQDN för proxyservern i din miljö.  

    - **Port**: Ange den nätverks port som ska kommunicera med proxyservern. Som standard använder den port **80**.  

    - **Använd autentiseringsuppgifter för att ansluta till proxyservern**: många proxyservrar kräver att en användare autentiseras. Som standard använder plats system servern sitt dator konto för att ansluta till proxyservern. Om det behövs aktiverar du det här alternativet, klickar på **Ange**och väljer sedan ett **befintligt konto** eller anger ett **nytt konto**. Dessa autentiseringsuppgifter är **Server kontot för plats systemets proxyserver**.  Mer information finns i [konton som används i Configuration Manager](../hierarchy/accounts.md).  

4. Välj **OK** för att spara den nya konfigurationen av proxyservern.  

## <a name="next-steps"></a>Nästa steg

Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, måste du tillåta åtkomst till Internet-slutpunkter. Mer information finns i [krav för Internet åtkomst](internet-endpoints.md).
