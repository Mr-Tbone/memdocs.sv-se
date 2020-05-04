---
title: Stöd för Active Directory-domäner
titleSuffix: Configuration Manager
description: Lär dig mer om kraven för ett Configuration Manager-plats system i en Active Directory-domän.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709616"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Stöd för Active Directory domäner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Alla Configuration Manager-plats system måste vara medlemmar i en Active Directory-domän som stöds. Configuration Manager klient datorer kan vara domän medlemmar eller arbets grupps medlemmar.  

## <a name="requirements-and-limitations"></a>Krav och begränsningar

- Domän medlemskap gäller även för plats system som stöder internetbaserad klient hantering i ett perimeternätverk. (Dessa nätverk kallas även DMZ, demilitariserad Zone och skärmat undernät).  

- Det finns inte stöd för att ändra följande konfigurationer för en dator som är värd för en plats system roll:  

  - Domän medlemskap, inklusive om du tar bort ett plats system från domänen och sedan återansluter till samma domän.

  - Domännamn  

  - Datornamn  

  Avinstallera plats system rollen innan du gör dessa ändringar. Om du vill göra dessa ändringar på en plats Server måste du först avinstallera platsen. Du kan också överväga att skapa en [plats server i passivt läge](../../servers/deploy/configure/site-server-high-availability.md) för att kunna hantera den här ändringen på en plats Server.

- Configuration Manager stöder domän-och skogs funktions nivån för Windows Server 2008 R2 eller senare.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Åtskilt namnområde

Du kan installera Configuration Manager plats system och klienter i en domän som har en *åtskild namnrymd*.  

I ett åtskilt namn område matchar inte datorns primära DNS-suffix det Active Directory DNS-domännamnet för datorn. Ett annat scenario med åtskilda namn områden uppstår om NetBIOS-domännamnet för en domänkontrollant inte matchar Active Directory DNS-domännamnet.  

### <a name="disjoint-scenarios"></a>Osammanhängande scenarier

I följande avsnitt hittar du de scenarier som stöds för ett osammanhängande namn område.  

#### <a name="scenario-1"></a>Scenario 1

Domänkontrollantens primära DNS-suffix skiljer sig från DNS-domännamnet i Active Directory. Datorer som är medlemmar i domänen kan vara åtskilda eller inte åtskilda.

Domänkontrollanten är åtskild i det här scenariot. Datorer som är medlemmar i domänen, t. ex. plats servrar och datorer, kan ha ett primärt DNS-suffix som antingen matchar:

- Domänkontrollantens primära DNS-suffix
- DNS-domännamnet för Active Directory

#### <a name="scenario-2"></a>Scenario 2

En medlems dator i en Active Directory domän är åtskild, även om domänkontrollanten inte är åtskild.

I det här scenariot skiljer sig det primära DNS-suffixet för ett plats system från det Active Directory DNS-domännamnet. Domänkontrollantens primära DNS-suffix är samma som namnet på den Active Directory DNS-domänen. Medlems datorer som Configuration Manager-klienter kan ha ett primärt DNS-suffix som antingen matchar:

- Det primära DNS-suffixet för den åtskilda plats system servern
- DNS-domännamnet för Active Directory

### <a name="configure-disjoint-namespace"></a>Konfigurera åtskild namnrymd

Om du vill ge en dator åtkomst till domänkontrollanter som är åtskilda ändrar du attributet **msDS-AllowedDNSSuffixes** Active Directory på domän objekts behållaren. Lägg till båda DNS-suffixen till attributet.  

För att se till att *Sök listan för DNS-suffix* innehåller alla DNS-namnområden i organisationen konfigurerar du Sök listan för varje dator i den åtskilda domänen. Inkludera följande suffix i listan över namn områden:

- Domänkontrollantens primära DNS-suffix
- DNS-domännamnet
- Ytterligare namn områden för andra servrar som Configuration Manager kan kommunicera med

Du kan använda grup principer för att konfigurera **Sök listan Domain Name System (DNS)** .  

> [!IMPORTANT]  
> När du refererar till en dator i Configuration Manager anger du datorn med hjälp av dess primära DNS-suffix. Det här suffixet måste matcha det fullständigt kvalificerade domän namnet som är registrerat som **dNSHostName** -attributet i Active Directory-domänen och tjänstens huvud namn som är associerat med systemet.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Enkla domännamn utan toppdomän

Configuration Manager stöder plats system och klienter i en enda etikett domän när följande villkor uppfylls:  

- Konfigurera den enkla etiketten domän i Active Directory Domain Services med ett separat DNS-namnområde som har en giltig toppnivå domän.  

  **Exempel:** Det enkla domännamnet Contoso är konfigurerat med ett åtskilt namnområde i DNS, contoso.com. När du anger DNS-suffixet i Configuration Manager för en dator i Contoso-domänen anger du "Contoso.com" och inte "contoso".  

- DCOM-anslutningar mellan plats servrar i system kontexten måste lyckas med Kerberos-autentisering.  
